# chrome-extension-starter

A boilerplate for building Chrome extensions with React, TypeScript, and Tailwind CSS. Includes popup, options page, background service worker, and content script setup.

## Features

- **React 18** + **TypeScript** — component-based UI
- **Tailwind CSS** — utility-first styling
- **Vite** — fast builds with HMR in dev
- **Manifest V3** — latest Chrome extension standard
- Pre-configured: popup, options page, background worker, content script
- Chrome storage API helpers
- Message passing between popup ↔ background ↔ content script

## Getting Started

```bash
git clone https://github.com/madhuveeraprasath-a/chrome-extension-starter.git
cd chrome-extension-starter
npm install
npm run dev
```

**Load in Chrome:**
1. Go to `chrome://extensions`
2. Enable **Developer mode**
3. Click **Load unpacked**
4. Select the `dist/` folder

## Project Structure

```
chrome-extension-starter/
├── src/
│   ├── popup/
│   │   ├── Popup.tsx         # Extension popup UI
│   │   └── index.html
│   ├── options/
│   │   ├── Options.tsx       # Settings page
│   │   └── index.html
│   ├── background/
│   │   └── service-worker.ts # Background tasks
│   ├── content/
│   │   └── content.ts        # Injected into web pages
│   └── lib/
│       ├── storage.ts        # Chrome storage helpers
│       └── messaging.ts      # Message passing helpers
├── manifest.json
└── vite.config.ts
```

## Message Passing

```ts
// From popup → background
sendMessage({ type: 'GET_DATA', payload: { url: tab.url } });

// In background service worker
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  if (message.type === 'GET_DATA') {
    // handle and respond
  }
});
```

## Chrome Storage Helper

```ts
import { storage } from './lib/storage';

// Save
await storage.set('settings', { theme: 'dark' });

// Read
const settings = await storage.get('settings');
```

## Build for Production

```bash
npm run build
```

Outputs to `dist/` — zip and upload to the Chrome Web Store.

## License

MIT
