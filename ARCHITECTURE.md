# Architecture

Awaaz is deliberately a **single self-contained HTML file**. That constraint is a design decision, not a shortcut: it means the app cannot fail to install, has no build step, no dependency rot, and can be handed to a user on a ₹6,000 phone by a family member over Bluetooth.

---

## 1. Layers

```
🎤 Input        SpeechRecognition (hi-IN / mr-IN / en-IN)  ·  typed fallback
   │
🧭 Router       ordered regex handlers — first match wins
   │
   ├── ⏰ Reminders      → scheduling + alarm + escalation
   ├── 📝 Notes          → create / read aloud / delete
   ├── 🌤️ Weather        → Open-Meteo
   ├── 📞 Calls          → tel: intent
   ├── 📍 Location       → Geolocation + wa.me deep-link
   ├── 🆘 SOS            → call + location, human-confirmed
   ├── 🧮 Calculator     → postfix-aware
   ├── 📅 Date / 💚 Tips / 🛡️ Scam check
   └── ♿ Settings        → dark mode, font scale, language, tutorial
   │
🔊 Output       SpeechSynthesis  ·  ARIA live region  ·  Notification  ·  vibration
```

---

## 2. Input layer

| Path | Implementation | Notes |
|---|---|---|
| Speech | `webkitSpeechRecognition` with `lang` set from the active locale | `continuous = false`, `interimResults = false` |
| Locale | `hi-IN`, `mr-IN`, `en-IN` | Switched by the language buttons or by voice |
| Typed | Text input + send button | Every command routed identically, so nothing is voice-only |
| Safety | Browsers block autoplay audio until a gesture | Onboarding exposes a **🔊 Suno** button instead of talking unprompted |

The typed fallback is not a convenience — it is the accessibility guarantee for users who cannot speak, or whose speech the engine mishears.

---

## 3. Command router

`handleCommand(said)` runs an **ordered** list of pattern groups. Order matters because spoken Hindi and Marathi collide:

| # | Group | Why it is placed here |
|---|---|---|
| 0 | Set emergency number | Explicit, high-specificity pattern |
| 0a | **SOS** | Must win over anything else — safety first |
| 0a2 | Location share | Safety |
| 0a3 | Dark mode | Cheap, unambiguous |
| 0b | Font size | Cheap, unambiguous |
| 1 | Caregiver number | New: `caregiver 98765…` |
| 2 | Note taking | "note karo …" |
| 3 | Read notes | Must be checked **before** creating a note, or "notes sunao" saves a note called "notes sunao" |
| 4 | Weather | Needs a network; fails gracefully offline |
| 5 | Calculator | Postfix-aware: Hindi/Marathi often place the operator *after* the numbers |
| 6 | Date, tips, delete, misc | Lowest specificity |

**Collision lessons (real bugs, fixed):**

- `"notes sunao"` was being stored as a *new* note. The read handler now precedes the create handler.
- `"jodo"` (add) collided between note-creation and the calculator. The calculator is reached only when the phrase parses as arithmetic.

---

## 4. Reminder engine

### Data model

```js
// localStorage key: awaaz_notes_v2
{
  text:  "Subah 8 baje dawai",
  at:    1753939200000,   // epoch ms, or null for a plain note
  daily: true,            // recurring?
  fired: false            // one-shot reminders only
}
```

### Firing

`checkReminders()` runs on a timer and on every app open:

```
for each note with at <= now and not fired:
    fireAlarm(note)
    if daily → n.at += 24h (and skip forward past any missed days)
    else     → n.fired = true
```

- **Alarm** → full-screen card, `Notification`, vibration, WebAudio beep, and a spoken alert **twice** (elderly users miss the first one).
- **Catch-up** → any reminder that expired while the app was closed fires immediately on reopen.
- **Recurrence** → daily reminders reschedule themselves, so a phone switched off for three days does not lose the habit.

---

## 5. Escalation engine

The part that makes Awaaz more than a reminder app.

```
reminder fires
   │
   ├── user taps "Theek hai"  ──────────────► done (escalation cancelled)
   │
   └── no confirmation within 3 minutes
              │
              ▼
       escalation banner: "Dawai confirm nahi hui"
              │
              ├── 📞 Call caregiver      → tel:<number>
              ├── 💬 WhatsApp caregiver  → wa.me/<number>?text=<prefilled>
              └── ✅ "Abhi le li"        → cancel, log the help event
```

| Parameter | Value | Rationale |
|---|---|---|
| Confirmation window | 3 minutes (`ESC_MS`) | Long enough to be useful, short enough to matter |
| Demo window | 9 seconds | Only when `?demo=1`, so screenshots and demos are fast |
| Trigger | `fireAlarm` is wrapped | Any reminder, from any code path, is covered |
| Cancel | `stopAlarm` is wrapped | Acknowledging the alarm always cancels |
| Caregiver absent | Banner explains how to add one | Never a dead end |

**Design note:** an unconfirmed dose is the failure mode that matters in elderly care. Every other app in this space treats "we notified them" as success. Awaaz treats it as unfinished.

---

## 6. Language system

```js
T = { hi:{…}, mr:{…}, en:{…} }   // 11 UI keys + 15 command examples each
R = { hi:{…}, mr:{…}, en:{…} }   // 41 response templates each
```

A **runtime parity check** counts the keys and commands per locale and renders the result in the UI:

```
✅ भाषा 3/3 · 52 strings · 15 commands each
```

This exists because half-translations ship silently. If a string is missing in Marathi, the badge changes state immediately — the gap is visible during development instead of during judging.

---

## 7. Storage

| Key | Contents |
|---|---|
| `awaaz_notes_v2` | Notes and reminders (array) |
| `awaaz_sos` | Emergency number |
| `awaaz_care_v1` | Caregiver contacts `[{name, num}]` |
| `awaaz_impact` | Help counter for today |
| `awaaz_pilot_v1` | Cumulative help counter |
| `awaaz_dark` | Dark-mode preference |
| `awaaz_font` | Font-scale step |
| `awaaz_onboard` | Whether the tutorial has been seen |

All of it is device-local. Nothing is transmitted.

---

## 8. Offline & installability

| Feature | Mechanism |
|---|---|
| Offline shell | Service Worker registered from an inline Blob URL |
| Install | PWA manifest inlined as a `data:` URI (no extra file) |
| Icon | Inline SVG data URI (also removes a favicon 404) |
| Core features offline | Notes, reminders, calculator, SOS contacts, voice loop |
| Network-dependent | Weather only — and it degrades with a spoken apology |

Because everything is inlined, the deployed file makes **zero external requests** at load time.

---

## 9. Output layer

Every reply goes out through **four** channels at once, because the target user may not be looking at the screen:

1. **Speech** — `speechSynthesis`, in the active locale
2. **Visual** — a large-text conversation card
3. **ARIA live region** — announced by screen readers
4. **Notification + vibration** — for reminders and escalations

---

## 10. Safety decisions

| Decision | Reason |
|---|---|
| SOS location opens WhatsApp instead of sending | A wrong number must never receive a live location without a human confirming |
| Escalation waits for confirmation | Avoids crying wolf on every missed tap |
| Scam check explains, never commands | An elderly user should not be told what to do with their money |
| No autoplay speech | Browsers block it anyway, and unprompted speech frightens this audience |
