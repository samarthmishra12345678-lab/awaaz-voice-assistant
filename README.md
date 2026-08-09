

# 🎙️ Awaaz

### *Sirf boliye — kaam ho jaayega.*  ·  *"Just speak — it's done."*

**A voice-first assistant for the people the smartphone forgot.**
Built for elderly & low-literacy users, in **Hindi · Marathi · English**.

</div>

---

## 💔 The Problem

My grandfather can't use a smartphone. Every day he asks — *"Beta, ye kaise karta hai?"*

Over **100 million elderly Indians** are locked out of the digital world because every app assumes you can read small text, tap tiny buttons, and type. Apps were never built for *them*.

So I built **Awaaz** — where **speaking is the only skill you need.** You press one big button, talk naturally, and it does the task, then speaks the answer back (because many users can't read).

---

## ✨ Features

🎙️ **Voice-first** — one giant mic button, speak in Hindi / Marathi / English
🔊 **Speaks back** — every answer is read aloud for users who can't read
⏰ **Smart reminders** — *"subah 8 baje dawai yaad dilao"* → alarm rings on time
🔁 **Daily recurring** — *"roz subah 8 baje..."* → rings every single day
🔔 **System notifications** — reminders ring with a system notification, sound & vibration **while the app is open or minimized** *(true background push, even when fully closed, is on the roadmap — see What's Next)*
⌨️ **Type-to-command fallback** — can't speak or mic mishears? Type the same command and it still works
📍 **SOS + Location** — emergency button sends your live location to family on WhatsApp
🌤️ **Live weather** · 🧮 **calculator** · 📅 **date/day** · 💚 **health tips** — all by voice
🛡️ **Scam check** — warns about OTP/lottery fraud (protects elderly)
🎓 **Voice onboarding** — a friendly 4-step tutorial, read aloud, for first-time users
♿ **Accessibility-first** — huge buttons, adjustable font, high-contrast dark mode, ARIA screen-reader support
📱 **Installable PWA** — works offline for core features, no app store needed

---

## 🚀 Live Demo

**🔗 [Open Awaaz](https://melodious-semifreddo-6c3f6c.netlify.app)** *(open in Chrome on your phone, allow microphone)*

> 💡 Voice needs a real browser + microphone permission (HTTPS). Try saying:
> *"Subah 8 baje dawai yaad dilao"* · *"Nagpur ka mausam batao"* · *"25 aur 30 jodo"*

---

## 🗣️ Everything you can say

| Just say... | What happens |
|---|---|
| *"Subah 8 baje dawai yaad dilao"* | Sets a medicine reminder |
| *"Roz subah 8 baje dawai yaad dilao"* | Daily recurring reminder 🔁 |
| *"Mere notes sunao"* | Reads all your notes aloud |
| *"Nagpur ka mausam batao"* | Live weather |
| *"Meri location bhejo"* | Sends location to family on WhatsApp 📍 |
| *"98765 43210 pe call lagao"* | Starts a call |
| *"25 aur 30 jodo"* | Voice calculator |

---

## 🛠️ How it's built

- **Single self-contained HTML file** — no server, no login, no dependencies. Runs on a cheap phone, installs like an app, works offline.
- **Web Speech API** — SpeechRecognition (listening) + SpeechSynthesis (speaking back) in 3 languages.
- **Notifications API + Service Worker** — reminders ring with a system notification (sound + vibration) while the app is open or minimized/in another tab, and any reminders missed while away fire the moment you reopen Awaaz. Tapping the notification re-opens the app. *(True background push when the app is fully closed needs a push server / native wrapper — see What's Next.)*
- **Open-Meteo API** (free, no key) for live weather.
- **Geolocation + WhatsApp deep-link** for the SOS location share.
- **localStorage** for notes, reminders, settings — all on-device, private.
- **WebAudio** generates the alarm beep, so no external sound files are needed.

---

## 🧪 Tested — 80/80 passing

A jsdom automated test suite of **80 test cases** covers command routing, the calculator (including tricky voice orders like *"100 me se 40 ghatao"*), reminder scheduling, notification firing, XSS-safety, onboarding, and all 3 languages. **All 80 pass.** The tests caught two real bugs I would have shipped otherwise.

---

## 🚀 What's Next

- **True background push** — reminders that fire even when the app is fully closed / after a phone reboot (via a lightweight push server or a native wrapper like Capacitor)
- More languages (Tamil, Telugu, Bengali)
- Caregiver mode — family adds reminders remotely
- Pilot with a local senior citizens' group

---

Built with - [SAMARTH MISHRA]
