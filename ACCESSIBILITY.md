# Accessibility

> Accessibility is not a feature you add at the end. For this audience it **is** the product.

Awaaz is built for people who cannot read small text, cannot tap tiny targets, and often cannot type. Every decision below follows from that.

---

## 1. Voice is the primary interface

| Barrier | How Awaaz removes it |
|---|---|
| Cannot read | Every answer is **spoken**, not just displayed |
| Cannot type | One big button; no keyboard is ever required |
| Cannot find the control | The microphone button is the largest element on screen, above the fold |
| Cannot spell a command | Natural phrasing — the router is built for how people actually talk |
| Misunderstood by the engine | **Type-to-command fallback** uses the identical router |

---

## 2. Screen-reader support

| Feature | Implementation |
|---|---|
| Labels | `aria-label` on every interactive control, in **all three languages** |
| Live region | `aria-live="polite"` + `aria-atomic="true"` on the conversation container, so each reply is announced |
| Skip link | "Skip to microphone" — one keystroke to the primary control |
| Focus visibility | `:focus-visible` outline (3 px, accent colour, 2 px offset) on every control |
| Alerts | `role="alert"` on the missed-dose escalation banner |
| Semantics | Real `<button>` elements, never clickable `<div>`s |
| Labels re-translate | Switching language rebuilds and re-labels every panel — a label is never left in the wrong language |

Because Awaaz speaks its own replies, it also avoids a common failure mode in accessible apps: **competing speech**. The app does not rely on the user running a screen reader at all, so there is no collision between Awaaz's voice and NVDA/TalkBack.

---

## 3. Vision

| Control | Availability |
|---|---|
| Font scaling | 🔍+ / 🔍− buttons **and** voice ("Text bada karo") |
| High-contrast dark mode | 🌗 button **and** voice ("Dark mode karo") |
| Contrast | Dark mode uses a warm high-contrast palette tested against the light theme |
| Target size | Primary button is the largest element; all secondary controls meet a 44 px minimum |
| Persistence | Font scale and dark mode survive reloads |
| No information by colour alone | Every state is also labelled in words |

---

## 4. Motor accessibility

- **One tap** starts anything. There are no double-taps, long-presses, or gestures.
- **No drag, no swipe, no precise aim.**
- Reminders can be acknowledged with a single large button (**✓ Theek hai**).
- Snooze is a single tap (10 minutes) — no time picker to fumble.
- Buttons are spaced to avoid accidental adjacent taps.

---

## 5. Cognitive accessibility

- **One screen, one job.** No navigation, no menus, no tabs, no settings maze.
- **Plain language** — short sentences, no jargon, in the user's mother tongue.
- **Repetition** — reminders are spoken twice; the missed-dose banner repeats the name of the medicine.
- **Confirmation, never punishment** — "Abhi le li" is always available; there is no failure state.
- **First-run tutorial**, four steps, read aloud, with a **🔊 Suno** button on every step.
- **No accounts, no passwords, no onboarding forms.**

---

## 6. Language accessibility

Hindi, मराठी and English are **all complete** — 52 strings and 15 commands each, verified at runtime. Marathi in particular is routinely skipped by Indian apps; here it is a first-class locale, because it is the language my family actually thinks in.

The app's own language-parity check makes an unfinished translation visible during development instead of during use.

---

## 7. Testing and verification

- Automated tests cover **language parity**, **label presence**, and **routing in all three languages** (see [TESTING.md](TESTING.md)).
- Layout verified across Hindi, Marathi and English at phone, tablet and desktop widths, in both light and dark mode.
- Screen-reader behaviour reviewed against NVDA (desktop) and TalkBack (Android) expectations.

---

## 8. Known gaps (honest)

- **Speech recognition accuracy** varies with device and ambient noise — mitigated by the typed fallback, not solved.
- **No on-device wake word** yet, so the first interaction is still a tap.
- **More Indian languages** (Tamil, Telugu, Bengali) are on the roadmap, not shipped.

---

## Design principle

> *"It reminded them" is not the same as "it helped them."*

The missed-dose escalation exists for exactly this reason. Accessibility means noticing when the user did **not** respond, not merely emitting an accessible notification.
