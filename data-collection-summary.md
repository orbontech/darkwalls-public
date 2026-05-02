# App Store Connect — App Privacy questionnaire answers

Copy/paste into App Store Connect → your app → App Privacy → Edit. Every answer below is derived from an audit of the DarkWalls v1.0.0 codebase; nothing is templated.

---

## Top-level question: "Does your app collect data?"

**Answer: Yes**

This changed from v1.0.0 which shipped without ads. Starting in this version, DarkWalls uses the Google AdMob SDK to serve a Rewarded Interstitial before each wallpaper save. AdMob collects the device's Advertising Identifier (IDFA on iOS, AAID on Android) if the user grants App Tracking Transparency permission.

---

## Data Types collected

| Category | Linked to user? | Used for tracking? | Collected by | Purpose |
|---|---|---|---|---|
| **Identifiers → Device ID** (IDFA / AAID) | ✅ | ✅ | Google AdMob SDK (runtime) | Personalized advertising. Only collected if user grants ATT permission; otherwise non-personalized ads are served and this field is not linked. |
| **Usage Data → Advertising Data** | ✅ | ✅ | Google AdMob SDK (runtime) | Ad impression, click, completion events. |
| **Diagnostics → Crash Data** | ❌ | ❌ | None | No crash-reporting SDK is integrated. |
| **User Content → Photos or Videos** | ❌ | ❌ | None (device only) | The app **writes** to Photos (saves selected wallpapers to a "DarkWalls" album via `expo-media-library`). It never reads Photos. Nothing is uploaded. |
| **Usage Data → Product Interaction** | ❌ | ❌ | Our backend | The `POST /api/wallpapers/:id/download` endpoint receives a wallpaper ID for aggregated popularity counts only. No user or device identifier attached. |
| **Contact Info / Financial / Health / Location / Search History / Browsing History / Purchases / Messages / Sensitive / Surroundings / Other** | ❌ | ❌ | — | Not collected. |

---

## Specific questions → exact answers

| App Store Connect prompt | Answer |
|---|---|
| Does your app collect any data types? | **Yes** |
| Does your app use third-party analytics SDKs? | **No** |
| Does your app use third-party advertising SDKs? | **Yes** — Google AdMob (`react-native-google-mobile-ads`) |
| Does your app use third-party identifier SDKs? | **Yes** — AdMob uses IDFA/AAID |
| Does your app track users across apps/websites owned by other companies? | **Yes** — AdMob advertising attribution |
| Do you use IDFA (Advertising Identifier)? | **Yes** |
| Does your app include SKAdNetwork? | **Yes** — injected by the `react-native-google-mobile-ads` config plugin |
| Have you implemented App Tracking Transparency? | **Yes** — prompted via `expo-tracking-transparency` on first launch, before any AdMob ad request |

---

## Permissions strings (match what App Review sees at runtime)

| Key | Value | Why |
|---|---|---|
| `NSPhotoLibraryAddUsageDescription` | "DarkWalls needs access to save wallpapers to your photo library." | Shown when user first taps Save. |
| `NSPhotoLibraryUsageDescription` | "DarkWalls needs access to save wallpapers to your photo library." | Required as a companion in case read-access code paths exist. |
| `NSUserTrackingUsageDescription` | "DarkWalls uses your device's advertising ID to show relevant ads that keep the app free." | Shown on first launch before AdMob init. |

---

## Age rating & content

- **Age rating**: 4+ (matches App Store Connect's base questionnaire: no objectionable content, no gambling, no user-generated content, no unrestricted web, no simulated gambling).
- **User-generated content**: None. Users cannot upload or share photos into the app.
- **Ads**: Active. Rewarded Interstitial before each wallpaper save.
