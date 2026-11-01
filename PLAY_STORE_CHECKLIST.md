# Play Store par upload checklist (ad-free version)

## 1. Developer account
- play.google.com/console par account banao (one-time $25 fee).
- Naya **personal** account ho to Google ki **closed testing** requirement (testers + din) check karo — upload se pehle Console mein dekh lo.

## 2. Keystore banao (SIRF EK BAAR, aur backup zaroor rakho)
```
keytool -genkeypair -v -keystore fluffy-release.jks -keyalg RSA -keysize 2048 -validity 10000 -alias fluffy
```
- Keystore file + password + alias kisi safe jagah save karo. **GitHub repo mein mat daalo** (.gitignore mein `*.jks` already hai).
- Play Console mein **Play App Signing** on rehne do (default).

## 3. AAB banao (GitHub Actions)
1. Poora project GitHub repo (root) mein upload karo.
2. Repo → Settings → Secrets and variables → Actions → ye 4 secrets banao:
   - `FLUFFY_KEYSTORE_BASE64` = keystore ka base64. Linux/Mac: `base64 -w0 fluffy-release.jks`. Windows PowerShell: `[Convert]::ToBase64String([IO.File]::ReadAllBytes("fluffy-release.jks"))`
   - `FLUFFY_KEYSTORE_PASSWORD`
   - `FLUFFY_KEY_ALIAS` (= `fluffy`)
   - `FLUFFY_KEY_PASSWORD`
3. Actions → **Build Fluffy Jar** → Run workflow.
4. Artifacts mein `FluffyJar-debug-APK` (phone par test) aur `FluffyJar-release-AAB` (Play ke liye) download karo.

(Android Studio se bhi ho sakta hai: Build → Generate Signed App Bundle.)

## 4. Upload se pehle phone par test (debug APK)
- Level khelo, pause/resume, **back button** (menu se bahar nikalna, pause, leaderboard band), app background/foreground, app band karke dobara kholna (progress save?).

## 5. Play Console mein bharna
- **Privacy policy URL**: `PRIVACY_POLICY.html` mein `[DATE]` aur `[YOUR EMAIL ADDRESS]` badlo, phir kahin host karo (GitHub Pages free hai) aur uska link daalo.
- **Ads**: "Contains ads" = **No**.
- **Data safety**: koi data collect/share nahi (app offline hai, koi permission nahi).
- **Target audience**: general audience (sirf bachchon ke liye select karoge to Families policy lagti hai).
- **Content rating** questionnaire, **App category = Game**.
- **Store listing**: title, short description (80 chars), full description, **icon 512x512** (`play_store_assets/icon_512.png`), **feature graphic 1024x500** (`play_store_assets/feature_graphic_1024x500.png`), kam az kam **2 phone screenshots** (apne phone se lo).
- AAB upload karo → Internal/Closed testing → review → Production.

## Version
`versionCode 3`, `versionName 1.1.0`. Har naye upload par `versionCode` barhana zaroori hai.
