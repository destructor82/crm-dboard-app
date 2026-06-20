# CRM Recovery Unit — Dashboard

An installable, offline-capable web app (PWA). This folder is everything you need to host it on GitHub Pages.

## Files

```
index.html              the app
manifest.webmanifest    PWA config (name, icons, colors)
service-worker.js       enables offline use + the install prompt
favicon.ico             browser tab icon
icons/                  all app icon sizes (incl. maskable Android icons)
```

## 1. Put it on GitHub

1. Create a new repository on GitHub (e.g. `crm-recovery-unit`). Public repos get free Pages hosting; private repos need GitHub Pro/Team/Enterprise for Pages.
2. Upload **all the files in this folder** to the repo root, keeping the `icons/` folder intact. Easiest way:
   - On the repo page, click **Add file → Upload files**, drag in everything, commit.
   - Or via git:
     ```
     git clone https://github.com/<you>/crm-recovery-unit.git
     cd crm-recovery-unit
     # copy these files in here
     git add .
     git commit -m "Add dashboard PWA"
     git push
     ```

## 2. Turn on GitHub Pages

1. In the repo: **Settings → Pages**.
2. Under "Build and deployment", set **Source** to **Deploy from a branch**.
3. Branch: `main` (or whichever you pushed to), folder: `/ (root)`. Save.
4. Wait a minute, then your app is live at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```

PWAs require HTTPS to install — GitHub Pages serves everything over HTTPS automatically, so no extra setup needed there.

## 3. Installing it on a device

Once it's live on GitHub Pages (installability needs a real HTTPS URL — it won't trigger the native prompt when opened straight from a local file):

- **Android (Chrome):** open the link → tap the **⤓ INSTALL APP** button in the header, or use Chrome's menu → "Install app".
- **iPhone/iPad (Safari):** open the link → tap **⤓ INSTALL APP** (or Safari's Share icon) → **Add to Home Screen**. iOS doesn't support automatic install prompts, so this is a manual step every time.
- **Desktop (Chrome/Edge):** open the link → click the install icon in the address bar, or the **⤓ INSTALL APP** button.

Once installed it opens in its own window/icon, no browser chrome, and keeps working offline thanks to the service worker.

## Updating the app later

Edit `index.html` (or anything else) and push the change. Then open `service-worker.js` and bump:
```js
const CACHE_VERSION = 'v1';   // change to 'v2', 'v3', etc.
```
This forces installed copies to fetch the new version instead of serving a stale cached one. Without this bump, people who already installed the app may not see your changes right away.

## Notes

- All data the dashboard collects is stored in the browser (see the app's own save/export behaviour) — GitHub Pages only hosts the static files, it doesn't store or see your data.
- The app icon (`icons/`, `favicon.ico`) was generated to match the dashboard's black/crimson visual style — a scan-reticle + forward-motion chevron. Swap the files in `icons/` (keeping the same filenames/sizes) if you ever want a different icon.
