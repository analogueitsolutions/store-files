# Android and iOS Deployment Checklist

## Before Both Android and iOS Submission

- Use owner-confirmed legal company name: ANALOGUE TECHNOSOL PRIVATE LIMITED.
- Confirm copyright ownership; the owner-confirmed app operator is ANALOGUE TECHNOSOL PRIVATE LIMITED.
- Publish Privacy Policy URL: `https://www.analogueitsolutions.com/privacy-policy/`.
- Use Support URL: `https://www.analogueitsolutions.com/contact/`.
- Create a demo/reviewer account with sample devices and data.
- Confirm production backend URL uses HTTPS.
- Confirm Google Maps API key restrictions for Android and iOS.
- Confirm app icon, adaptive icon, splash screen, and app name are final.
- Confirm app version and build numbers.
- Test login, logout, forgot password, OTP, and password reset.
- Test Monitoring, Tracks, Reports, Geofences/Zones, Alerts, Settings, Account switching, and Auto Lock.
- Test light and dark mode.
- Test no-data/empty states using a reviewer/demo account.
- Test on physical Android device.
- Test on physical iPhone.
- Remove development logs if possible before production.
- Confirm no staging/dev backend is used for production.
- Confirm privacy policy matches actual backend data retention and sharing.

## Configuration and Earlier Implementation Claims to Confirm

The supplied configuration is the current reference. Earlier claims below about the API endpoint and storage need verification against application source; this documentation repository does not contain that source.

- `app.config.js` production package/bundle ID: `com.aits.analogueiot`
- `app.config.js` app name: `Analogue IOT`
- `.env` currently points to `https://dev.bmrjewells.com/api/v2`; confirm this is the real production endpoint or replace it before release.
- Android has fine and coarse location permissions.
- Supplied Expo Location configuration disables Android background location; verify the built manifest.
- Supplied iOS configuration requests foreground location for geofence selection/creation; Always options are disabled.
- SecureStore is used for credentials and saved accounts.
- AsyncStorage is used for preferences and local app data.

## Android Play Console Checklist

### App Setup

- Create app in Play Console.
- App name: Analogue IOT.
- Default language: English.
- App or game: App.
- Free or paid: choose correct option.
- Category: Navigation, Business, or Tools/Utilities.
- Add contact email.
- Add support website.
- Add privacy policy URL.

### Store Listing

- Add short description from `store-listing-content.md`.
- Add full description from `store-listing-content.md`.
- Upload app icon.
- Upload feature graphic.
- Upload phone screenshots.
- Upload tablet screenshots if supporting tablets.
- Add tags related to GPS tracking, fleet management, vehicle tracking.

### Policy

- Complete Data Safety using `app-privacy-and-data-safety.md`.
- Complete App Access and provide login credentials.
- Complete Ads declaration: select No unless ads are added.
- Complete Content Rating questionnaire.
- Complete Target Audience: likely 18+ or business users, not children.
- Complete News app declaration: No.
- Complete Government app declaration: No unless applicable.
- Complete Financial features declaration: No unless applicable.
- Complete Health features declaration: No.
- Verify the release does not request background location; complete background-location declarations only if that behavior is deliberately added.

### Release

- Build Android App Bundle with EAS.
- Upload `.aab` to internal testing first.
- Fix pre-launch report issues.
- Test installation from Play internal testing.
- Promote to closed testing/production when ready.

Suggested command:

```bash
eas build --platform android --profile production
```

Optional submit command:

```bash
eas submit --platform android --profile production
```

## iOS App Store Connect Checklist

### App Information

- Create app in App Store Connect.
- Name: Analogue IOT.
- Bundle ID: `com.aits.analogueiot`.
- SKU: `analogue-iot-ios` or company-specific SKU.
- Primary category: Navigation.
- Secondary category: Business or Utilities.
- Age rating: complete questionnaire based on actual content.

### Store Listing

- Add promotional text from `store-listing-content.md`.
- Add subtitle.
- Add description.
- Add keywords.
- Add support URL.
- Add privacy policy URL.
- Add copyright.
- Upload iPhone screenshots.
- Upload iPad screenshots if iPad support remains enabled.
- Add app review notes and demo login.

### App Privacy

- Complete App Privacy using `app-privacy-and-data-safety.md`.
- Declare precise and coarse location.
- Declare email/name/account identifiers.
- Declare data linked to user where applicable.
- Confirm data is not used for tracking unless tracking SDKs are added.

### Permissions and Review

- Confirm `NSLocationWhenInUseUsageDescription` is user-friendly.
- Verify no stale Always location descriptions or background-location modes remain in the built app.
- Explain foreground phone location separately from vehicle-tracker data in review notes.
- Remove the mandatory phone-number requirement from signup and backend validation; test signup without a number.
- Implement and test in-app initiation of account deletion; email-only instructions are insufficient for this app.
- If the app requires login, provide a working reviewer account.

### Release

- Build iOS app with EAS.
- Upload to TestFlight first.
- Test TestFlight build on real iPhone.
- Submit to App Review after fixing TestFlight issues.

Suggested command:

```bash
eas build --platform ios --profile production
```

Optional submit command:

```bash
eas submit --platform ios --profile production
```

## Recommended App Config Improvements Before Release

- Add `android.versionCode` if not relying only on EAS remote versioning.
- Add `ios.buildNumber` if not relying only on EAS remote versioning.
- Confirm whether `ios.supportsTablet: true` is intentional. If yes, provide iPad screenshots.
- Restrict Google Maps API key by package name/SHA-1 for Android and bundle ID for iOS.
- Replace any development API URL with production API URL.
- Consider adding Android notification permission handling for Android 13+ if push notifications are implemented.
- Publish a public account/data deletion page using `delete-account-policy.md` and add its URL to Play Console where requested. Confirm deletion scope, processing times, and retention periods against backend procedures before publishing.

## Final Manual QA Checklist

- Fresh install works.
- Login works.
- Invalid login shows error.
- Forgot password flow works.
- OTP flow works.
- Monitoring map loads.
- Vehicle list loads.
- Single vehicle details load.
- Route history loads.
- Route replay works.
- Geofence list loads.
- Create/edit/delete geofence works.
- Alerts screens load.
- Reports generate.
- Report export opens.
- Settings save.
- Notification settings save.
- Account switch works.
- Logout clears session.
- Auto-lock works.
- Biometric prompt works where enabled.
- App works after force close.
- App handles denied location permission.
- App handles no internet.
- App handles backend error.
- App handles empty vehicle account.
