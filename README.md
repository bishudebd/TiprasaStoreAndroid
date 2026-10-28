# TiprasaStore Android app starter

This is a Kotlin Android Studio project for a branded Android app shell for:
https://tiprasastore.smartbiz.in/

## Important integration limitation

This starter loads the live SmartBiz storefront inside Android WebView. It does **not** use a verified SmartBiz public product/order API. Products, cart, login, payments and order management therefore remain on SmartBiz's website. Payment providers may open a secure browser or app depending on their redirect flow.

I could not verify from public SmartBiz documentation that a supported public storefront API exists for custom native product/order sync. Ask SmartBiz support before paying for API integration.

## Build a debug APK (Windows)

1. Install Android Studio and a compatible JDK (Android Studio's bundled JDK is recommended).
2. Open Android Studio → Open → select this `TiprasaStoreAndroid` folder.
3. Allow Gradle sync and install Android SDK Platform 35 if prompted.
4. In Android Studio choose **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
5. When it finishes, click **locate**. The debug APK is normally at `app/build/outputs/apk/debug/app-debug.apk`.
6. Copy it to your Android phone and install it. If prompted, allow installation from that file source.

Command-line alternative from this folder (after Android SDK/Gradle setup):
```bash
gradlew.bat assembleDebug
```
On macOS/Linux, use `./gradlew assembleDebug` only if you add the Gradle wrapper; alternatively use Android Studio's Gradle task.

## Change the brand

- App name: `app/src/main/res/values/strings.xml`
- Main color: `app/src/main/res/values/colors.xml`
- Store URL: `app/src/main/java/in/tiprasa/store/MainActivity.kt`

## Current features

- Branded status/navigation bars and splash theme
- Storefront WebView
- Loading indicator and progress bar
- Pull-to-refresh
- Back navigation inside the store
- Share store link
- External intents for `tel:`, `mailto:`, and common UPI/payment app links
- Friendly offline/error screen with retry
- Internet connectivity permission

## Before Google Play submission

This project is a **starter/testing project, not a guarantee of Play approval**. Google Play requires useful app functionality and may reject low-value website-only wrappers. Add meaningful, tested app-specific functionality and ensure you have permission to package the store. Complete privacy/data-safety disclosures, provide a privacy policy URL, app icon/screenshots, content rating, target API requirements, and any applicable closed testing requirement for new personal developer accounts. Create a signed release AAB in Android Studio (Build → Generate Signed Bundle / APK → Android App Bundle).

Do not add credentials, payment secrets, or private SmartBiz seller data to the app. Never scrape the storefront or reverse-engineer private APIs.

## Build on GitHub Actions (no local Android Studio required for compiling)

1. Create a GitHub repository named `TiprasaStoreAndroid` (public or private).
2. Upload **all files and folders** from this project, including the hidden `.github/workflows/android-build.yml` file, to the repository root.
3. Open the repository's **Actions** tab. If prompted, enable GitHub Actions.
4. Open **Build TiprasaStore Android** and click **Run workflow**, or push a commit to `main`/`master`.
5. Wait for the workflow to finish. Open the successful workflow run and download the `TiprasaStore-Android-build` artifact.
6. Extract the downloaded artifact ZIP. The debug APK is inside `app/build/outputs/apk/debug/app-debug.apk`.

The workflow also creates an **unsigned** release AAB as a build check. It is not ready for Play Store upload until a release signing key and secure GitHub Actions signing configuration are set up. Never commit a keystore or passwords to the repository.

If you upload files through GitHub's web interface, ensure `.github/workflows/android-build.yml` is included. GitHub's web UI can make hidden dot-folders easy to overlook.


## Fix for GitHub Actions error: "Wrong version in preinstalled sdkmanager"

The workflow was updated to skip `android-actions/setup-android@v3` and use the SDK manager preinstalled on the GitHub-hosted Ubuntu runner directly. Replace the old `.github/workflows/android-build.yml` with the updated one in this project, commit it, and run the workflow again.
