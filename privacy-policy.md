# DarkWalls — Privacy Policy

**Effective date:** 2026-04-23
**Contact:** privacy@orbontech.com

DarkWalls ("the app", "we", "us") is a wallpaper app published by Orbon Tech. This policy explains exactly what the app does with data — in plain terms, matching what the code actually does, with no template filler.

---

## 1. Summary

- We **do not** create user accounts.
- We **do not** collect any identifier that can be linked to you personally.
- We **do not** show third-party advertising at this time.
- We **do not** use analytics, telemetry, or crash-reporting SDKs.
- Everything you save in the app (favorites, recent searches, download counter) is stored **on your device** and never leaves it.
- The only data that leaves your device is anonymous: the ID of a wallpaper you chose to download, so we can show popularity counts.

---

## 2. What we store on your device

The following items are stored locally using your device's standard app storage (`AsyncStorage` on iOS/Android). They never leave your device unless you back up your phone via Apple / Google.

| Item | Purpose |
|---|---|
| Favorites | Wallpaper IDs you've bookmarked inside the app. |
| Download counter | Count of how many wallpapers you've saved (used to throttle an occasional interstitial). |
| Recent searches | Up to six most-recent search terms you've typed, for quick re-use. |
| Supporter flag | A boolean indicating whether you've tipped the developer via an in-app link, so we can disable ad interruptions for you. |

Uninstalling the app permanently deletes all of the above. There is no way for us, or anyone else, to retrieve it.

---

## 3. What we request from the operating system

- **Photo library write access** (iOS `NSPhotoLibraryAddUsageDescription`, Android `WRITE_EXTERNAL_STORAGE` equivalents via `expo-media-library`) — required to save a wallpaper you've chosen into your Photos and into a "DarkWalls" album. We never read your photo library.
- **Temporary file storage** — when you save a wallpaper, the image is downloaded to a temp folder on your device (`documentDirectory` / `cacheDirectory`), copied to Photos, and the temp copy is deleted.

We do not request location, camera, microphone, contacts, health, HomeKit, or any other sensitive permission.

---

## 4. What we send to our backend

When the app is configured to use our hosted catalogue (a Cloudflare Worker at the URL configured in the app), it makes the following requests:

| Request | What's sent | Purpose |
|---|---|---|
| `GET /api/wallpapers`, `/api/wallpapers/:id`, `/api/categories`, `/api/search`, `/api/tags` | Standard HTTP request; `X-API-Key` header; `X-App-Version` header (the app's release version) | Fetch the wallpaper catalogue and search results. |
| `POST /api/wallpapers/:id/download` | The wallpaper's ID (not yours) | Increments a public download counter so we can show "most downloaded" ordering. |

**No user identifier is ever attached to these requests** — no account, no advertising ID, no device ID, no email. The wallpaper ID travels on its own.

### Cloudflare as infrastructure

Our backend is hosted on Cloudflare Workers. Cloudflare automatically logs the IP address of incoming requests as part of standard infrastructure operations (security, rate limiting). Cloudflare is a GDPR-compliant processor under its standard data-processing addendum. We do not use these logs for profiling, and they expire under Cloudflare's standard retention windows. For details of what Cloudflare logs, see Cloudflare's privacy documentation at cloudflare.com/privacypolicy.

---

## 5. Advertising

At the time this policy takes effect, **no advertising SDK is active in the app**. The Google Mobile Ads SDK is shipped as a dependency but is not initialized anywhere in the codebase, so it neither runs nor collects an advertising identifier.

If we ever enable advertising, this policy will be updated to disclose the advertising partner, what identifier they collect, and where their own policy lives. The app will request `App Tracking Transparency` permission at that time per Apple's rules; you can decline and continue using DarkWalls without degradation.

---

## 6. Analytics and crash reporting

The app currently includes **no analytics or crash reporting SDKs** (no Sentry, no Firebase, no Amplitude, no Mixpanel, none). If we add diagnostics in the future, we will update this document and clearly describe what is collected.

---

## 7. Children's privacy

DarkWalls is rated 4+ and suitable for all ages. We do not knowingly collect data from children — since we do not collect personal data from anyone, this follows automatically. If a parent or guardian has questions, please contact us at privacy@orbontech.com.

---

## 8. Your rights

- **Access / deletion / export**: Since all of your data lives on your device, you already have full access. Uninstalling the app deletes it.
- **Opt-out of download-count tracking**: The anonymous `POST /download` ping contains no information about you; there is no opt-out because there is nothing to opt out of. Blocking the network request (e.g. via a content blocker) will not break the app.
- **Complaints**: You can write to privacy@orbontech.com at any time. Residents of the UAE may also contact the UAE Data Office (uaedataoffice.gov.ae).

---

## 9. Changes to this policy

If we change what the app does with data, we will update this document, update its effective date, and — for material changes — show an in-app notice the first time you open the app after the change. This file is versioned in the app's public repository.

---

## 10. Governing law and contact

This policy is governed by the laws of the United Arab Emirates. Disputes are subject to the exclusive jurisdiction of the UAE courts.

For any privacy question, write to **privacy@orbontech.com**.
