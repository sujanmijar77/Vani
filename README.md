# Vaani Captions

Android app that listens to a voice (or takes a video/audio file), transcribes it **on the phone**, and
turns it into styled, word-timed subtitles — exported as a 9:16, 16:9 or 1:1 video, or as .srt/.vtt files.

## Get the APK (no Android Studio needed)

1. Create a new GitHub repository and upload everything in this folder (or `git push` it).
2. Open the repo's **Actions** tab → **Build Android APK** runs by itself (≈ 6–10 min). You can also press **Run workflow**.
3. When it finishes, open **Releases** on the repo page and download **VaaniCaptions.apk**
   (it is also under the run's *Artifacts*).
4. On your phone: open the APK → allow *Install unknown apps* → install.

### Or build locally
```
npm install
npx cap sync android
cd android && ./gradlew assembleDebug      # needs JDK 21 + Android SDK
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```
(or `npx cap open android` and use Android Studio → Build → Build APK)

## Using it

* **Capture tab** – pick the spoken language (Hinglish is the default) and model size.
  Tap *Start listening* for live voice, or *Choose video / audio* to upload a file. Text appears while it works.
* **Edit tab** – fix any wording. Word timings stay attached.
* **Studio tab** – choose 9:16 / 16:9 / 1:1, one of 7 styles (Classic, Karaoke, Pop, Highlight, Neon,
  Typewriter, Lyric), colour, size, position and a timing nudge, then **Export video** or save .srt / .vtt / .txt / word-timing .json.

First use downloads the speech model once (about 110 / 170 / 330 MB for Tiny / Base / Small) and then it works offline.

## Notes

* Speech recognition: OpenAI Whisper (via transformers.js, WASM) running inside the app. Nothing is uploaded.
* **Hinglish** = Whisper recognises the Hindi, then the app converts Devanagari to Roman letters. Spelling follows common
  Hinglish habits but is approximate — use the Edit tab for names and slang.
* Export records the preview in real time, so a 1-minute video takes about 1 minute. Keep the app open and the screen on.
* The APK is debug-signed: fine for installing on your own devices, not for Google Play (needs a release keystore).
* `npm test` runs the unit tests for the Hinglish converter, caption grouping and subtitle files.
