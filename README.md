# WTR-Lab Old UI Restore

A Chrome/Edge browser extension that restores the classic WTR-Lab interface on the live site after the May 2026 redesign.

---

## What it does

WTR-Lab updated their UI in May 2026. This extension injects the original CSS from a saved snapshot of the old site, making it look and feel exactly as it did before the redesign — including dark mode, light mode, the reader, novel cards, library, rankings, and all other pages.

---

## Features

- **Pixel-faithful restoration** — uses the actual CSS files saved from the old site, not a recreation
- **Dark & light mode** — detects your saved site preference or OS setting automatically
- **Works everywhere** — homepage, novel list, reader, library, profile, leaderboard, community, all pages
- **Toggle on/off** — popup switch instantly enables or disables the old UI without a page reload
- **SPA-aware** — handles Next.js client-side navigation correctly
- **No flash** — legacy styles apply before first paint
- **Lightweight** — no background polling, minimal observers, no external requests

---

## Install

### Chrome

1. [Download the ZIP](../../archive/refs/heads/main.zip) and extract it, or clone the repo:
   ```
   git clone https://github.com/YOUR_USERNAME/wtr-lab-old-ui.git
   ```
2. Open Chrome and go to `chrome://extensions`
3. Turn on **Developer mode** using the toggle in the top-right corner
4. Click **Load unpacked**
5. In the file picker, navigate into the extracted folder and select the **`wtr-lab-old-ui`** subfolder (the one that contains `manifest.json`)
6. The extension appears in your toolbar. Visit [wtr-lab.com](https://wtr-lab.com) — done.

> **Important:** Select the inner `wtr-lab-old-ui` folder, not the outer repo folder. Chrome needs to see `manifest.json` at the root of whatever folder you select.

---

### Microsoft Edge

1. Download and extract the ZIP (same as above)
2. Go to `edge://extensions`
3. Turn on **Developer mode** (left sidebar toggle)
4. Click **Load unpacked**
5. Select the `wtr-lab-old-ui` folder
6. Visit [wtr-lab.com](https://wtr-lab.com)

---

### Brave

Same steps as Chrome. Go to `brave://extensions` instead of `chrome://extensions`.

---

### Pinning to the toolbar (Chrome/Edge)

After installing, the extension icon may be hidden in the puzzle-piece menu:

1. Click the **puzzle piece** icon (🧩) in the top-right of your browser
2. Find **WTR-Lab Old UI** in the list
3. Click the **pin** icon next to it
4. The W icon now appears in your toolbar for quick access

---

### Firefox

Firefox requires extensions to be signed through Mozilla. For now, use Chrome, Edge, or Brave.

---

## Usage

Click the extension icon in your toolbar to open the popup.

- **Toggle ON** — old UI is active (default)
- **Toggle OFF** — new UI is shown, all injected styles removed

The toggle takes effect instantly on all open WTR-Lab tabs.

---

## How it works

The extension loads three CSS files saved directly from the old WTR-Lab site:

| File | Contents |
|---|---|
| `bs.css` | Bootstrap base styles |
| `wtr.css` | WTR-Lab custom styles (all components, dark/light vars) |
| `widgets.css` | Rating stars, tooltips, activity calendar |

These are injected into every `wtr-lab.com` page. Theme detection mirrors the original site's own logic — it reads your saved preference from `localStorage`, falling back to your OS dark/light setting.

---

## Files

```
wtr-lab-old-ui/
├── manifest.json      Chrome extension manifest (MV3)
├── background.js      Service worker — CSS injection lifecycle
├── content.js         Theme detection and hydration guard
├── popup.html         Extension popup UI
├── popup.js           Popup toggle logic
├── bs.css             Bootstrap CSS (from old site)
├── wtr.css            WTR-Lab custom CSS (from old site)
├── widgets.css        Widget CSS (from old site)
└── icons/
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

---

## Known limitations

- If WTR-Lab renames their HTML class names in a future update, some components may not style correctly. The CSS targets the old class names.
- Inline styles set by React after page load can override injected CSS in rare cases.
- The reader theme selector (Light/Dark buttons inside the reader settings) controls the site's own theme — the extension respects whichever option you pick there.

---

## Contributing

If WTR-Lab updates their site and breaks something, open an issue or PR. The fix is usually updating a selector in `wtr.css`.

---

## License

The CSS files (`bs.css`, `wtr.css`, `widgets.css`) are derived from WTR-Lab's own frontend assets and belong to their respective owners. The extension code (`background.js`, `content.js`, `popup.*`, `manifest.json`) is released under the MIT License.

This extension is an unofficial fan tool. It is not affiliated with or endorsed by WTR-Lab.
