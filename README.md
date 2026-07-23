# HyroFit — Android app project (Capacitor)

This folder is a real native Android project (via Capacitor) wrapping the
HyroFit web app. I can't compile the `.apk` myself in this sandbox — that
needs Google's Android SDK servers, which aren't reachable here — but the
GitHub Actions workflow in `.github/workflows/build-apk.yml` does the
compiling for you, for free, the moment you push this to GitHub.

## Get your APK (no Android Studio needed)

1. Create a new repo on github.com (public or private, doesn't matter).
2. Push this whole folder to it:
   ```
   git init
   git add .
   git commit -m "HyroFit Android app"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
   git push -u origin main
   ```
3. Go to your repo on GitHub → **Actions** tab. A workflow run will already
   be in progress (or click "Build Android APK" → "Run workflow" to trigger
   it manually). It takes 3-5 minutes.
4. Once it finishes (green check), click into the run → scroll to
   **Artifacts** → download **ration-debug-apk** → unzip it. Inside is
   `app-debug.apk`.
5. Transfer that `.apk` to your phone (email it to yourself, Google Drive,
   USB cable, whatever's easiest).
6. On your phone, open the file. Android will ask to allow installs from
   this source (Settings → your file manager/browser → "Install unknown
   apps" → allow) — this is expected for any app installed outside the Play
   Store. Tap install.
7. Open "HyroFit" from your app drawer. Camera permission prompt will appear
   the first time you open the barcode scanner — allow it.

## If you already have Android Studio installed

Skip GitHub Actions entirely: open the `android/` folder in Android Studio
directly, let it sync, then Run ▶ on your connected phone (with USB
debugging enabled), or Build → Build Bundle(s)/APK(s) → Build APK(s).

## What this is, technically

Capacitor wraps the same `www/index.html` (identical to the standalone web
app) in a native Android WebView shell, so it installs and runs like a real
app — its own icon, no browser bar, camera access, works offline for
everything except barcode lookups and payment. It is not a Play
Store-signed release build; this debug APK is fine to sideload for personal
use, but Google Play requires a signed release build with your own keystore,
which is a further step if you ever want to publish it there.

## Updating the app later

Whenever you change `www/index.html` (or copy in a new version from the
main HyroFit project), just `git push` again — the Actions workflow rebuilds
the APK automatically. Re-download and reinstall on your phone.
