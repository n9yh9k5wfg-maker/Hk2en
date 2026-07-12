# Hk2en — Cantonese → English Live Translator

Speak Cantonese, read English. A single-page web app that listens to long
Cantonese speech and turns it into large, readable English text on screen,
phrase by phrase, as you talk. Works on iPhone/iPad, Android, and desktop.

## Using it on iPhone / iPad (simplest path)

iOS Safari's in-page speech recognition is unreliable, so on iOS the app
uses the **native keyboard dictation** instead — Apple's Cantonese
dictation is excellent, on-device, and handles long speech.

**One-time setup (about 30 seconds):**

1. Settings → General → Keyboard → **Keyboards** → Add New Keyboard →
   **Cantonese, Traditional (廣東話)**
2. Same Keyboard screen: make sure **Enable Dictation** is on.

**Every time:**

1. Open the app in Safari (see *Hosting* below for the URL).
2. Tap the text box at the bottom.
3. Hold the 🌐 key to switch to the 廣東話 keyboard, then tap the
   keyboard's **🎙️** button and just talk.
4. English appears above in large text as you pause — keep talking as long
   as you like. The app shows these instructions on screen too.

## Using it on desktop / Android

Open it in **Chrome** or **Edge**, click **Start listening**, allow the
microphone, and speak. Recognition runs continuously and auto-restarts, so
long speech keeps flowing. The ⌨️/🎤 button in the header switches between
in-page mic and keyboard-dictation modes on any platform.

## Controls

- **A− / A+** — shrink or enlarge the English text
- **粵** — show/hide the original Cantonese under each line
- **Clear** — wipe the screen
- **⌨️ / 🎤** — switch input mode

## Hosting

It's one HTML file with no build step, but phones need an **https://** URL.
The easiest free option is GitHub Pages:

1. In this repo: Settings → Pages → *Deploy from a branch* → pick this
   branch, folder `/ (root)` → Save.
2. After a minute the app is live at
   `https://<your-username>.github.io/Hk2en/` — open that on the iPhone
   and add it to the Home Screen (Share → Add to Home Screen) for
   one-tap access.

For local desktop testing: `python3 -m http.server 8000` then open
`http://localhost:8000` in Chrome.

## How it works

1. **Dictation** — on iOS, the native keyboard mic streams Cantonese text
   into a box and the app translates each new chunk after a ~1 s pause.
   Elsewhere, the Web Speech API transcribes Cantonese
   (`yue-Hant-HK`, or `zh-HK` on Apple browsers) continuously.
2. **Translation** — each Cantonese chunk is sent to Google Translate's
   public web endpoint (Cantonese → English, no API key needed) and shown
   as big English text with the original Cantonese underneath. Requests
   are queued so lines always appear in speaking order.

## Notes

- Internet connection required for translation (and for in-page speech
  recognition on Chrome). iOS keyboard dictation itself works on-device.
- Translation tries Cantonese (`yue`) first and falls back to Traditional
  Chinese if the Cantonese route is unavailable.
