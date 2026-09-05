# Changelog

All notable changes to Awaaz are recorded here.
This project follows [Keep a Changelog](https://keepachangelog.com/) conventions.

## [Unreleased]

### Planned
- True background push so reminders survive a reboot
- Caregiver mode — add reminders remotely for a family member
- More Indian languages: Tamil, Telugu, Bengali
- Published pilot report with real seniors
- Optional on-device wake word

---

## [1.2.0] — Documentation & Knowledge Base

### Added
- `docs/GETTING-STARTED.md` — first-run guide in Hindi, Marathi and English
- `docs/TROUBLESHOOTING.md` — failure modes written for elderly users
- `docs/FAQ.md` — frequently asked questions, in all three languages
- `docs/FOR-FAMILIES.md` — 10-minute setup checklist for caregivers
- `CHANGELOG.md`, `CONTRIBUTING.md`, `LICENSE`
- Runtime language-parity check surfaced in the UI (52 strings, 15 commands × 3)

### Changed
- README restructured as a documentation hub with a table of contents
- Every documentation link verified to resolve (no broken links)

---

## [1.1.0] — Safety & Reach

### Added
- **Missed-dose escalation** — an unconfirmed reminder offers to call or WhatsApp a caregiver
- **"Mere Apne"** caregiver contacts, savable by voice
- Offline state indicator in the header
- Inline PWA manifest and inline SVG favicon (zero external requests at load)
- Type-to-command fallback for users who cannot speak

### Fixed
- "notes sunao" was creating a new note instead of reading notes (handler ordering)
- Daily reminders drifted into the past after several days away

---

## [1.0.0] — First release

### Added
- Voice-first assistant in Hindi, Marathi and English
- Medicine reminders (one-time and daily)
- Notes, weather, calculator, date, health tips, scam check
- Emergency SOS with call and WhatsApp location sharing
- Notifications, vibration and WebAudio alarm with spoken alerts
- Dark mode and font scaling, controllable by voice
- Four-step first-run voice tutorial
