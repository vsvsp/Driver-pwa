DARSHANA SETHU DRIVER - FCM BACKGROUND ONLINE REQUEST SETUP

1) Upload these files beside the Driver HTML/PWA:
   - index (32) FCM Background Online Driver.html (rename to index.html if this is your deployed entry)
   - firebase-messaging-sw.js
   - icon-192.png (optional; use your existing PWA icon)

2) Firebase Console -> Project settings -> Cloud Messaging -> Web configuration:
   Create/get the Web Push certificate key (VAPID public key).
   In the Driver HTML replace:
   PASTE_FIREBASE_WEB_PUSH_CERTIFICATE_KEY_HERE
   with that public key.

3) Put functions/ in your Firebase project and run:
   cd functions
   npm install
   firebase deploy --only functions

4) IMPORTANT:
   - The driver must tap Online once while logged in and grant notification permission.
   - The Online state is saved in Firestore as isOnline:true / rideEligible:true.
   - When the PWA is closed, the browser's service worker receives the FCM push and shows the ride notification.
   - The current app still uses Firestore realtime requests when open, so existing data/ride flow remains.
   - This dispatch code sends to ALL approved online drivers with a registered FCM token. It does not yet perform nearby-driver distance selection.
   - For production, Firestore security rules should not allow unrestricted writes until 2026-09-30.
