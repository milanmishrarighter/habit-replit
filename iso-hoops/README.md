# Iso Hoops

Isometric flat-illustration basketball, one self-contained HTML5 canvas game
(`www/index.html`) wrapped with Capacitor for Android.

## Play in a browser

Open `www/index.html` — drag back anywhere to aim, release to shoot.

## Build the APK

The GitHub Actions workflow `.github/workflows/iso-hoops-apk.yml` builds a
debug APK on every push and uploads it as the `iso-hoops-debug-apk` artifact.

Locally (needs the Android SDK and JDK 21):

```bash
cd iso-hoops
npm install
npx cap sync android
cd android && ./gradlew assembleDebug
# -> android/app/build/outputs/apk/debug/app-debug.apk
```

Install with `adb install -r app-debug.apk`, or copy the APK to the phone and
open it (allow "install unknown apps").

## Game notes

- Camera: yaw 26°, pitch 0.52, scale fitted to the viewport each resize.
- Physics: 32.17 ft/s², fixed 1/240 s step with an accumulator.
- Launch angle is 70°, not 48°: at 48° a shot from inside ~36 ft reaches
  10 ft only at its apex, so it arrives flat and clangs off the rim every
  time. 70° puts the apex above the ring and gives a ~55° entry.
- Aiming aids: dashed ground track of the whole flight, arc dots for the
  first 45%, a predicted landing ring, a power ring, and the rim lights up
  when the aim lines up with the hoop.
- Points come from where the ball spawned: key = 1, inside the arc = 2,
  beyond the arc = 3. Difficulty escalates at 50 / 80 / 110 / 140 points.
