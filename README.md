# Fluffy Jar — Android (ad-free build for first Play release)

- Game: `app/src/main/assets/index.html` (WebView, fully offline). `standalone.html` = same file for browser preview.
- Ads **removed** for first release (no ads SDK, no permissions). Original ads version: `ads_backup/`.
- Back button fixed for Android 16 / targetSdk 36 (predictive back).
- Release signing + AAB: see `PLAY_STORE_CHECKLIST.md`.
- Privacy policy template: `PRIVACY_POLICY.html` (fill `[DATE]` and `[YOUR EMAIL ADDRESS]`).
- Adding ads later: `ads_backup/HOW_TO_ADD_ADS_BACK.md`.

NOTE: this project was edited without an Android SDK, so it has **not been compiled here**. Build it with GitHub Actions or Android Studio and test the debug APK on a real phone before uploading.
