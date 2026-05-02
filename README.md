# YAMS Co-op PWA — Deployment Guide

Your PWA wrapper is ready. Follow these steps to deploy it so members can install it on their Android phones.

## What's in the `pwa-wrapper/` folder

| File | Purpose |
|---|---|
| `index.html` | Main page — shows a splash screen, then loads your Apps Script app |
| `manifest.json` | Tells Android this is an installable app (name, icon, colors) |
| `sw.js` | Service Worker — enables the "Add to Home Screen" feature |
| `icons/` | App icons for the home screen (192px and 512px) |

---

## Step-by-Step: Deploy to GitHub Pages (Free)

### 1. Create a GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. **Repository name**: `yams-coop-app` (or any name you like)
3. Set it to **Public** (required for free GitHub Pages)
4. Click **Create repository**

### 2. Upload the Files

**Option A — Via GitHub Web UI (Easiest):**
1. On your new repo page, click **"uploading an existing file"** (or go to Add file → Upload files)
2. Drag the **entire contents** of the `pwa-wrapper/` folder into the upload area:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192x192.png`
   - `icons/icon-512x512.png`
3. Click **Commit changes**

> **Important:** Upload the *contents* of `pwa-wrapper/`, NOT the folder itself. The `index.html` must be at the root of the repo.

**Option B — Via Git Command Line:**
```bash
cd yams-coop-app/pwa-wrapper
git init
git add .
git commit -m "YAMS Co-op PWA"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/yams-coop-app.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages** (left sidebar)
2. Under "Source", select **Deploy from a branch**
3. Branch: **main**, Folder: **/ (root)**
4. Click **Save**
5. Wait 1–2 minutes, then your app will be live at:

```
https://YOUR_USERNAME.github.io/yams-coop-app/
```

---

## How Members Install the App

Share this link with your members:
```
https://YOUR_USERNAME.github.io/yams-coop-app/
```

### On Android (Chrome):
1. Open the link in **Chrome**
2. A banner will appear at the bottom: **"Install YAMS Co-op"**
3. Tap **Install**
4. The app icon appears on their home screen!
5. Tapping the icon opens the app in full-screen (no browser bar)

### On iPhone (Safari):
1. Open the link in **Safari**
2. Tap the **Share** button (square with arrow)
3. Tap **"Add to Home Screen"**
4. Tap **Add**

---

## Updating the App

If you redeploy your Apps Script (new version URL), update the URL in two places in `pwa-wrapper/index.html`:
1. The `<iframe src="...">` attribute
2. The `APPS_SCRIPT_URL` constant in the `<script>` section

Then push the change to GitHub — it auto-updates within minutes.

---

## Troubleshooting

| Issue | Fix |
|---|---|
| "Install" button doesn't appear | Must be served over HTTPS (GitHub Pages does this automatically). Also, the browser may not show it on first visit — revisit after a few seconds. |
| App shows blank after install | Check that the Apps Script URL is correct and the deployment is set to "Anyone with Google Account". |
| Splash screen stays forever | Your Apps Script may be slow to load — it will auto-dismiss after 8 seconds. |
