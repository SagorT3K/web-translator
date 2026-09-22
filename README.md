# Web Translator

A free, client-side web translator that runs entirely in your browser — no server, no installation, no API key required.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![Vanilla JS](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Languages](https://img.shields.io/badge/languages-109-blue?style=flat-square)](#features)
[![No build step](https://img.shields.io/badge/build-none-success?style=flat-square)](.)

**Single file, zero dependencies.** The whole app is [`index.html`](index.html) — open it and it works, on your machine or from any static host.

## Quick start

```bash
git clone https://github.com/SagorT3K/web-translator.git
cd web-translator
# then either double-click index.html, or serve it:
python -m http.server 8080     # http://localhost:8080
```

Because there is no backend, the same file can be dropped on GitHub Pages, Netlify, Cloudflare Pages or any static host.

## Features

- Translate between **109 languages** with automatic source-language detection
- Long-text support (input is automatically chunked, up to 5000 characters)
- Swap source/target languages with one click
- Copy translation to clipboard
- 🔊 Listen to the translation (text-to-speech)
- Keyboard shortcut: `Ctrl+Enter` (or `Cmd+Enter` on Mac) to translate
- Responsive design — works on desktop and mobile

## How to use

1. **Open the app**: double-click `index.html` to open it in your browser
   (Chrome, Edge, Firefox, or Safari).
2. **Enter your text** in the left box (up to 5000 characters).
3. **Pick languages** using the dropdowns — set the source to *Auto-detect*
   or choose a language manually, then choose the target language.
4. **Click Translate** (or press `Ctrl+Enter`).
5. The translation appears on the right. Use **Copy** to copy it, or
   **🔊 Speak** to hear it aloud.
6. Use **⇅ Swap** to switch the languages and keep translating.

### Tips

- Speech uses your operating system's installed voices. If a language
  doesn't speak, install its voice pack (Windows: Settings → Time &
  Language → Speech; macOS: System Settings → Accessibility → Spoken Content).
- The translation service is free with no sign-up. Very heavy automated
  usage may be rate-limited.

## How it works

A single HTML file with no dependencies, no bundler and no build output:

```
index.html
├── <style>   inline CSS (responsive layout, dark-ish gradient theme)
└── <script>  LANGUAGES[]  – 109 [code, name] pairs
              chunkText()  – splits input on sentence/line boundaries (1500 chars per request)
              translate()  – one request per chunk, results joined
              speak()      – Web Speech API (speechSynthesis)
```

- **Translation** — `GET https://translate.googleapis.com/translate_a/single?client=gtx&sl=…&tl=…&dt=t&q=…`, the same public endpoint the Google Translate web widget uses. Requests are sent straight from the browser, so there is no server in the middle and nothing to deploy.
- **Chunking** — the service takes text through the URL, so long input would break it. Input is split on sentence/line boundaries into ~1500-character chunks, each translated separately, then concatenated in order.
- **Text-to-speech** — `speechSynthesis` with the browser's installed voices, so quality and availability depend on your OS voice packs.
- **Detection label** — when the source is *Auto-detect*, the code the service returns is mapped back to a language name and shown under the box.

## Project structure

```
web-translator/
└── index.html      the entire application (markup + styles + logic)
```

## Limitations

- The Google endpoint used here is **public but unofficial** — no key, no quota, no SLA. Very heavy or automated traffic can be rate-limited or temporarily blocked.
- 5,000 characters per translation is the app's own cap; longer text must be translated in parts (chunking happens inside that limit).
- Translation happens client-side, so anything you paste is sent to `translate.googleapis.com` from your browser. Don't paste secrets.
- No document/PDF translation and no in-place page translation — this is a two-box text translator.

## Browser support

Latest Chrome, Edge, Firefox and Safari. Speech output additionally needs the Web Speech API (`speechSynthesis`), which all four provide; missing voice packs simply mean a language can't be spoken.

## Development

```bash
git clone https://github.com/SagorT3K/web-translator.git
# edit index.html, then reload the page — no install, no build, no tests
```

The language list lives in the `LANGUAGES` array at the top of the `<script>` block: add a `["code", "Display Name"]` entry and it appears in both dropdowns automatically.
