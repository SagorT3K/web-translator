# Web Translator

A free, client-side web translator that runs entirely in your browser — no server, no installation, no API key required.

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

A single HTML file with no dependencies. Translation is done in the browser
via Google's public `translate.googleapis.com` endpoint, and speech uses the
browser's built-in Web Speech API.

## Development

```bash
git clone https://github.com/SagorT3K/web-translator.git
# open index.html in any browser
```
