# Analogue IOT — Permissions and App Review Fix

Reviewed October 2, 2026 against the configuration supplied in chat, the rejection screenshot, existing app documents, and official documentation. Application source, dependency versions, generated native files, and backend behavior were not available in this repository. No app code or deployed website was changed.

## What the configuration requests or enables

| Item | Evidence and meaning |
| --- | --- |
| Android precise and approximate location | `ACCESS_FINE_LOCATION` and `ACCESS_COARSE_LOCATION` are explicitly declared. Intended purpose: current location for geofence selection/creation. Runtime permission still needs to be requested by app code. |
| iOS foreground location | `NSLocationWhenInUseUsageDescription` and the Expo Location purpose string describe geofence selection/creation. |
| Background phone location | Disabled through `isIosBackgroundLocationEnabled: false` and `isAndroidBackgroundLocationEnabled: false`; both Always purpose-string options are false. Verify final native files for stale or dependency-added entries. |
| Face ID / biometrics | SecureStore and LocalAuthentication plugins configure Face ID purpose text. LocalAuthentication can add Android `USE_BIOMETRIC` and legacy `USE_FINGERPRINT`. These allow system authentication, not access to biometric templates. |
| Notifications | `expo-notifications` configures notification support. User-visible notifications require the relevant runtime authorization on iOS and Android 13+. Plugin presence does not prove push token registration or server delivery is implemented. |
| Secure storage | SecureStore supports protected local storage; `configureAndroidBackup: true` configures backup handling/exclusions for its encrypted entries. It does not mean biometric data or credentials are uploaded to your backend. |
| External maps | `LSApplicationQueriesSchemes` permits checks for map/navigation apps. It is not a location permission or access to their data. |
| Network updates | The Expo Updates URL configures update delivery. Inspect actual network metadata and provider processing for the policy. This is not a sensitive-data runtime permission. |
| Other access | No explicit contacts, SMS, phone/call-log, camera, microphone, photo-library, or advertising-tracking permission appears in the supplied configuration. Native dependencies can add permissions, so this is not a complete compiled-manifest audit. |

The `ITSAppUsesNonExemptEncryption: false` flag is an export-compliance declaration; it does not mean the app uses no encryption. `googleServicesFile` alone does not prove Firebase Analytics is active. MapLibre does not identify the map/tile host.

Use matching wording in both Face ID plugin entries: “Use Face ID to unlock your Analogue IOT account on this device.” This better describes the purpose than “access your Face ID biometric data.”

Sources: [Expo Location](https://docs.expo.dev/versions/latest/sdk/location/), [LocalAuthentication](https://docs.expo.dev/versions/latest/sdk/local-authentication/), [SecureStore](https://docs.expo.dev/versions/latest/sdk/securestore/), and [Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/). Check documentation matching the installed Expo SDK before changing configuration.

## Required fix for the September 8 rejection

The screenshot explicitly shows “Phone is required.” This is a form/backend collection issue, not a missing phone permission in app.config.js.

1. Prefer removing Phone from signup unless there is an identified optional purpose. Otherwise label it “Phone number (optional)” and explain that purpose.
2. Remove required-field validation in the client, API, and database. Accept an omitted or blank value without a placeholder number. Validate formatting only when a number is supplied.
3. Ensure signup, login, core fleet features, recovery, and deletion work without a phone number or mandatory phone OTP.
4. Check other required information, including Name, for actual necessity; make nonessential profile details optional.
5. Test a new account with no phone number on iPhone and iPad, including the production API. Also test existing accounts and denied location/notification permissions.
6. Update the policy and store declarations to match the shipped behavior. Optional phone collection still needs to be assessed for disclosure; “optional” does not mean “not collected.”
7. Submit a tested replacement build with a new build number and clear review notes. Do not claim the fix is complete before testing it.

Apple requires necessary-only collection and accessible privacy disclosures: [App Review Guidelines, section 5.1.1](https://developer.apple.com/app-store/review/guidelines/#5.1.1).

### Reply template — use only after implementation and testing

Hello App Review Team,

Thank you for identifying the issue in submission 704b497f-8d94-429c-9b91-f5e717feb939. In version [version], build [build], we have [removed the phone-number field from registration / made the phone-number field optional]. Users can create an account and access core features without providing a phone number. We have updated both client and server validation and tested registration with no phone number on [devices].

To verify, open Sign Up, complete the required account fields, [leave the optional Phone field blank, if retained], and select Submit. Our privacy policy and App Privacy disclosures have been updated to reflect the revised behavior.

Thank you.

## Separate account-deletion gap

The existing deletion document provides email instructions only. Because the app supports account creation, implement an accessible way to initiate full account deletion within the app. Do not invent a working menu path in the public policy before implementation. Email-only support is generally insufficient for this type of app. See [Apple account deletion guidance](https://developer.apple.com/support/offering-account-deletion-in-your-app/).

## Website verification and publication

The [official contact page](https://www.analogueitsolutions.com/contact/) confirms Analogue IT Solutions, its Hyderabad address, general email, and phone numbers. It does not verify the registered entity suffix or app backend practices. The [existing website policy](https://www.analogueitsolutions.com/privacy-policy/) concerns website visitors; it does not substantiate app-specific provider, retention, biometric, or location claims.

Publish the completed app policy at a dedicated public URL and link it from the app and store metadata. Verify the operational details for the policy: optional phone purpose if retained, actual data flows/providers, retention and backup expiry, security, processing countries, advertising/tracking practices, and working deletion route. Confirm provider protections before making that commitment. Do not copy unrelated website marketing or consent language into the app policy.

## Owner-confirmed legal entity and internal drafting note

On October 2, 2026, the owner supplied organization developer-account details confirming **ANALOGUE TECHNOSOL PRIVATE LIMITED**, H NO 12-1-532/A/1, 2ND FLOOR, P NO 25/B, BANDLAGUDA, Hyderabad – 500068, India, with development.analogue@gmail.com as the account email. These details supersede the website business name and contact address for identification of the app’s legal operator.

The public policy’s publication reminder was moved here: the draft describes the intended release without a mandatory phone number and with foreground-only phone location. The reviewed build required a phone number. Confirm implementation and verify remaining operational details before publication. Backend practices have not been audited. Legal-entity confirmation does not establish retention periods, providers, or release behavior.

## Public policy cleanup

The public policy now contains reader-facing text without drafting placeholders. No numeric retention period, hosting country, analytics provider, sale/tracking claim, or implemented in-app deletion route has been invented. The supplied Expo configuration does not establish these facts. The policy discloses phone numbers where supplied without falsely claiming the rejected signup flow has been fixed. Phone optionality/removal and in-app deletion remain implementation work. Provider-protection and security wording are operational commitments to uphold, not findings of a backend audit. Complete the data-flow assessment and add any further disclosures required by actual processing before treating this as a fully verified notice.
