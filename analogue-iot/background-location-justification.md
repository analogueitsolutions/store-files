# Location Review Explanation

Updated October 2, 2026. The former background-location justification is superseded by the configuration supplied by the app owner.

The supplied configuration disables background phone location on Android and iOS. Do not submit a justification claiming continuous tracking of the phone while the app is closed.

## Proposed review explanation — verify against the build

Analogue IOT requests location access while using the app to assist with selecting or creating a geofence. Vehicle locations and trip history supplied by separate GPS trackers are distinct from the phone or tablet’s location. Those trackers may report to the fleet backend independently of whether the mobile app is open.

Confirm this behavior in the release binary and runtime code before using this explanation. See `permissions-and-review-fix.md` for verification and the signup rejection fix.
