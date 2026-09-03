## 💔 Inspiration — The Problem

It was 8 in the morning and my grandfather was standing in the doorway with his phone in his hand, holding it out to me the way you hand someone something broken.

"Beta, ye kaise karta hai?"

He needed a medicine reminder. Fifteen seconds of work for me. For him, an afternoon of waiting until someone came home.

He is not sick. He is not unwilling. He is not slow. He is simply locked out — by design. Over 100 million elderly Indians are on the wrong side of the same door, because every app ever built assumes three things: that you can read small text, that you can tap a tiny button, and that you can type.

**And every existing answer asks something of him in return.** A reminder app has to be installed and configured. A helpline has to be found and dialled. A health wearable has to be worn, charged and remembered. An SOS button has to be reached — which is useless in precisely the situation it exists for. A voice assistant will help, if you speak English, and if you can see the screen well enough to find it. Marathi is an afterthought, where it exists at all.

The cruel part is how ordinary the failure looks from outside. Nothing is wrong. He just quietly stops trying, and the people who love him assume he is managing.

So I built Awaaz around one mandate: **speaking should be enough.** Not "speaking helps." Not "speaking, once you've set it up." Press one big button, say it the way you'd say it to a person, and it's done — then it says the answer back out loud, because plenty of the people who need this most can't read it either.

The name means "voice" in Hindi. Marathi was non-negotiable from day one, because it is the language my family actually thinks in, and because the apps that bother with India usually stop at Hindi.

One more thing I learned while building it: **a reminder that rings and is ignored is not help.** An unconfirmed dose is the one that matters. That is why Awaaz doesn't just remind — it notices when nobody answered, and it tells someone who can.

## 🎯 What It Does

Awaaz is a voice-first assistant designed from the ground up for elderly and low-literacy users. You press one big button, speak naturally in Hindi, Marathi, or English, and it does the task — then speaks the answer back out loud (because many users can't read).

Everything it can do — by voice:

- "Subah 8 baje dawai yaad dilao" → medicine reminder that rings on time
- "Roz subah 8 baje dawai yaad dilao" → daily recurring reminder 🔁
- "Mere notes sunao" → reads all saved notes aloud
- "Nagpur ka mausam batao" → live weather from a real API
- "98765 43210 pe call lagao" → starts a phone call
- "Meri location bhejo" → sends live location to family on WhatsApp 📍
- "25 aur 30 jodo" → voice calculator
- "Aaj kaunsa din hai" → date & day
- "Sehat ki salah do" → a friendly health tip
- "Ye SMS scam hai?" → scam / fraud safety check
- 🆘 SOS button → emergency help + calls saved contact + shares location

### 🆕 Missed-dose escalation (the feature I'm proudest of)

If a medicine reminder fires and nobody taps "Theek hai", Awaaz waits, then escalates: a loud banner appears with one-tap buttons to call or WhatsApp the caregiver — "Dawai confirm nahi hui." Most health apps only remind. Awaaz notices when the reminder was *ignored*, because an unconfirmed dose is the one that actually matters.

### 👨‍👩‍👧 "Mere Apne" — caregiver contacts

Save family numbers by voice ("caregiver number 98765..."). Every SOS and every missed-dose alert reaches a real person, not a notification nobody reads.

### 📴 It works with no internet

Notes, reminders, calculator, SOS contacts, and the full voice loop all run offline. A live chip in the header tells the user the current state. Most assistive apps stop working the moment the network drops — that's exactly when an elderly user is most likely to be alone with a problem.

Plus, it just works for real life:

- 🔔 Reminders ring with a system notification, sound & vibration while the app is open or minimized — and any reminder missed while you were away fires the instant you reopen Awaaz.
- ⌨️ Type-to-command fallback — if a user can't speak, or the mic mishears, they can type the exact same command and every feature still works.
- 🎓 First-run voice tutorial — holds a new user's hand in 4 friendly steps, read aloud.
- 📱 Installable (PWA) — works offline for core features.
- ♿ Screen-reader (ARIA) support with labels in all 3 languages, a skip-to-mic link, a live region for every reply, huge buttons, adjustable font, high-contrast dark mode.

## 🌐 Three languages — all three complete

Hindi, Marathi and English, and none of them is a second-class citizen. This is verified, not claimed: the app reports at runtime that all three locales carry the same **52 strings and the same 15 voice commands** (11 UI keys + 41 response keys × 3). Adding a partial language is easy; keeping three in lockstep is the part teams skip.

## 🛠️ How I Built It

- 100% front-end, single self-contained HTML file — no server, no login, no dependencies. It runs on a cheap phone, installs like an app, and works offline.
- Web Speech API — SpeechRecognition for listening + SpeechSynthesis for speaking back, in 3 languages (hi-IN / mr-IN / en-IN).
- Notifications API + Service Worker — reminders reach the user while the app is open or minimized, and missed ones fire on reopen.
- Escalation engine — a confirmation window per reminder; if it lapses, the caregiver is surfaced with one-tap call / WhatsApp deep-links.
- Open-Meteo API (free, no key) for live weather.
- Geolocation + WhatsApp deep-link for the SOS location share.
- localStorage for notes, reminders, caregiver contacts and settings — all on-device, private. No account, no server, no face recognition, no data leaving the phone.
- WebAudio generates the alarm beep, so no external sound files are needed.

Every feature is automatically tested. I wrote a jsdom test suite of 80 test cases covering command routing, the calculator, reminder scheduling, notifications, XSS-safety, and all 3 languages. All 80 pass. I didn't want to hope it works on demo day — I wanted to know.

## 🧗 Challenges I Ran Into

- Reminders that only fired inside the tab — I added the Notifications API + a service worker so alarms reach the user while the app is open or minimized, plus a "catch-up" check that fires any missed reminder the moment the app reopens.
- Voice command collisions — "notes sunao" was being saved as a new note; "jodo" (add) confused the calculator. I had to carefully order the command handlers and build a postfix-aware calculator (Hindi/Marathi often say the operator after the numbers).
- Browsers block auto-play audio until the user taps — so onboarding can't just start talking. I added a big 🔊 Suno button.
- Autonomy vs. safety — an SOS that could dial a wrong number is dangerous, so location-share opens WhatsApp for a final human confirm. The same caution shaped the escalation window: it waits long enough to be useful and short enough to matter.
- Keeping three languages in lockstep — the fix was a runtime parity check that counts keys and commands per locale, so an unfinished translation is visible immediately instead of shipping silently.

## 🏆 Accomplishments I'm Proud Of

- It genuinely works for the person I built it for.
- 80/80 automated tests passing — real engineering rigor, not a demo that works once.
- Full 3-language support including Marathi, which most apps ignore — and all three are complete.
- A missed-dose escalation loop that closes the gap most reminder apps leave open.
- Offline install, no account, no server, no cost — it feels like a real product, not a hackathon toy.

## 📚 What I Learned

- Accessibility isn't a feature you add at the end — it's the whole design.
- "It reminded them" is not the same as "it helped them." Building the escalation taught me to design for the moment the reminder fails.
- Testing early saves you on demo day. My suite caught two real bugs I would have shipped.
- The hardest part of voice UX isn't the tech — it's understanding how a real person actually talks.
- Being honest about what works now vs. what's coming next builds more trust than over-claiming.

## 🚀 What's Next for Awaaz

- True background push — reminders that fire even when the app is fully closed / survive a reboot (push server or a native wrapper like Capacitor).
- More Indian languages (Tamil, Telugu, Bengali) — the parity check makes each addition safe.
- Caregiver mode — a family member can add reminders remotely.
- A real-world pilot with a local senior citizens' group, and publishing the results honestly.

Built with -[SAMARTH MISHRA]
