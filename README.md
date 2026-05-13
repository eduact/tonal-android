# Tonal — Mobile Android App

This is a **WebView-wrapped Android app** for the Tonal color palette studio. It's a single HTML file (the desktop version adapted for mobile) running inside a native Android shell.

## What's inside

- **Mobile-optimized HTML** (`app/src/main/assets/index.html`) — same data and harmony engine as the desktop version, but rewritten for a phone screen:
  - Bottom tab navigation (Android pattern)
  - Single-column stacked layouts
  - Touch-optimized swatches (no hover states)
  - Sticky preview panels
  - Bottom-sheet modals

- **Android wrapper** (`MainActivity.kt`) — minimal WebView with a JavaScript bridge that lets the app save PNG/SVG exports directly to Downloads and Pictures.

- **GitHub Actions workflow** (`.github/workflows/build.yml`) — builds the APK in the cloud on every push. No Android Studio needed on your machine.

## How to build the APK (no Android Studio)

1. **Create a GitHub repo:**
   ```bash
   cd /path/to/this/folder
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/tonal-android.git
   git push -u origin main
   ```

2. **Wait for GitHub Actions to build:**
   - Go to your repo on GitHub → Actions tab
   - The workflow will run automatically on push
   - Wait ~3-5 minutes for the build to complete

3. **Download the APK:**
   - Click the successful workflow run
   - Scroll to "Artifacts" at the bottom
   - Download `tonal-debug-apk.zip`
   - Extract the ZIP to get `app-debug.apk`

4. **Install on your phone:**
   - Transfer `app-debug.apk` to your phone (via USB, Google Drive, email, etc.)
   - Open the APK file on your phone
   - Android will ask "Install from unknown sources?" → Allow it (this is normal for sideloading)
   - Tap "Install"

## Features that work

- ✅ All 12 color families, 180 shades, harmony engine
- ✅ Palette Builder (up to 4 tones, copy hex, save to library, export PNG/SVG)
- ✅ Outfit Visualizer (2 figures, 4 garments, harmony score)
- ✅ Library (saved palettes in local storage)
- ✅ About page
- ✅ Bottom tab navigation
- ✅ Android safe-area support (notches, gesture bars)
- ✅ PNG/SVG export saves to Pictures/Tonal and Downloads/Tonal

## File structure

```
tonal-android/
├── app/
│   ├── src/main/
│   │   ├── assets/
│   │   │   └── index.html          ← THE ACTUAL APP (66 KB single HTML file)
│   │   ├── java/com/eduardo/tonal/
│   │   │   └── MainActivity.kt     ← WebView wrapper + file-save bridge
│   │   ├── res/                    ← Android resources (icons, colors, theme)
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── .github/workflows/build.yml     ← GitHub Actions workflow
├── build.gradle
├── settings.gradle
└── README.md
```

## APK details

- **Package name:** `com.eduardo.tonal`
- **Min SDK:** Android 7 (API 24)
- **Target SDK:** Android 14 (API 34)
- **Size:** ~4-5 MB (unsigned debug build)
- **Permissions:** INTERNET (only to load Google Fonts from CDN)

## Notes

- The APK is **debug-signed**, which is fine for personal use (sideloading). It's not production-signed, so you can't publish it to the Play Store as-is.
- All data (saved palettes) lives in the WebView's localStorage. Uninstalling the app deletes everything.
- The app works **offline** once the HTML is loaded (fonts may not render without network, but the app is functional).

## Future improvements (if you want to iterate)

- Add a splash screen
- Enable dark mode toggle (CSS already has the tokens, just needs a toggle)
- Add haptic feedback on swatch selection
- Publish to Play Store (requires a production signing key)

---

**Built for Eduardo | May 2026**
