# L ScalpX Bot — turning this into a real installable Android app (.apk)

I can't compile and sign an .apk myself in this environment — that genuinely
needs either Android Studio or a build service, neither of which I have
access to here. But there's a real path that needs **zero terminal, zero
Android Studio**, using tools other people already run for you:

## Step 1 — Put the app on the public internet (needs a real URL)
PWABuilder (step 2) needs to fetch your app from a real https:// address —
it can't use a file on your phone. Easiest free option: GitHub Pages.

1. Go to github.com, sign in (or sign up).
2. Create a new repository, e.g. `lscalpx-app`. Public is fine — there's no
   secret data in this app; your backend URL and login happen at runtime,
   not baked into the file.
3. Upload all 4 files from this folder (`index.html`, `manifest.json`,
   `service-worker.js`, `icon-192.png`, `icon-512.png`) to the repo root.
4. In the repo: Settings → Pages → under "Build and deployment", set
   Source = "Deploy from a branch", Branch = main, folder = / (root). Save.
5. GitHub gives you a URL like `https://yourname.github.io/lscalpx-app/`.
   Open it — you should see the real app running there.

## Step 2 — Turn that URL into a real APK
1. Go to **pwabuilder.com** (an official, free, well-known Microsoft tool
   for exactly this).
2. Paste your GitHub Pages URL in and click "Start".
3. It scores your app as a PWA (manifest + service worker are already
   included, so this should score well) and shows a "Package for Stores"
   button.
4. Choose **Android**. It will ask a few options (package name, e.g.
   `com.yourname.lscalpx`) — defaults are fine.
5. It builds and hands you a **signed .apk** (and/or .aab) file to download
   directly. No install, no terminal, no Android Studio.

## Step 3 — Install it on a phone
Transfer the .apk to an Android phone (email it to yourself, or download
directly on the phone) and open it. Android will ask you to allow installs
from this source once — approve it, then install like any app.

## Notes
- This wraps the exact same app you've been testing — same login, same
  Scanner, same everything. Once you set your backend URL in Account
  settings inside the installed app, it behaves identically to the browser
  version, just as a real home-screen app with its own icon.
- If you update the app later, just re-upload the changed files to the
  same GitHub repo — the installed app will pick up the update next time
  it's opened (the service worker refreshes the cache).
- iPhone users can also "Add to Home Screen" straight from Safari using
  the same hosted URL — no separate build needed for iOS.
