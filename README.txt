DealRadar — All-in-one: Push to GitHub, get a hosted app AND an APK
=====================================================================

This folder is a complete, ready-to-push GitHub repo. It contains:

  index.html, manifest.json, sw.js, icons/   -> the app (PWA)
  .github/workflows/deploy-pages.yml         -> auto-hosts it on GitHub Pages
  .github/workflows/build-apk.yml            -> auto-builds a signed .apk
  twa-manifest.json                          -> Android packaging config
  android.keystore.b64                       -> your app's signing key (base64)

ONE-TIME SETUP (about 5 minutes):

1. Create a new empty repo on github.com (any name, Public, no README).

2. Push everything in this folder to it:

     cd dealradar-full
     git init
     git add .
     git commit -m "DealRadar app"
     git branch -M main
     git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
     git push -u origin main

3. Repo -> Settings -> Pages -> under "Build and deployment", set
   Source to "GitHub Actions" (one-time toggle, then it's automatic
   on every push after this).

4. Open twa-manifest.json in the repo, replace every YOUR_USERNAME
   and YOUR_REPO_NAME with your real values, then commit + push
   that change.

5. Repo -> Settings -> Secrets and variables -> Actions ->
   New repository secret. Add TWO:

     ANDROID_KEYSTORE_B64      = paste the full contents of android.keystore.b64
     ANDROID_KEYSTORE_PASSWORD = dealradar123

FROM NOW ON:

Every time you push to main:
  - "Deploy to GitHub Pages" runs -> your app goes live at
    https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/
  - "Build APK" runs -> go to the Actions tab -> open the run ->
    scroll to Artifacts -> download "dealradar-apk" -> unzip -> .apk

Send the .apk to your phone and tap to install (allow "install
unknown apps" if prompted).

NOTE: android.keystore.b64 and its password are your app's signing
identity — keep them private. If Build APK fails, open the failed
run's log for the exact error (Bubblewrap's flags occasionally shift
between versions) and paste it back for a fix.
