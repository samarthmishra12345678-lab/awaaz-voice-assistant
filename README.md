🎙️ Awaaz
Sirf boliye — kaam ho jaayega. · "Just speak — it's done."
A voice-first assistant for the people the smartphone forgot.
Built for elderly & low-literacy users, in Hindi · Marathi · English.
Try live-dancing-haupiae78999.netlify.app
💔 The Problem
My grandfather can't use a smartphone. Every day he asks — "Beta, ye kaise karta hai?"

Over 100 million elderly Indians are locked out of the digital world because every app assumes you can read small text, tap tiny buttons, and type. Apps were never built for them.

So I built Awaaz — where speaking is the only skill you need. You press one big button, speak naturally, and it does the task, then speaks the answer back (because many users can't read).
✨ Features
🎙️ Voice-first — one giant mic button, speak in Hindi / Marathi / English
🔊 Speaks back — every answer is read aloud for users who can't read
⏰ Smart reminders — "subah 8 baje dawai yaad dilao" → alarm rings on time
🔁 Daily recurring — "roz subah 8 baje..." → rings every single day
🔔 Background notifications — reminders fire even when the app is closed
📍 SOS + Location — emergency button sends your live location to family on WhatsApp
🌤️ Live weather · 🧮 calculator · 📅 date/day · 💚 health tips — all by voice
🛡️ Scam check — warns about OTP/lottery fraud (protects elderly)
🎓 Voice onboarding — a friendly 4-step tutorial, read aloud, for first-time users
♿ Accessibility-first — huge buttons, adjustable font, high-contrast dark mode, ARIA screen-reader support
📱 Installable PWA — works offline for core features, no app store needed
🗣️ Everything you can say
Just say...	What happens
"Subah 8 baje dawai yaad dilao"	Sets a medicine reminder
"Roz subah 8 baje dawai yaad dilao"	Daily recurring reminder 🔁
"Mere notes sunao"	Reads all your notes aloud
"Nagpur ka mausam batao"	Live weather
"Meri location bhejo"	Sends location to family on WhatsApp 📍
"98765 43210 pe call lagao"	Starts a call
"25 aur 30 jodo"	Voice calculator
"Aaj kaunsa din hai"	Date & day
"Sehat ki salah do"	Health tip
"Pehla note hatao" / "sab hatao"	Delete notes by voice"Dark mode karo" / "text bada karo"	Accessibility by voice
🆘 SOS button	Emergency help + location
🛠️ How It's Built
Single self-contained HTML file — no server, no login, no build step. Runs on a cheap phone, installs like an app, works offline. Deliberate: nothing between the user and the help they need.
Web Speech API — SpeechRecognition (listen) + SpeechSynthesis (speak) in 3 languages.
Notifications API + Service Worker — reminders fire in the background, even when the app is closed.
Open-Meteo API — free live weather, no API key.Geolocation + WhatsApp deep-link — for SOS location share.
localStorage — notes, reminders, settings, all on-device & private.
WebAudio — generates the alarm beep, no sound files needed.
🚀 What's Next
Reminders that survive a phone reboot
More languages (Tamil, Telugu, Bengali)
Caregiver mode — family adds reminders remotely
Pilot with a local senior citizens' group

build with - [Samarth Mishra ]
