# WiFi Scout — Root Edition

[![Android Version](https://img.shields.io/badge/Android-8.0%2B%20(API%2026%2B)-brightgreen.svg)](https://developer.android.com)
[![Target SDK](https://img.shields.io/badge/Target%20SDK-35%20(Android%2015%2F16)-blue.svg)](https://developer.android.com)
[![Architecture](https://img.shields.io/badge/Architecture-Kotlin%20%7C%20Compose%20%7C%20M3-emerald.svg)](https://developer.android.com/jetpack/compose)
[![Security](https://img.shields.io/badge/Security-Offline%20%7C%20Android%20KeyStore-cyan.svg)](https://developer.android.com/training/articles/keystore)

**WiFi Scout — Root Edition** is an offline, defensive Wi-Fi scanner, diagnostic suite, and security audit tool built specifically for Android power users and cybersecurity professionals. Designed with a tactical dark charcoal aesthetic and tuned for devices like the **Xiaomi Redmi K60 (mondrian)** running custom ROMs (such as **Project Infinity X** on **Android 16**).

---

## Deliverables & Artifacts

| Deliverable | Location | Size | Application ID | Version |
| :--- | :--- | :--- | :--- | :--- |
| **Release APK** | `dist/WiFiScout-release.apk` | ~11.32 MB | `com.megumin2812.wifiscout` | `1.0.0 (1)` |
| **Debug APK** | `dist/WiFiScout-debug.apk` | ~17.17 MB | `com.megumin2812.wifiscout.debug` | `1.0.0 (1)` |

---

## Key Features

### 1. Real Wi-Fi Scanner (Feature A)
* **Radio State Detection:** Detects whether the Wi-Fi radio is enabled and offers quick re-check status.
* **Access Point Discovery:** Discovers nearby 2.4 GHz, 5 GHz, and 6 GHz (Wi-Fi 6E) access points using official Android Wi-Fi APIs (`WifiManager`).
* **Deep Telemetry:** Displays SSID, BSSID (with privacy redaction detection), RSSI (dBm), signal quality rating (Excellent/Good/Fair/Poor), exact Wi-Fi channel derived from frequency, and security capabilities (WPA3-SAE, WPA2-PSK, WPS, OWE, Open).
* **Search & Filters:** Real-time search across SSIDs and BSSIDs, band filtering (2.4 GHz / 5 GHz / 6 GHz), security protocol filtering (WPA3 / WPA2 / Open), and signal sorting.
* **Network Detail Sheet:** In-depth modal sheet with full advertised beacon capabilities, security posture assessment, and one-tap integration into the Authorized Audit workflow.

### 2. Connected Network Telemetry (Feature B)
* **Real-Time Link Inspection:** Monitors current Wi-Fi link speed (Mbps), RSSI signal levels, operating band, and channel.
* **IP & Routing Details:** Inspects local IPv4 interface assignments (`wlan0`/`wifi`) and network capabilities.
* **Redaction Transparency:** Clearly explains Android 10+ privacy protections when SSID or BSSID are redacted by the OS.

### 3. Password Lab (Feature C)
* **100% Offline Analysis:** Zero internet calls, zero telemetry, zero analytics.
* **Heuristic Scoring Engine:**
  * Length scoring (with penalties for passwords < 12 characters).
  * Character set variety (lowercase, uppercase, numbers, symbols).
  * Detection of repeated characters (`aaa`, `999`), sequential digits (`1234`, `9876`), and keyboard walks (`qwerty`, `asdfgh`).
  * Detection of common dictionary words (`password`, `admin`, `welcome`, `router`, etc.) and calendar years.
  * Substring repetition detection (`wifiwifi`).
  * Transparent entropy estimation in bits ($H = L \cdot \log_2(R)$ adjusted for patterns).
* **Safe In-Memory Demo:** Safe educational demonstration comparing candidate patterns against a local wordlist in memory without sending network packets.
* **Cryptographic Generator:** Secure random password generator (`java.security.SecureRandom`) with customizable lengths, character toggles, and ambiguous character suppression (`1`, `l`, `I`, `0`, `O`).

### 4. Authorized Network Audit (Feature D)
* **Scope Confirmation:** Explicit authorization verification before auditing commences.
* **Hardening Inspection:** Records security standard, router admin credential status, Wi-Fi Protected Setup (WPS) PIN exposure, and Protected Management Frames (802.11w PMF).
* **Actionable Report:** Automatically produces markdown and plain-text audit summaries with risk ratings (Critical, High, Medium, Low).
* **Export & Vault:** Exports reports via standard Android share sheets and encrypts records into local vault storage.

### 5. Root Diagnostics (Feature E)
* **Redmi K60 / Android 16 Tuning:** Tailored for custom ROMs like Project Infinity X on device `mondrian`.
* **Hardware & OS Telemetry:** Reports Manufacturer, Model, Codename, Kernel Version (`/proc/version`), Android Version, API Level, and SELinux enforcement status (`getenforce`).
* **Controlled `su` Execution:** Safe diagnostic check (`su -c id`) with a strict 5-second coroutine timeout. Handles root manager prompts (KernelSU, Magisk, APatch) and user denials gracefully without hanging.
* **Strict Defensive Boundary:** Never modifies protected system files or accesses credential files (`/data/misc/wifi/*`).

### 6. Device Capability Diagnostics (Feature F)
* Comprehensive hardware matrix: 5 GHz, 6 GHz (Wi-Fi 6E), Wi-Fi Direct (P2P), Wi-Fi Aware (NAN), Wi-Fi RTT (802.11mc), and Passpoint support.
* Permission matrix: Location Services, Location permissions, Nearby Wi-Fi Devices permission, and root subsystem presence.

### 7. Encrypted Audit History (Feature G)
* **Android KeyStore Backed:** Audit records are serialized and encrypted using AES-256-GCM (`AndroidKeyStore` provider).
* **Zero Password Persistence:** Evaluated Wi-Fi passwords are never saved to disk.
* **Management:** Full search, view, export, individual deletion, and bulk wipe actions.

---

## Visual Design & Theme

* **Background:** Deep charcoal (`#0B0F11`, `#0F1416`).
* **Surfaces:** Deep black surfaces (`#12171A`, `#1A2226`) with subtle borders (`#2A363E`).
* **Primary Accent:** Muted emerald green (`#10B981` / `#059669`).
* **Secondary Highlight:** Tactical cyan (`#06B6D4` / `#0891B2`).
* **Edge-to-Edge:** Native Android edge-to-edge layout with full support for system bars and gesture navigation.

---

## Technology Stack

* **Language:** Kotlin 2.0.21
* **UI Framework:** Jetpack Compose + Material 3 (Compose BOM `2024.10.00`)
* **Architecture:** MVVM, StateFlow, Coroutines, Navigation Compose
* **Cryptography:** Android KeyStore (AES-256-GCM)
* **Build System:** Gradle 8.10.2 + Android Gradle Plugin 8.6.0
* **Target SDK:** 35 (Android 15 / 16 compatible)
* **Min SDK:** 26 (Android 8.0 Oreo)

---

## How to Install the APK

1. Transfer `dist/WiFiScout-release.apk` (or `WiFiScout-debug.apk`) to your phone via USB or local file sharing.
2. Open your device file manager (e.g., MiXplorer, Solid Explorer, or AOSP Files) and tap the `.apk` file.
3. If prompted, allow your file manager to install unknown apps from this source.
4. Launch **WiFi Scout** from your app drawer.
5. Grant the **Nearby Wi-Fi Devices** (Android 13+) or **Location** permission to permit Android to return Wi-Fi scan results.
6. (Optional) If rooted with KernelSU / Magisk / APatch, open **Root Diagnostics** and tap **Execute Diagnostic SU Probe** when you wish to verify root capabilities.

Alternatively, install via ADB:
```powershell
adb install -r "dist/WiFiScout-release.apk"
```

---

## Android 16 & Project Infinity X Notes

* **Scan Throttling:** Android limits foreground applications to at most 4 scans every 2 minutes. When throttled, WiFi Scout seamlessly displays cached results from the OS rather than failing.
* **Redacted Fields:** On Android 10 and above, SSIDs may display as `<unknown ssid>` and BSSIDs as `02:00:00:00:00:00` if Location services are toggled off in the device quick settings, even if Wi-Fi is active. Ensure Location services are active to view full network names.
* **Root Manager Compatibility:** Tested with Magisk, KernelSU, and APatch `su` implementations.

---

## Automated Test Results

The automated JUnit test suite runs clean:
```text
> Task :app:testDebugUnitTest
> Task :app:testReleaseUnitTest
BUILD SUCCESSFUL in 2m 49s
45 actionable tasks: 45 executed
```
Verified test suites:
* `PasswordAnalyzerTest`: Empty inputs, dictionary words, short lengths, keyboard walks, repeated characters, and high-entropy passwords.
* `WifiBandHelperTest`: Frequency-to-band mapping, channel calculation (2.4 GHz, 5 GHz, 6 GHz), signal categorization, and security capability parsing.
* `PasswordGeneratorTest`: Length verification, ambiguous character exclusion, and complexity combinations.
* `AuditRecordTest`: Markdown audit report formatting and data serialization.

---

## Developer Credit
* **Application:** WiFi Scout — Root Edition
* **Application ID:** `com.megumin2812.wifiscout`
* **Developer:** `megumin2812`
