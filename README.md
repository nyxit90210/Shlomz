# One Day at a Time 🔥

A smoke-free stamp card app for your friend, with a monthly surprise scratch card.

## What it does

- **Dark theme**: warm charcoal background with terracotta, sage green, and gold accents — easy on the eyes, day or night.
- **Calendar tab**: Tap any past or present day and choose how it went:
  - **Smoke-free, easy** → a happy swan stamp (🦢) in sage green
  - **Smoke-free, hard** → a checkmark stamp, and you're asked to write about the near-miss (shows up in the Journal)
  - **Smoked** → a sad swan stamp in red, and you're asked what led to it and how to avoid it next time
  - Smoke-free stamps (easy or hard) trigger a full-screen celebration — a giant stamp animation plus confetti across the whole screen.
  - Calendar weeks start on Sunday.
- **Journal & Stats tab**: stats for the viewed month (smoke-free days, best streak, reflections written), plus a feed of all near-miss reflections and "what led to it / how to avoid it" entries.
- **Surprise tab**: A month becomes "ready" the moment every full Sun–Sat week within it is entirely smoke-free — this can happen mid-month, or even retroactively if you go back and fix a missed day later. The app automatically switches to this tab and shows the scratch card the instant a month becomes ready. Scratch with mouse/finger to reveal the surprise (title, icon or photo, and your message). If a month has fully ended without success, it shows the "You're incredible..." message instead, signed "Love, S."
- **Admin tab**: Password-protected (default code: `ramen2026`). Set the title, message, and icon/photo for each of the next 12 months.
- **Language toggle**: EN / עב (Hebrew) — full RTL layout support.
- **Cloud sync** (optional): surprises can sync across devices — see the section below.

## How to use it

### As a website
Upload the whole folder to any static host (GitHub Pages, Netlify, Vercel, etc.) and open `index.html`.

### As a "downloadable" app (PWA)
1. Host the folder online (see above) — PWAs need to be served over HTTPS (or localhost) to install.
2. Open the site on your phone (iOS Safari or Android Chrome).
3. **iOS**: tap Share → "Add to Home Screen".
4. **Android**: tap the browser menu → "Install app" / "Add to Home screen".
5. It now opens full-screen like a normal app and works offline.

### Running locally to test
From this folder, run:
```
python3 -m http.server 8000
```
Then open `http://localhost:8000` in your browser.

## ☁️ Shared storage setup (so your friend sees your updates automatically)

This is a **one-time, 2-minute setup** that you (the admin) do once. After that, every time you save a surprise in the Admin tab, it automatically appears on your friend's phone too — no need to touch their device.

### Step 1: Create a free JSONBin account
1. Go to **jsonbin.io**
2. Click **Sign up** (you can use a Google account)
3. Once logged in, go to the **API Keys** page (in the left menu)
4. Copy your **Master Key** (a long string of letters/numbers) — keep this page open

### Step 2: Create the shared "bin"
1. Go to the JSONBin dashboard, click **Create Bin** (or "+")
2. Paste this exact content into the bin:
   ```json
   {}
   ```
3. Make sure the bin is **Private**
4. Click **Create**
5. After it's created, copy the **Bin ID** shown at the top (a long string like `64f1a2b3c4d5e6f7...`)

### Step 3: Paste your keys into the app
1. Open `index.html` in a text editor (Notepad, TextEdit, or right-click → Edit on GitHub — see below for editing on GitHub directly)
2. Find these two lines near the top of the `<script>` section:
   ```js
   const CLOUD_BIN_ID = "PASTE_YOUR_BIN_ID_HERE";
   const CLOUD_API_KEY = "PASTE_YOUR_API_KEY_HERE";
   ```
3. Replace the text between the quotes with your **Bin ID** and **Master Key** from steps 1–2. For example:
   ```js
   const CLOUD_BIN_ID = "64f1a2b3c4d5e6f7a8b9c0d1";
   const CLOUD_API_KEY = "$2a$10$abc123...";
   ```
4. Save the file and re-upload it (or edit it directly on GitHub — see below)

### How to edit `index.html` directly on GitHub (no downloading needed)
1. Go to your repository on github.com
2. Click on `index.html`
3. Click the pencil icon (✏️ "Edit this file") in the top right
4. Use Ctrl+F (or Cmd+F) to find `PASTE_YOUR_BIN_ID_HERE` and `PASTE_YOUR_API_KEY_HERE`
5. Replace them with your real values (keep the quotes!)
6. Scroll down, click **Commit changes**
7. GitHub Pages will update automatically within ~1 minute

### That's it!
Once both values are filled in:
- The **Admin tab** will show "☁️ Shared with your friend's device"
- Any surprise you save in Admin gets pushed to the cloud automatically
- When your friend opens the Surprise tab, the app checks the cloud for the latest version
- When your friend finishes scratching a card, that "revealed" status also syncs back, so it won't ask them to scratch again

### What stays private vs. shared
- **Shared (cloud)**: surprise titles, messages, icons/photos — basically everything you set in Admin
- **Stays local/private to your friend's device only**: their daily stamps and journal notes — these are never uploaded anywhere

### A note on photos
If you upload a photo as a surprise icon, keep it small (under ~500KB, ideally a square photo resized to around 500x500px) — the free cloud storage has a request limit, and large photos use it up faster. Emojis don't count against this at all, so they're a totally fine default.

### If something's not syncing
- Double check there are no extra spaces or missing quotes around your Bin ID / API Key
- Open the browser console (rarely needed) — sync errors are logged there
- Worst case fallback: the app still works perfectly offline/local — you can always fall back to setting it up directly on your friend's phone



## Customizing
- **Admin code**: search for `ADMIN_CODE` in `index.html` and change the string.
- **Icons**: replace `icons/icon-192.png` and `icons/icon-512.png` with your own artwork (same filenames, square images).
- **Colors/fonts**: all defined as CSS variables near the top of `index.html` (`:root { ... }`).
- **Default first-month surprise**: search for `seedDefault` in the script — this pre-fills the current month's surprise with the ramen workshop. Edit text there or just use the Admin tab.
