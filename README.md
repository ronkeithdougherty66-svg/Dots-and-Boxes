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

## 4. Turn on online play (optional)

You can now play with someone on a different phone, anywhere — not just pass-and-play. This uses your existing Firebase account as the go-between.

**A. Get a Realtime Database going**
1. Open the [Firebase console](https://console.firebase.google.com/) and pick the project you'd like to use (a new one is fine, or reuse an existing one).
2. In the left sidebar, go to **Build → Realtime Database → Create Database**. Pick any region and start in **test mode** for now (we'll lock it down in step C).
3. Once it's created, copy the database URL shown at the top (looks like `https://your-project-default-rtdb.firebaseio.com`).

**B. Get your web app config**
1. In the console, go to **Project settings** (gear icon) → **General**.
2. Under **Your apps**, click the **</>** (web) icon to register a new web app if you don't already have one — you can call it "Dots & Boxes."
3. Firebase will show a `firebaseConfig` object with values like `apiKey`, `authDomain`, `projectId`, etc.
4. Open `index.html` in this folder, find the `firebaseConfig` block near the top of the `<script>` section, and replace the placeholder values with your real ones (including the `databaseURL` from step A).

**C. Lock down access**
By default, anyone who has the Firebase project's database URL could read/write it. Since the app only reads and writes under a `rooms/` path with a random 5-character code, set these rules so it's scoped there: in the Realtime Database section, go to the **Rules** tab and paste:
```json
{
  "rules": {
    "rooms": {
      "$roomCode": {
        ".read": true,
        ".write": true
      }
    },
    ".read": false,
    ".write": false
  }
}
```
Click **Publish**. This keeps everything outside `rooms/` locked, and a room can only be reached by someone who has its code.

**D. Re-upload and play**
1. Upload the edited `index.html` back to your GitHub repo (overwrite the old one).
2. On your phone: open the game, tap **Play online with a partner → Create game**. You'll get a room code and a "Copy invite link" button.
3. Send that code or link to your wife however you like (text, etc.). She opens the game and taps **Play online with a partner**, then either pastes the code and taps **Join**, or just opens the link you sent, which fills the code in for her.
4. From there it plays like normal — you take turns, and each move appears on both phones in real time.

Tapping **Leave online game** on either phone disconnects and returns to local pass-and-play.

## Updating later

If you ask me to tweak the game again, just re-upload the changed file(s) to the same GitHub repo (overwriting `index.html`, for instance) — the home screen icon will pick up changes the next time it's opened with a connection.
