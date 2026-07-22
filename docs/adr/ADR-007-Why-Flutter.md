# ADR 007: Selection of Flutter for Mobile Application Development

## Status
**Accepted**

## Context
Together-Wifi requires cross-platform mobile applications (Android and iOS) supporting high-performance map rendering, background geolocation tracking, hardware Wi-Fi scanning, and seamless UI animations.

## Decision
We selected **Flutter (Dart)** as the single cross-platform framework for building mobile applications.

## Consequences

### Positive
- **Single Codebase:** Cross-platform development reduces engineering effort by compiling to native iOS and Android packages from a single codebase.
- **Native Performance:** Renders at 60/120 FPS using Skia/Impeller graphics engines without JS bridge overhead.
- **Rich Hardware Plugin Ecosystem:** Excellent plugin ecosystem for Google Maps, location services, and Wi-Fi network management.

### Negative
- Application bundle size (APK/IPA) is larger than minimalist native Java/Swift apps.
- Native platform channel code is occasionally required for specialized Wi-Fi OS APIs.
