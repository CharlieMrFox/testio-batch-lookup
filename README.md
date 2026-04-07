# Test IO Batch Lookup

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Tampermonkey](https://img.shields.io/badge/Tampermonkey-userscript-brightgreen)](https://www.tampermonkey.net/)

A Discord userscript for the Test IO onboarding team. Enter any number of tester names and instantly verify which ones have a Test IO profile — results are colour-coded and linked, and your input is saved between sessions.

---

## Features

- 🔍 **Batch lookup** — enter any number of Discord display names (one per line) and check them all in parallel
- ✅ / ❌ **Instant results** — colour-coded badges show which names were found or not found
- 🔗 **Clickable names** — every result links directly to the tester's profile page
- 💾 **Persistent input** — the modal remembers what you typed, even after closing and reopening
- ⌨️ **Keyboard shortcut** — open/close with **Alt + T** from anywhere on Discord
- 🔘 **Floating button** — a small TIO button sits in the bottom-right corner of Discord as a permanent trigger

---

## Installation

### Option A — Install via loader (recommended)

This method loads the script live from this repository. Any update pushed here is reflected immediately — no reinstall needed.

1. Install the [Tampermonkey](https://www.tampermonkey.net/) browser extension
2. Click **[Install Loader Script](https://raw.githubusercontent.com/CharlieMrFox/testio-batch-lookup/refs/heads/main/Testio%20batch%20lookup.user)**
3. Tampermonkey will open an install prompt — click **Install**

### Option B — Install the script directly

1. Install [Tampermonkey](https://www.tampermonkey.net/)
2. Click **[Install Script](https://raw.githubusercontent.com/CharlieMrFox/testio-batch-lookup/refs/heads/main/Tio%20batch%20lookup.loader.user)**
3. Tampermonkey will open an install prompt — click **Install**

> ⚠️ With Option B, you'll need to reinstall manually each time the script is updated.

---

## Usage

1. Open Discord in your browser
2. Press **Alt + T** or click the **TIO** button in the bottom-right corner
3. Paste or type Discord display names — one per line
4. Click **Check Profiles**
5. Results appear sorted by status: found first, then missing
   - Click any name or the `→ view profile` link to open the profile directly

---

## Files

| File | Where it lives | Purpose |
|------|---------------|---------|
| `tio-batch-lookup.user.js` | GitHub | The full userscript — update this to release changes |
| `tio-batch-lookup.loader.user.js` | Tampermonkey | Installed in the browser; loads the script from GitHub via `@require` |
| `README.md` | GitHub | This file |
| `LICENSE` | GitHub | MIT licence |

---

## How it works

- Profile existence is checked via an HTTP `HEAD` request to `https://tester.test.io/profile_pages/<slug>`
- `GM_xmlhttpRequest` is used to bypass CORS restrictions
- Input is persisted between sessions using Tampermonkey's `GM_getValue` / `GM_setValue` storage (scoped to this script, visible in the Tampermonkey dashboard → Storage tab)
- The slug conversion mirrors Test IO's format: spaces and dots → `_`, non-alphanumeric characters stripped

---

## Updating

Push changes to `tio-batch-lookup.user.js`. Users on the **loader** script will pick up changes automatically on their next Discord page load.

To force an immediate cache refresh, append a version query string to the `@require` URL in the loader:

```
@require  https://raw.githubusercontent.com/YOUR_USERNAME/test-io-batch-lookup/main/tio-batch-lookup.user.js?v=1.3.0
```

---

## Licence

[MIT](LICENSE) © Charlie / Test IO Community Building Team
