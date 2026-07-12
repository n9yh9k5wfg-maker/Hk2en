# Hk2en — Cantonese → English Live Translator

Speak Cantonese, read English. A single-page web app that listens to long
Cantonese speech and turns it into large, readable English text on screen,
phrase by phrase, as you talk.

## How it works

1. **Dictation** — the browser's built-in Web Speech API transcribes your
   voice as Cantonese (`yue-Hant-HK`), running continuously so long speech
   keeps flowing (it auto-restarts whenever the browser pauses recognition).
2. **Translation** — each finalized Cantonese phrase is sent to Google
   Translate's public web endpoint (Cantonese → English, no API key needed)
   and displayed as big English text, with the original Cantonese shown
   smaller underneath.

## Usage

No build step — it's one HTML file. Serve it locally and open it in
**Chrome** or **Edge** (the Web Speech API needs `https://` or `localhost`):

```bash
python3 -m http.server 8000
# then open http://localhost:8000 in Chrome
```

1. Click **Start listening** and allow microphone access.
2. Speak Cantonese — pauses are fine, it keeps listening until you stop it.
3. Read the English on screen. Controls in the header:
   - **A− / A+** — shrink or enlarge the English text
   - **粵** — show/hide the original Cantonese under each line
   - **Clear** — wipe the screen
   - **Stop** — pause listening

## Requirements & notes

- Chrome or Edge (desktop or Android). Firefox and iOS Safari don't support
  Web Speech API dictation.
- Internet connection (both speech recognition and translation are online
  services).
- Translation tries Cantonese (`yue`) first and falls back to Traditional
  Chinese if the Cantonese route is unavailable.
