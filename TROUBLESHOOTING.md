# Troubleshooting / समस्या निवारण / अडचणींचे निराकरण

> Written for elderly users and their families. Plain language, no jargon.

---

## 🔴 "I press the button and nothing happens"

| Cause | Fix |
|---|---|
| Microphone permission was denied | Browser settings → Site settings → Microphone → **Allow** for this site. Then reload. |
| You are offline and the browser blocked the service worker | Reconnect once, then it keeps working offline afterwards |
| The page needs a reload | Close the tab and reopen the app from the home-screen icon |

---

## 🔴 "It does not understand what I say"

1. **Wait for the prompt.** Press 🎙️, wait for *"Sun rahi hoon…"*, **then** speak. Speaking too early is the most common cause.
2. **Speak a little slower**, but normally — do not shout.
3. **Reduce noise.** Turn the TV or fan down if you can.
4. **Check the language.** If you are speaking मराठी but the app is set to हिंदी, tap **मराठी** at the top.
5. **Just type it.** Use the text box and send the same sentence — every command works by typing too.

---

## 🔴 "It hears me but says it did not understand"

The words were heard but no command matched. Try phrasing it the way you would say it to a person:

| Instead of | Say |
|---|---|
| "REMIND MEDICINE" | "Subah 8 baje dawai yaad dilao" |
| "weather" | "Nagpur ka mausam batao" |
| "delete" | "Pehla note hatao" |

---

## 🔴 "The reminder did not ring"

| Situation | What to do |
|---|---|
| **The app was open or minimised** | Reminders always fire in this state. Check that notification permission is **Allow**. |
| **The app was fully closed** | Awaaz fires any missed reminder the moment you reopen it. Open the app and it will speak the missed reminder. |
| **The phone was switched off** | Daily reminders reschedule themselves, so tomorrow's reminder still works. |
| **Phone was on silent** | The notification may be silent, but the in-app alarm, vibration and spoken alert still fire. |

> **Honest limitation:** Awaaz cannot ring while the app is fully closed and the phone is locked. That needs a push server or a native app — it is on the [roadmap](../README.md#roadmap).

---

## 🔴 "The weather does not work"

Weather needs the internet. Everything else — notes, reminders, calculator, SOS — works offline. If the weather fails, Awaaz says so out loud instead of failing silently.

---

## 🔴 "It speaks but I cannot hear it"

| Cause | Fix |
|---|---|
| Phone on silent / media volume at zero | Raise the **media** volume (not the ringer) |
| Bluetooth device connected | Disconnect it, or select the phone speaker |
| Browser blocked autoplay audio | Tap the **🔊 Suno** button — browsers only allow speech after you touch something |

---

## 🔴 "The SOS did not call anyone"

SOS calls the number saved as your emergency contact. If none is saved, nothing can be called.

Say: **"SOS number 98765 43210"**, or tap the emergency number field and save one.

---

## 🔴 "I lost all my notes"

Notes are stored **on the phone itself**, in browser storage. They are deleted if you:
- clear browser data / site data, or
- use private/incognito mode and close it.

There is no cloud copy, by design — see [PRIVACY.md](PRIVACY.md).

---

## 🔴 "The text is too small"

Say **"Text bada karo"**, or tap the 🔍+ button at the top. The setting is remembered.

---

## 🔴 "It hurts my eyes at night"

Say **"Dark mode karo"**, or tap 🌗. It switches to a high-contrast dark theme.

---

## Still stuck?

Every command also works by **typing**. If speech is not cooperating today, typing does exactly the same thing.
