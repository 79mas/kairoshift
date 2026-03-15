# KairoShift PWA

Advanced shift tracking app with Google Sign-In and Drive sync.

## Setup Instructions

### 1. Google Cloud Console Setup

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Select your existing project (or create new)
3. Go to **APIs & Services → Credentials**
4. Click your existing **OAuth 2.0 Client ID**
5. Under **Authorized JavaScript origins**, add:
   - `https://YOUR_USERNAME.github.io`
6. Under **Authorized redirect URIs**, add:
   - `https://YOUR_USERNAME.github.io/kairoshift`
7. Save and copy your **Client ID**

### 2. Enable Google Drive API

1. Go to **APIs & Services → Library**
2. Search for **"Google Drive API"** → Enable it
3. Search for **"Google Identity Services"** → Enable it (usually auto-enabled)

### 3. Insert Client ID into index.html

Open `index.html` and replace **both** occurrences of:
```
REPLACE_WITH_YOUR_CLIENT_ID
```
With your actual Client ID (looks like: `123456789-abc...apps.googleusercontent.com`)

**Search for it in two places:**
- `data-client_id="REPLACE_WITH_YOUR_CLIENT_ID"`
- `CLIENT_ID: 'REPLACE_WITH_YOUR_CLIENT_ID'`

### 4. Deploy to GitHub Pages

```bash
# Create repo named 'kairoshift' on GitHub, then:
git init
git add .
git commit -m "Initial KairoShift PWA"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/kairoshift.git
git push -u origin main
```

5. Go to repo **Settings → Pages**
6. Source: **Deploy from branch → main → / (root)**
7. Your app will be live at: `https://YOUR_USERNAME.github.io/kairoshift`

### 5. Install as PWA on Android

1. Open Chrome on Android
2. Go to `https://YOUR_USERNAME.github.io/kairoshift`
3. Tap the **⋮ menu → Add to Home screen**
4. App icon appears on home screen — opens fullscreen like a native app!

## File Structure

```
kairoshift/
├── index.html      ← Main app (React-free vanilla JS)
├── manifest.json   ← PWA manifest
├── sw.js           ← Service Worker (offline support)
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

## How It Works

- **Login**: Google Sign-In (OAuth 2.0 + OIDC)
- **Data**: Stored as `kairoshift.kash` in your private Google Drive
- **Offline**: Service Worker caches app shell, works without internet
- **Backups**: Auto-backup at midnight, keeps last 2 days in Drive
- **Privacy**: Data is in YOUR Drive — only you can access it

## Data Storage

Your shift data is saved to a file named `kairoshift.kash` in the root of your Google Drive. This file is:
- Private (only your account can access it)
- Automatically synced on every save
- Backed up daily (2 days retention)

If Drive sync fails, data falls back to browser localStorage automatically.
