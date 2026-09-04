# Privacy

Awaaz is built for elderly users who are frequent targets of fraud. Privacy here is not a policy — it is an architectural property.

## The short version

| | |
|---|---|
| Account required | **No** |
| Login / email / phone verification | **No** |
| Server | **None** |
| Database | **None** |
| Analytics / telemetry / tracking cookies | **None** |
| Cloud processing of voice | **None** |
| Face recognition or biometrics | **None** |
| Data leaving the device | **Only a city name**, when you ask for the weather |

---

## What is stored, and where

Everything lives in the phone's own **localStorage**. It never leaves the device.

| Key | Contents |
|---|---|
| `awaaz_notes_v2` | Your notes and reminders |
| `awaaz_sos` | Your emergency number |
| `awaaz_care_v1` | Caregiver contacts (name + number) |
| `awaaz_impact` | How many times Awaaz helped today |
| `awaaz_pilot_v1` | Cumulative help counter |
| `awaaz_dark` | Dark-mode preference |
| `awaaz_font` | Font-size preference |
| `awaaz_onboard` | Whether the tutorial has been seen |

Clearing the browser's site data removes all of it. There is no copy anywhere else, because there is nowhere else.

---

## Network requests

The app makes **zero requests at load time** — it is a single self-contained HTML file.

At runtime there is exactly **one** outgoing request, and only when you ask for it:

| Request | When | What is sent | What comes back |
|---|---|---|---|
| Open-Meteo | You ask for the weather | The **city name only** | Current temperature and conditions |

No identifier, no device ID, no location coordinate, no user agent is packaged with it.

WhatsApp and phone links (`wa.me`, `tel:`) are **local intents** — they hand off to an app already installed on the phone. Awaaz does not send anything on your behalf.

---

## Voice

Speech recognition uses the browser's built-in engine (`SpeechRecognition`), configured with the locale you selected (`hi-IN`, `mr-IN`, `en-IN`). Depending on the browser and OS, that engine may run on-device or use the platform's own service — Awaaz adds **no** cloud speech provider of its own and records nothing.

---

## Permissions

| Permission | Requested when | Required? |
|---|---|---|
| Microphone | You press the mic button | Optional — typing works identically |
| Notifications | First time you set a reminder | Optional — the in-app alarm still fires |
| Location | You ask to share your location | Optional, only for that action |

Every permission can be denied, and the app keeps working.

---

## Safety by design

| Risk | Mitigation |
|---|---|
| An SOS leaking location to the wrong number | Location opens in **WhatsApp** for a human to confirm before sending — it is never sent automatically |
| A scam message tricking the user | The scam check **explains** risk factors; it never instructs the user what to do with money |
| A stranger adding a caregiver | Caregiver contacts are added by the user, on their own device |
| Data breach | There is no server to breach |

---

## Children and vulnerable adults

Awaaz collects nothing that could identify a user, so there is no profile to protect. This makes it suitable for precisely the audience most at risk online — people who cannot reliably read a privacy policy.

---

## Questions

Open an issue on the repository. There is no data controller, because there is no data.
