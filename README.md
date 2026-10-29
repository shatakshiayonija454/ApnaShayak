# Apna Sahayak — A caring voice, in your language

A senior-friendly responsive website using HTML, CSS and JavaScript, with the supplied logo, language selector, browser voice input/output, local reminders, one-tap family calls, local data persistence, optional browser notifications, and a progressive-web-app offline shell.

## Run locally
For the best voice and service-worker support, serve the folder from localhost rather than opening the HTML directly. With Python installed, run `python -m http.server 8080` in this folder and open `http://localhost:8080`.

## Publish the front end on GitHub Pages
1. Create a GitHub repository and upload the contents of this folder (including `assets/`, `manifest.webmanifest`, and `service-worker.js`).
2. Open **Settings → Pages** and deploy from the `main` branch, root (`/`).
3. The static site works in demo mode. It can use browser speech APIs when the device/browser supports them.

## Language and voice support
English is the default. The selector includes Indian languages (Hindi, Punjabi, Bengali, Tamil, Telugu, Marathi, Gujarati, Kannada, Malayalam, Odia, Assamese, Urdu, Konkani, Maithili, Sanskrit, Nepali, Sindhi, Kashmiri, Dogri, Meitei/Manipuri, Santali and Bodo). The current UI and demo assistant have fuller translations for English, Hindi and Punjabi; other languages are listed but some interface text may remain English. A language being listed does not guarantee that the browser has speech recognition or a text-to-speech voice for it. Test with your target devices and native speakers before launch.

## Reminders: important limitation
Reminders and contacts are stored in the current browser using localStorage. Reminder checks happen while the website is open; notifications require permission and browser support. A static GitHub Pages website cannot guarantee alarms when the browser is closed, the phone is asleep, or the OS suspends the tab. Do not use this prototype for critical medication timing. Production-grade reminders need a native app/push-notification design and testing.

## Optional AI backend (keeps the API key off GitHub)
GitHub Pages is static and cannot run the Node API. To enable AI replies, deploy `server/` to a Node host such as Render/Railway/Fly.io and set environment variables in that host's dashboard:
- `OPENAI_API_KEY`: your private provider key (never commit it to GitHub)
- `OPENAI_MODEL`: a model available to your API account
- `ALLOWED_ORIGIN`: your GitHub Pages origin, e.g. `https://username.github.io`

Steps:
1. Deploy the `server` directory as a Node service. Build/install command: `npm install`; start command: `npm start`.
2. Set the environment variables on the hosting provider. Do not upload `.env` or expose keys in browser JavaScript.
3. In the front-end `script.js`, set `API_BASE` to the deployed API base URL (for example `https://your-service.example.com`) and change `state.mode` default from `demo` to `ai` if you want AI mode by default. Alternatively, add a settings toggle before launch.
4. Test CORS and errors. Add authentication, rate limits, abuse protection, monitoring and privacy notices before public use; this sample server is a starter, not a hardened production service.

## Safety and privacy
- The site is not an emergency service and does not replace a clinician.
- Never ask the AI to diagnose or change medicine doses; do not rely on this prototype for medical decisions.
- Local contacts/reminders stay in the browser profile unless the user clears browser data. Anyone with access to that device/profile may be able to view them.
- Voice recognition and speech synthesis are browser-dependent and may process speech through the browser/device provider.
- Review translations, accessibility, security, consent, data retention and local privacy-law requirements before real deployment.

## Files
- `index.html`: page structure and language selector
- `styles.css`: responsive styling
- `script.js`: voice, translations, reminders, contacts, persistence and demo/AI call logic
- `assets/apna-sahayak-logo.jpg`: logo image
- `manifest.webmanifest`, `service-worker.js`: installable/offline shell
- `server/`: optional Node API example for AI responses
