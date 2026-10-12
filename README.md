# EST AI Native Android Repository (GitHub Actions)

This repository wraps the current EST AI website frontend in a Cordova Android WebView app. The website source is included under `www/`; the app uses the existing Render API endpoint configured in `www/app.js`.

## Build APK automatically with GitHub Actions

1. Download and extract this ZIP on your device/computer.
2. Create a **new empty GitHub repository** for the native app.
3. Upload the **extracted files and folders** from this ZIP to the repository root. Do not upload this ZIP as a single file.
4. Make sure `.github/workflows/build-android.yml` is present in the repo. GitHub may hide `.github` in some mobile file pickers; if it is missing, Actions will not run.
5. Commit/push the files to the `main` branch (or `master`). The workflow starts automatically on push.
6. On GitHub, open the repository → **Actions** → **Build EST AI Android APK**.
7. Wait for the workflow to show a green check. Open that run and scroll to **Artifacts**.
8. Download `EST-AI-debug-APK`, extract it, and install `app-debug.apk` on your Android device. Android may ask you to allow installs from that source.

You do **not** upload a ZIP into the Actions tab. GitHub Actions builds the source files after they are committed to the repository. You can also start a build manually from Actions → Build EST AI Android APK → Run workflow.

## What is included

- The full current frontend folder from `ESTAI-Full-App-V1.1.zip`, including HTML, CSS, JavaScript, Firebase web config, logo, brand icons, and intro animation.
- Cordova Android project configuration.
- GitHub Actions workflow that installs the Android platform and produces a debug APK.
- The existing API endpoint is retained in the website JavaScript; the backend itself remains hosted on Render.

## Important limitations to know before publishing

- This workflow creates an **unsigned debug APK** for testing/sideloading. A Play Store release requires a signed release build and secure signing secrets.
- The frontend bundle's own documentation says some features remain prototypes/not connected end-to-end (including image generation, file library/upload, subscription activation, push notifications, and real-time voice/video calls). The APK build does not implement those missing backend features by itself.
- Firebase email/password auth may work in the WebView, but Google OAuth pop-up/redirect behavior inside an embedded Android WebView is not guaranteed. Test Google sign-in on the generated APK; production-quality native Google sign-in may need a native Firebase Authentication integration and matching Firebase configuration.
- Browser speech recognition/speech synthesis support varies inside Android WebView. Microphone permission declarations are included, but they do not guarantee every browser voice feature works on every device.
- The current website's Watch Ads screen contains a banner/ad prototype; this ZIP does not add AdMob rewarded-video integration. Adding AdMob SDK later requires another native build.
- Firebase web configuration in `www/firebase-config.js` is client-side configuration. Never add Firebase Admin private keys, Groq API keys, or Cloudinary secrets to this repository.

## Updating the app later

- Website-only updates can be deployed to Netlify separately, but the APK's bundled `www/` copy will not change until you replace those files and rebuild.
- Native Android changes (such as adding AdMob SDK) require another APK/AAB build. GitHub Actions will build it automatically after you commit the changes.
