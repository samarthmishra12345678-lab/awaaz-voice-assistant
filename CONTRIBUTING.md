# Contributing to Awaaz

Thank you for wanting to help. Awaaz is used by people for whom a bug is not an inconvenience — it is a missed dose. So the bar for changes is deliberately high.

## The one rule

> **Every change must make the app easier for someone who cannot read, cannot type, and cannot see small text.**

If a change makes the app more powerful but harder to use, it does not belong here.

## Ways to help

| What | How |
|---|---|
| 🐛 Report a bug | Open an issue with the device, browser, language, and exactly what was said |
| 🌐 Add a language | See below — this is the most valuable contribution |
| ♿ Improve accessibility | Report anything that requires reading, typing, or precise tapping |
| 📖 Improve documentation | Especially the guides in Hindi and Marathi |
| 👴 Run a pilot | Test with an actual elderly user and report honestly |

## Adding a language

Awaaz has three complete locales: `hi`, `mr`, `en`. Adding a fourth means adding **all** of them, never a partial translation.

1. Add the locale to the `T` object (UI strings) and the `R` object (response templates).
2. Add the 15 command examples.
3. Add the `SpeechRecognition` locale code (e.g. `ta-IN`).
4. **Run the in-app parity check.** The badge must read `n/n`. If it does not, the translation is not finished.

> A half-translated language is worse than no language. The parity check exists to make that impossible to ship by accident.

## Code guidelines

- **Keep it one file.** The single-file constraint is a feature — it means the app can be handed to a user on any phone with no build step.
- **No external requests at load time.** No CDN, no fonts, no analytics.
- **Nothing leaves the device.** No telemetry, ever.
- **Route through `handleCommand()`.** Every command must work by speech *and* by typing.
- **Escape user input.** Notes and names are user-controlled and rendered in the DOM.
- **Speak the answer.** A feature that only displays a result is not finished for this audience.

## Tests

The suite lives in `tests/`. Run it before opening a pull request:

```bash
npm install --save-dev jsdom
node tests/awaaz.test.js
```

All cases must pass. Add a case for every bug you fix — two shipped bugs were caught this way (see `docs/TESTING.md`).

## Reporting honestly

If you pilot Awaaz with a real user, please report **failures as well as successes**. Where did they get stuck? What did they try to say? The project's most valuable data so far has come from things that did not work.

## Licence

Contributions are accepted under the [MIT Licence](LICENSE).
