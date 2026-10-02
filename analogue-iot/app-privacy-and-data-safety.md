# App Privacy and Data Safety Answers

These are provisional prompts, not verified submission answers. The latest supplied configuration disables background phone location. Confirm every answer against the production app, backend, SDK data flows, and current store definitions; permissions alone do not establish off-device collection. See `permissions-and-review-fix.md`.

## Apple App Store Connect - App Privacy

### Data Types Collected

Contact Info:

- Email Address: Yes
- Name: Yes
- Phone Number: Declare if actually collected, even if optional; remove the mandatory signup requirement.

Location:

- Precise Location: Yes
- Coarse Location: Yes

Identifiers:

- User ID: Yes, if backend account/user ID is used
- Device ID: Yes, device/installation identifiers and GPS device identifiers may be used

User Content:

- Other User Content: Yes, if user-created geofences, groups, settings, reports, or account preferences are stored

Diagnostics:

- Crash Data: Only if crash reporting is enabled
- Performance Data: Only if diagnostics/analytics are enabled

### Purpose Mapping

Email Address:

- App Functionality
- Account Management

Name:

- App Functionality
- Account Management

Precise Location:

- App Functionality
- Safety

Coarse Location:

- App Functionality
- Safety

User ID:

- App Functionality
- Account Management

Device ID:

- App Functionality
- Fraud Prevention/Security

Other User Content:

- App Functionality

Diagnostics:

- Analytics
- App Functionality

### Linked to User

Likely yes for:

- Name
- Email address
- Location
- User ID
- Vehicle/device data
- Geofence and report data

### Used for Tracking Across Apps and Websites

No, unless you add advertising SDKs or cross-app tracking SDKs.

### Background Location

The supplied configuration disables background phone location. Verify the final binary. Vehicle trackers may independently report locations to the backend; assess this data separately.

## Google Play Console - Data Safety

### Does the app collect or share user data?

Collects user data: Yes  
Sharing: assess actual recipients using Google’s definitions and exceptions. Qualifying service-provider transfers are not automatically reportable sharing; do not select Yes or No solely from this document.

### Data Types

Personal info:

- Name
- Email address
- Phone number, only if actually collected (optional after the review fix)
- User IDs

Location:

- Approximate location
- Precise location

App activity:

- App interactions
- In-app search/settings activity, if tracked by backend or analytics

App info and performance:

- Crash logs, if enabled
- Diagnostics, if enabled

Device or other IDs:

- Device or other IDs
- GPS device identifiers
- Installation identifier

Files and docs:

- Mark only if exported reports are uploaded or stored by the app. Current app appears to download/open report export URLs rather than upload user files.

### Is Data Shared?

Shared with:

- Backend/API service providers
- Hosting/infrastructure providers
- Map service providers
- Authorized users under the same organization/account
- Legal authorities when required

Purpose:

- App functionality
- Account management
- Security/fraud prevention
- Analytics, only if enabled

### Is Data Processed Ephemerally?

No for account, location history, reports, geofences, and settings because the app/backend may retain them for service functionality.

### Is Data Required or Optional?

Required:

- Account information
- Vehicle/device identifiers
- Vehicle-tracker data needed for tracking features; distinguish this from optional phone location for geofence assistance.

Optional:

- Phone number, if retained for an explained optional purpose
- Phone location permission for location-assisted geofence features
- Notification preferences
- Biometric/local authentication
- Some app settings

### Can Users Request Data Deletion?

Yes, if you provide a public deletion request method.

Use this email for account/data deletion requests in Play Console: development.analogue@gmail.com

Recommended deletion/support page: https://www.analogueitsolutions.com/contact/

Suggested deletion request text:

Users may request deletion of eligible account and tracking data by contacting development.analogue@gmail.com. Some records may be retained where required for legal, security, contractual, or operational reasons.

### Is Data Encrypted in Transit?

Yes, if production API uses HTTPS.

Important: Confirm production `EXPO_PUBLIC_BASEURL` uses HTTPS before submitting.

### Can Users Delete Data?

Existing documents describe support requests only. Implement and verify in-app initiation of account deletion before iOS submission; do not defer this requirement for an app supporting account creation.

## Permission Declarations

See `permissions-and-review-fix.md` for the current permission inventory. The supplied configuration explicitly declares Android fine/coarse location, configures iOS When In Use location, disables background location, and includes biometric and notification plugins.

Do not infer that both approximate and precise location are collected merely because both permissions exist. Check what leaves the device, is retained, is linked to accounts, and is received from vehicle trackers. Likewise, distinguish operational GPS monitoring from advertising-related tracking in store terminology.

Official form guidance: [Google Play Data Safety](https://support.google.com/googleplay/android-developer/answer/10787469).
