<div align="center">

# 🎙️ Awaaz

### *Sirf boliye, kaam ho jaayega* — "Just speak, and it's done."

**A voice-first assistant for elderly people who cannot use apps.**

[![Live demo](https://img.shields.io/badge/Live%20demo-Try%20it-ff7a45?style=for-the-badge)](https://vocal-sunshine-f192d7.netlify.app)
[![Demo video](https://img.shields.io/badge/Video-2%3A33%20min-CD201F?style=for-the-badge&logo=youtube)](https://youtu.be/tyo7MFopw24)
[![Devpost](https://img.shields.io/badge/Devpost-HackSocial%202026-003e54?style=for-the-badge)](https://devpost.com/software/awaaz-sirf-boliye-kaam-ho-jaayega)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![PWA](https://img.shields.io/badge/PWA-installable-5A0FC8?style=flat-square)](https://developer.mozilla.org/en-US/docs/Progressive_web_apps)
[![Offline](https://img.shields.io/badge/Offline-first-brightgreen?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
[![Languages](https://img.shields.io/badge/Languages-3%20complete-orange?style=flat-square)](#three-languages)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

<br>

<i>Press one big button. Speak in हिंदी, मराठी or English. It does the task — and says the answer back out loud.</i>

</div>
help center link 🔗 - stupendous-souffle-fae9dc.netlify.app
---

## Table of contents

- [The problem](#the-problem)
- [What Awaaz does](#what-awaaz-does)
- [Three languages, all complete](#three-languages-all-complete)
- [Quick start](#quick-start)
- [Voice command reference](#voice-command-reference)
- [How it is built](#how-it-is-built)
- [Documentation](#documentation)
- [Testing](#testing)
- [Accessibility](#accessibility)
- [Privacy](#privacy)
- [Browser support](#browser-support)
- [Known limitations](#known-limitations)
- [Roadmap](#roadmap)
- [License](#license)
- [Author](#author)

---

## The problem

It was 8 in the morning and my grandfather was standing in the doorway with his phone in his hand, holding it out to me the way you hand someone something broken.

> *"Beta, ye kaise karta hai?"*

He needed a medicine reminder. Fifteen seconds of work for me. For him, an afternoon of waiting until someone came home.

He is not sick. He is not unwilling. He is not slow. He is simply **locked out by design**. Over **100 million elderly Indians** are on the wrong side of the same door, because every app ever built assumes three things: that you can read small text, that you can tap a tiny button, and that you can type.

**And every existing answer asks something of him in return.** A reminder app has to be installed and configured. A helpline has to be found and dialled. A wearable has to be worn, charged and remembered. An SOS button has to be reached — *which is useless in precisely the situation it exists for*. A voice assistant will help, if you speak English, and if you can see the screen well enough to find it. Marathi is an afterthought, where it exists at all.

The cruel part is how ordinary the failure looks from outside. Nothing is wrong. He just quietly stops trying, and the people who love him assume he is managing.

So Awaaz was built around one mandate: **speaking should be enough.** Not "speaking helps." Not "speaking, once you've set it up."

One more thing learned while building it: **a reminder that rings and is ignored is not help.** An unconfirmed dose is the one that matters. That is why Awaaz does not just remind — it notices when nobody answered, and it tells someone who can.

---

## What Awaaz does

Awaaz is a voice-first assistant designed from the ground up for elderly and low-literacy users. You press one big button, speak naturally, and it does the task — then **speaks the answer back out loud**, because many users cannot read the screen.

| | Feature | Notes |
|---|---|---|
| ⏰ | **Medicine reminders** | Fires with alarm + system notification + vibration + spoken alert |
| 🔁 | **Daily recurring reminders** | Reschedules itself for the next day, even after days of absence |
| 🚨 | **Missed-dose escalation** | If nobody confirms, escalates to a caregiver by call or WhatsApp |
| 👨‍👩‍👧 | **"Mere Apne" caregiver contacts** | Saved by voice; every SOS and escalation reaches a real person |
| 🆘 | **Emergency SOS** | Calls the saved contact and shares live location on WhatsApp |
| 📍 | **Location sharing** | WhatsApp deep-link, with a human confirmation step for safety |
| 🌤️ | **Live weather** | Open-Meteo API, no key required; answered aloud |
| 📖 | **Notes** | Save, read aloud, and delete — entirely by voice |
| 🧮 | **Voice calculator** | Postfix-aware, so "25 aur 30 jodo" works as spoken |
| 📅 | **Date and day** | Spoken, not displayed |
| 💚 | **Health tips** | Short, friendly, spoken |
| 🛡️ | **Scam check** | Explains whether a suspicious message is risky |
| 📴 | **Offline core** | Notes, reminders, calculator, contacts, SOS — no internet needed |
| ♿ | **Accessibility controls** | Dark mode, font scaling, ARIA labels, screen-reader live region |
| ⌨️ | **Type-to-command fallback** | Every command also works by typing, if speech is not possible |
| 🎓 | **First-run voice tutorial** | Four steps, read aloud, with a 🔊 *Suno* (Listen) button |

### The missed-dose escalation loop

Most health apps remind. Awaaz closes the loop:

1. A reminder fires — notification, sound, vibration, and a spoken alert (twice).
2. A confirmation window opens (3 minutes by default).
3. If nobody taps **"Theek hai"**, a loud banner appears: *"Dawai confirm nahi hui"*.
4. One tap calls the caregiver, or opens WhatsApp with a prefilled message.
5. Confirming the dose at any point cancels the escalation.

> An unconfirmed dose is the one that matters. This is the failure mode other reminder apps leave open.

---

## Three languages, all complete

हिंदी · मराठी · English — and none of them is a second-class citizen.

This is **verified, not claimed**: the app reports at runtime that all three locales carry the same **52 strings and the same 15 voice commands** (11 UI keys + 41 response keys × 3). Adding a partial language is easy; keeping three in lockstep is the part teams skip.

| Hindi | Marathi | English |
|---|---|---|
| "सुबह 8 बजे दवाई याद दिलाओ" | "सकाळी 8 वाजता औषध आठवण कर" | "Remind medicine at 8 am" |
| "नागपूर का मौसम बताओ" | "नागपूरचे हवामान सांग" | "Weather in Nagpur" |
| "मेरी लोकेशन भेजो" | "माझी लोकेशन पाठव" | "Send my location" |

Marathi was non-negotiable from day one — it is the language my family actually thinks in, and the apps that bother with India usually stop at Hindi.

---

## Quick start

**Option 1 — just open it**

```bash
# Download the single file and open it in any modern browser
open awaaz.html          # macOS
start awaaz.html         # Windows
xdg-open awaaz.html      # Linux
```

**Option 2 — serve it locally** (recommended: service workers need `http://` or `https://`)

```bash
python3 -m http.server 8000
# then open http://localhost:8000/awaaz.html
```

**Option 3 — install it as an app**

Open the hosted version on a phone and choose *"Add to Home Screen"*. It installs as a PWA and works offline.

That is the whole setup. There is **no build step, no package install, no API key, and no server**.

---

## Voice command reference

<details>
<summary><b>हिंदी (Hindi)</b></summary>

| Say this | What happens |
|---|---|
| "शाम 5 बजे डॉक्टर जाना याद दिलाओ" | Alarm rings at 5 pm |
| "सुबह 8 बजे दवाई याद दिलाओ" | Medicine reminder |
| "रोज़ सुबह 8 बजे दवाई याद दिलाओ" | Daily recurring reminder |
| "मेरे नोट्स सुनाओ" | Reads all notes aloud |
| "नागपूर का मौसम बताओ" | Live weather |
| "98765 43210 पे कॉल लगाओ" | Starts a call |
| "मेरी लोकेशन भेजो" | Shares location on WhatsApp |
| "25 और 30 जोड़ो" | Calculator |
| "आज कौनसा दिन है" | Date and day |
| "सेहत की सलाह दो" | Health tip |
| "पहला नोट हटाओ" / "सब हटाओ" | Delete notes |
| "डार्क मोड करो" / "टेक्स्ट बड़ा करो" | Accessibility |

</details>

<details>
<summary><b>मराठी (Marathi)</b></summary>

| Say this | What happens |
|---|---|
| "संध्याकाळी 5 वाजता डॉक्टर आठवण कर" | योग्य वेळी अलार्म |
| "सकाळी 8 वाजता औषध आठवण कर" | औषधाची आठवण |
| "माझ्या नोंदी वाच" | सर्व नोंदी वाचून दाखवते |
| "नागपूरचे हवामान सांग" | थेट हवामान |
| "माझी लोकेशन पाठव" | WhatsApp वर लोकेशन |
| "25 आणि 30 जोड" | हिशोब |
| "आज कोणता वार आहे" | तारीख आणि वार |
| "डार्क मोड कर" / "अक्षरे मोठी कर" | सुलभता |

</details>

<details>
<summary><b>English</b></summary>

| Say this | What happens |
|---|---|
| "Remind me doctor at 5 pm" | Alarm rings at 5 pm |
| "Remind medicine at 8 am" | Medicine reminder |
| "Remind medicine every day at 8 am" | Daily recurring reminder |
| "Read my notes" | Reads all notes aloud |
| "Weather in Nagpur" | Live weather |
| "Call 98765 43210" | Starts a call |
| "Send my location" | Shares location on WhatsApp |
| "Add 25 and 30" | Calculator |
| "What day is today" | Date and day |
| "Give a health tip" | Wellness tip |
| "Delete first note" / "delete all" | Delete notes |
| "Dark mode" / "Make text bigger" | Accessibility |

</details>

Full reference: [`COMMANDS.md`](COMMANDS.md)

---

## How it is built

```
┌─────────────────────────────────────────────────────────────┐
│                    ONE SELF-CONTAINED HTML FILE              │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  🎤 INPUT LAYER        Web Speech API (SpeechRecognition)    │
│                        + type-to-command fallback            │
│                              │                               │
│                              ▼                               │
│  🧭 COMMAND ROUTER      ordered regex handlers               │
│                        15 command families × 3 languages     │
│                              │                               │
│      ┌───────────────┬───────┴───────┬──────────────┐        │
│      ▼               ▼               ▼              ▼        │
│  ⏰ REMINDERS    📝 NOTES      🌤️ WEATHER      🆘 SOS         │
│  alarm + notif   localStorage  Open-Meteo    call + location  │
│  + escalation    (on-device)   (free API)    (WhatsApp link)  │
│      │                                                        │
│      ▼                                                        │
│  🚨 ESCALATION ENGINE   3-min confirmation window             │
│                         → caregiver call / WhatsApp           │
│                              │                               │
│                              ▼                               │
│  🔊 OUTPUT LAYER       SpeechSynthesis + ARIA live region     │
│                        + system notification + vibration      │
├─────────────────────────────────────────────────────────────┤
│  💾 Persistence: localStorage  │  📴 Offline: Service Worker  │
│  📱 Installable: inline PWA manifest  │  🔒 No backend, ever  │
└─────────────────────────────────────────────────────────────┘
```

| Concern | Choice | Why |
|---|---|---|
| Structure | One HTML file | Runs anywhere, no build, no dependency, cannot break |
| Speech in | `SpeechRecognition` — `hi-IN`, `mr-IN`, `en-IN` | Native, offline-capable on device, no API cost |
| Speech out | `SpeechSynthesis` | Essential: many users cannot read the screen |
| Persistence | `localStorage` | No account, no server, no sync, no data leaving the phone |
| Reminders | `Notification` API + Service Worker | Reaches the user when the app is minimised |
| Alarm tone | WebAudio oscillator | Generated, so no audio files ship with the app |
| Weather | Open-Meteo | Free, no key, no quota card |
| Location | Geolocation + `wa.me` deep-link | Human confirmation before anything is sent |
| Install | Inline PWA manifest (data URI) | Installable without a separate manifest file |

Deep dive: [`ARCHITECTURE.md`](ARCHITECTURE.md)

---

## Documentation

| Document | What it covers |
|---|---|
| [`ARCHITECTURE.md`](ARCHITECTURE.md) | Command router, reminder + escalation engine, storage schema, language system |
| [`COMMANDS.md`](COMMANDS.md) | Complete voice-command reference in all three languages |
| [`TESTING.md`](TESTING.md) | What the automated suite covers and how to run it |
| [`ACCESSIBILITY.md`](ACCESSIBILITY.md) | ARIA, screen readers, font scaling, contrast, motor accessibility |
| [`PRIVACY.md`](PRIVACY.md) | What is stored, where, and what never leaves the device |

---

## Testing

The project ships with an automated **jsdom test suite of 80 cases** covering:

- command routing and handler ordering
- the postfix-aware calculator
- reminder scheduling, recurrence, and catch-up after absence
- the missed-dose escalation window
- notification behaviour
- XSS safety of rendered user input
- language parity across all three locales

```
80 passed, 0 failed
```

Details: [`TESTING.md`](TESTING.md)

---

## Accessibility

Accessibility is not a feature added at the end — it is the whole design.

- **Voice-first**: nothing requires reading, typing, or precise tapping
- **Spoken output**: every reply is read aloud, not just displayed
- **ARIA labels** in all three languages, on every interactive control
- **Live region** (`aria-live="polite"`) so screen readers announce each reply
- **Skip-to-mic link** — one keystroke to the primary control
- **Font scaling** by voice ("Text bada karo") or button
- **High-contrast dark mode**
- **Huge tap targets** — the primary button is the largest element on screen
- **Type-to-command fallback** for users who cannot speak or are not understood

Details: [`ACCESSIBILITY.md`](ACCESSIBILITY.md)

---

## Privacy

- **No account. No login. No email.**
- **No server, no database, no analytics, no telemetry.**
- **No face recognition, no cloud processing of voice.**
- Everything — notes, reminders, caregiver numbers, settings — lives in the phone's own `localStorage`.
- The only network calls are: weather (Open-Meteo, city name only) and the WhatsApp deep-link the user triggers.

Details: [`PRIVACY.md`](PRIVACY.md)

---

## Browser support

| Browser | Speech recognition | Speech synthesis | Notes |
|---|---|---|---|
| Chrome / Edge (desktop + Android) | ✅ | ✅ | Fully supported |
| Safari (iOS / macOS) | ✅ | ✅ | Requires a user gesture to start audio |
| Firefox | ⚠️ partial | ✅ | Type-to-command fallback covers recognition |
| Any browser, offline | ✅ core | ✅ | Weather is the only feature needing a network |

---

## Known limitations

Stated plainly, because an honest limitation builds more trust than an over-claim:

- **True background push is not implemented.** Reminders fire while the app is open or minimised, and any reminder missed while away fires the moment the app is reopened. Firing while the app is *fully closed* needs a push server or a native wrapper.
- **Speech recognition accuracy depends on the device's engine** and on ambient noise — hence the type-to-command fallback.
- **Reminders are device-local.** They do not sync between phones.
- **Three languages only** — Tamil, Telugu and Bengali are on the roadmap.

---

## Roadmap

- [ ] True background push (push server or Capacitor wrapper) so reminders survive a reboot
- [ ] Caregiver mode — a family member can add reminders remotely
- [ ] More Indian languages: Tamil, Telugu, Bengali
- [ ] A published, honest pilot report with real seniors
- [ ] Optional on-device wake word

---

## Project structure

```
awaaz-voice-assistant/
├── awaaz.html          # the entire application (single file, offline)
├── README.md           # this file
├── LICENSE             # MIT
├── ARCHITECTURE.md     # command router, reminder + escalation engine
├── COMMANDS.md         # voice-command reference (3 languages)
├── TESTING.md          # the 80-case test suite
├── ACCESSIBILITY.md    # ARIA, screen readers, contrast, motor access
└── PRIVACY.md          # what is stored, and what never leaves the device
```

---

## License

[MIT](LICENSE) — free to use, modify and build upon.

---

<div align="center">

### made with ✦ by **Samarth Mishra**

Built for **HackSocial 2026 — Hack the Change Again**

[![Live demo](https://img.shields.io/badge/🌐%20Try%20Awaaz-vocal--sunshine-f192d7-ff7a45?style=for-the-badge)](https://vocal-sunshine-f192d7.netlify.app)

</div>
