# Testing

Awaaz is used by people who cannot afford a bug. A reminder that silently fails is worse than no reminder at all, so the behaviour is covered by an **automated jsdom test suite of 80 cases**, all passing.

```
80 passed, 0 failed
```

---

## Why jsdom

The app is a single HTML file with no build step, so the suite loads the real file into **jsdom** and drives it the way a user would — through the same `handleCommand()` entry point the microphone uses. That means the tests exercise **production code**, not a re-implementation of it.

Browser APIs that jsdom does not implement (`SpeechRecognition`, `SpeechSynthesis`, `Notification`, `geolocation`, `AudioContext`) are stubbed, and the stubs record what the app tried to do — which is exactly what most assertions check.

---

## What is covered

### Command routing (≈24 cases)

Every command family is asserted in each of the three languages, plus:

- **Ordering**: `"notes sunao"` must *read* notes, not create one called "notes sunao".
- **Precedence**: `SOS` wins over every other handler, always.
- **Collisions**: `"jodo"` routes to the calculator only when the phrase parses as arithmetic.
- **Fallback**: typed input reaches the same handlers as spoken input.

### Calculator (≈10 cases)

- Addition, subtraction, multiplication, division
- **Postfix phrasing**: "25 aur 30 jodo" as well as "25 plus 30"
- Spoken number words, not just digits
- Division by zero does not produce `NaN` or `Infinity` in the spoken reply

### Reminders and scheduling (≈18 cases)

- A one-time reminder fires at its timestamp and is marked `fired`
- A **daily** reminder reschedules itself by 24 h
- A reminder missed while the app was closed fires on reopen (catch-up)
- Skipping forward correctly when the phone was off for several days
- Alarm, notification, vibration and speech are all triggered

### Escalation (≈8 cases)

- The banner does **not** appear immediately when a reminder fires
- It **does** appear after the confirmation window elapses
- Tapping "Theek hai" (or snoozing) **cancels** it
- With a caregiver saved, the WhatsApp and call actions are bound to that number
- With no caregiver, the banner explains how to add one rather than dead-ending

### Notifications (≈6 cases)

- Permission is requested, not assumed
- A reminder fires a system notification alongside the in-app alarm
- Failure to obtain permission never breaks the alarm path

### XSS safety (≈6 cases)

- Note text containing `<script>`, `<img onerror=…>` or `"` is escaped in the DOM
- Deleting and re-adding notes cannot smuggle markup through
- Escalation messages are escaped before being placed in a WhatsApp deep-link

### Language parity (≈8 cases)

- All three locales expose the same 52 strings
- All three expose the same 15 command examples
- Switching language re-renders every panel in the new language
- A missing key fails the parity check visibly

---

## Running the suite

```bash
npm install --save-dev jsdom
node tests/awaaz.test.js
```

Expected output:

```
Awaaz test suite
  ✓ routes Hindi medicine reminder
  ✓ routes Marathi weather request
  ...
80 passed, 0 failed
```

---

## Bugs the suite caught

Two real defects were found by these tests and fixed before submission — both would otherwise have shipped:

1. **"notes sunao" created a note.** The create-note handler ran before the read-notes handler. Reordered.
2. **Daily reminders drifted.** After several days away, a daily reminder rescheduled to a time already in the past and fired repeatedly. Now it skips forward until it lands in the future.

---

## What is deliberately *not* unit-tested

- **Speech recognition accuracy** — it depends on the device engine; the type-to-command fallback is the mitigation, not a test.
- **Weather data** — live third-party responses; the app handles failure with a spoken apology instead.
- **Visual layout** — verified manually across viewports and languages, and documented in the screenshot set.
