# Voice command reference

Every command below works in **हिंदी**, **मराठी** and **English**. Anything you can say, you can also **type** — the typed path uses the exact same router, so nothing is voice-only.

> **How to speak:** press the big 🎙️ button once, wait for *"Sun rahi hoon…"*, then speak naturally. There is no wake word and no special syntax.

---

## ⏰ Reminders

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "शाम 5 बजे डॉक्टर जाना याद दिलाओ" | "संध्याकाळी 5 वाजता डॉक्टर आठवण कर" | "Remind me doctor at 5 pm" | One-time alarm |
| "सुबह 8 बजे दवाई याद दिलाओ" | "सकाळी 8 वाजता औषध आठवण कर" | "Remind medicine at 8 am" | Medicine reminder |
| "रोज़ सुबह 8 बजे दवाई याद दिलाओ" | "रोज सकाळी 8 वाजता औषध आठवण कर" | "Remind medicine every day at 8 am" | 🔁 Daily recurring |

**Behaviour:** fires with a full-screen alarm, a system notification, vibration, a WebAudio beep, and a **spoken alert twice**. If the app was closed when it was due, it fires the moment Awaaz is reopened.

**If nobody confirms within 3 minutes** → see [Missed-dose escalation](#-missed-dose-escalation).

---

## 🚨 Missed-dose escalation

Not a spoken command — an automatic safety net. When a reminder fires and nobody taps **"Theek hai"**, Awaaz waits, then shows:

> ⚠️ **Dawai confirm nahi hui** — *[the reminder text]*
> 📞 Call · 💬 WhatsApp · ✅ Abhi le li

**Add a caregiver first** (otherwise the banner asks you to):

| हिंदी | मराठी | English |
|---|---|---|
| "caregiver number 98765 43210" | "caregiver number 98765 43210" | "caregiver number 98765 43210" |

You can also tap **+ Caregiver number jodo** in the *Mere Apne* card.

---

## 🆘 Emergency

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "SOS" / "बचाओ" / "मदद करो" | "SOS" / "मदत करा" | "SOS" / "emergency" / "help me" | Calls the saved contact |
| "मेरी लोकेशन भेजो" | "माझी लोकेशन पाठव" | "Send my location" | Shares live location on WhatsApp |
| "SOS number 98765 43210" | "आपत्कालीन नंबर 98765 43210" | "emergency number 98765 43210" | Sets the emergency number |

The red **🆘 SOS** button does the same thing without speaking.

**Safety:** location is opened in WhatsApp for a human to confirm before sending — a mistyped number must never receive a live location automatically.

---

## 📝 Notes

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "नोट करो — कल बाज़ार जाना है" | "नोंद कर — उद्या बाजारात जायचे आहे" | "Note — go to market tomorrow" | Saves a note |
| "मेरे नोट्स सुनाओ" | "माझ्या नोंदी वाच" | "Read my notes" | Reads every note aloud |
| "पहला नोट हटाओ" | "पहिली नोंद काढ" | "Delete first note" | Deletes by position |
| "सब हटाओ" | "सर्व काढ" | "Delete all" | Clears the list |

---

## 🌤️ Weather

| हिंदी | मराठी | English |
|---|---|---|
| "नागपूर का मौसम बताओ" | "नागपूरचे हवामान सांग" | "Weather in Nagpur" |

Live data from **Open-Meteo** (free, no API key). The answer is **spoken**, not just displayed. Needs a network — offline it says so aloud instead of failing silently.

---

## 📞 Calls

| हिंदी | मराठी | English |
|---|---|---|
| "98765 43210 पे कॉल लगाओ" | "98765 वर कॉल कर" | "Call 98765 43210" |

Opens the phone dialler with the number filled in, so the user only has to press the green button.

---

## 🧮 Calculator

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "25 और 30 जोड़ो" | "25 आणि 30 जोड" | "Add 25 and 30" | 55 |

The calculator is **postfix-aware**, because Hindi and Marathi commonly place the operator *after* the numbers ("25 aur 30 jodo").

---

## 📅 Date, tips, reading

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "आज कौनसा दिन है" | "आज कोणता वार आहे" | "What day is today" | Speaks the date and weekday |
| "सेहत की सलाह दो" | "आरोग्य सल्ला दे" | "Give a health tip" | A short spoken wellness tip |
| "ये पढ़ो — [कोई बात]" | "हे वाच — […]" | "Read this — […]" | Reads any text aloud |
| "ये SMS स्कैम है?" | "हा मेसेज स्कॅम आहे का?" | "Is this SMS a scam?" | Explains the risk factors |

---

## ♿ Accessibility & settings

| हिंदी | मराठी | English | Result |
|---|---|---|---|
| "डार्क मोड करो" | "डार्क मोड कर" | "Dark mode" | Toggles high-contrast dark mode |
| "टेक्स्ट बड़ा करो" | "अक्षरे मोठी कर" | "Make text bigger" | Increases the font scale |
| — | — | — | Language buttons: हिंदी · मराठी · English |
| — | — | — | 🔍+ / 🔍− buttons in the header |
| — | — | — | 🎓 "Tutorial dobara dekho" replays onboarding |

---

## 🎓 First-run tutorial

On the very first open, Awaaz walks through four steps **read aloud**, with a **🔊 Suno** button on each step (browsers block unprompted speech, so the user always chooses when to hear it).

1. Namaste — what Awaaz is
2. Press and speak
3. Try a reminder
4. You are done — this is the only button you need

---

## 💡 Tips for best recognition

- Speak **after** the *"Sun rahi hoon…"* prompt, not before.
- Use everyday wording — the router is built for how people actually talk, not for commands.
- A quiet room helps; if it mishears, just **type** the same sentence.
- Switch language with the top buttons if a word keeps being misheard.
