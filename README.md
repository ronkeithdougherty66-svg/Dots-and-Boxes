# Dots & Boxes

A two-player, pass-and-play Dots and Boxes game for your phone. Tap a dot, then tap the next one to connect them — complete a box to claim it and score.

This folder is a small installable web app (PWA). Once it's hosted on GitHub Pages, you can add it to your phone's home screen and it'll open full-screen, like a regular app icon — no App Store needed.

## 1. Put it on GitHub

1. Create a new repository on GitHub (public repos get free Pages hosting) — for example `dots-and-boxes`.
2. Upload everything in this folder to the repository, keeping the folder structure:
   ```
   index.html
   manifest.json
   sw.js
   icons/
     icon-192.png
     icon-512.png
     apple-touch-icon.png
     favicon-32.png
   ```
   The easiest way: on the repo's GitHub page, click **Add file → Upload files**, drag all of the above in (including the `icons` folder), and commit.

## 2. Turn on GitHub Pages

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to `Deploy from a branch`.
3. Choose the `main` branch and the `/ (root)` folder, then **Save**.
4. GitHub will give you a URL after a minute or two, something like:
   `https://your-username.github.io/dots-and-boxes/`

## 3. Add it to your phone's home screen

**iPhone (Safari):**
1. Open the GitHub Pages link above in Safari.
2. Tap the **Share** icon (square with an arrow).
3. Tap **Add to Home Screen**, then **Add**.

**Android (Chrome):**
1. Open the link in Chrome.
2. Tap the **⋮** menu in the top right.
3. Tap **Add to Home screen** (or Chrome may show an **Install app** banner automatically) → **Install**.

Either way, you'll get a home screen icon that opens the game full-screen, and it'll keep working even without a signal once you've opened it once.

## Updating later

If you ask me to tweak the game again, just re-upload the changed file(s) to the same GitHub repo (overwriting `index.html`, for instance) — the home screen icon will pick up changes the next time it's opened with a connection.
