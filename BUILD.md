# Jet Pak for Android (Mangmi Air X)

Needs: Node 18+, Android Studio (includes the SDK and JDK).

    npm install
    npx cap add android
    sed -i 's/<activity/<activity android:screenOrientation="sensorLandscape"/' android/app/src/main/AndroidManifest.xml
    npx cap sync android
    cd android && ./gradlew assembleDebug

APK: android/app/build/outputs/apk/debug/app-debug.apk
Copy it to the handheld (USB, or `adb install app-debug.apk`) and allow "install unknown apps".

Controls: the built-in pad is read through the Gamepad API.
D-pad/left stick = move, A / LT / D-pad up = thrust, B / X / Y / RB / RT = fire, Start = pause.
If the pad isn't detected, press any button once. Many handheld launchers also send Enter/arrow keys, which work too.

No-build alternative: host www/index.html anywhere over https, open it in Chrome on the device, and use "Add to Home screen".

## Build in the cloud (no Android Studio)

1. Create a new GitHub repo and push the contents of this folder to the `main` branch
   (the `.github/workflows/build-apk.yml` file must come along).
2. Open the repo's Actions tab. The "Build Jet Pak APK" workflow runs on every push,
   or press "Run workflow" to start it by hand.
3. When it finishes (about 3-5 minutes), open the run and download `jetlift-apk` from Artifacts.
   Unzip it to get `app-debug.apk`, copy it to the handheld, and install it.

The app now runs full screen with no on-screen controls (gamepad / keyboard only). Android fullscreen is applied by the workflow via styles.xml.
