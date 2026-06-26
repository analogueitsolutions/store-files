# App Privacy and Data Safety Answers

These answers are based on the current Expo/React Native app code and app configuration. Confirm against production backend behavior before final submission.

## Apple App Store Connect - App Privacy

### Data Types Collected

Contact Info:

- Email Address: Yes
- Name: Yes

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

Answer yes for location access in the background. Provide the explanation from `background-location-justification.md`.

## Google Play Console - Data Safety

### Does the app collect or share user data?

Collects user data: Yes  
Shares user data: Yes, only with service providers and authorized account users as needed for app functionality. Do not mark as sale.

### Data Types

Personal info:

- Name
- Email address
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
- Location data required for tracking features

Optional:

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

Yes, via support/admin request. Add an in-app deletion flow later if required by your account model.

## Permission Declarations

Android permissions in current config:

- `ACCESS_FINE_LOCATION`
- `ACCESS_COARSE_LOCATION`
- Background location is enabled through the Expo Location plugin.

iOS permission descriptions in current config:

- `NSLocationWhenInUseUsageDescription`
- `NSLocationAlwaysAndWhenInUseUsageDescription`

Recommended additional Android permission declaration text:

Analogue IOT uses location access to show live vehicle position, trip tracking, route history, geofence alerts, and safety monitoring. Background location is used so tracking and alerts can continue even when the app is closed or not in use.
