# Redfox Driver V4 — APK/AAB source

## Screens included
1. Secure Driver Login
2. Driver Home
3. Assigned LR List
4. Real QR / barcode scanner
5. Trip Sheet
6. Live GPS status/map shell
7. POD entry module contract

## Real scanner
This project uses Google Play services Code Scanner for QR/Code 128/Code 39 with auto-zoom. Google documents Code Scanner as a permission-minimizing option; it returns the scan result to the app and processes scanning on-device. For a fully custom camera UI, replace it with ML Kit Barcode Scanning. 

## Build
Open `Redfox_Driver_V4_Android` in Android Studio, sync Gradle, then:
- Debug APK: `./gradlew assembleDebug`
- Release APK: `./gradlew assembleRelease`
- Play Store AAB: `./gradlew bundleRelease`

Configure signing for release builds and provide your Google Maps API key before enabling the production map surface.

## Backend
Replace the marked GPS POST section with the authenticated Supabase Edge Function from the V4 backend package. Never embed a Supabase service/secret key in the APK.

## Production POD
Wire `PodScreen.kt` to CameraX/MediaStore + a Compose signature canvas + private Storage upload. Only transition an LR to DELIVERED after photo/signature upload succeeds.

## GPS
The app declares a location foreground service. Android 14+ requires an appropriate foreground-service type, and location foreground services should be started while the app is visible unless a documented exemption applies.
