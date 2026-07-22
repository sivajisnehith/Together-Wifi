# 17 - Mobile Architecture

## Overview
The Together-Wifi mobile application is built using Flutter (Dart) for Android and iOS devices, designed with clean architecture principles to deliver smooth performance and high reliability.

---

## 1. Application Layering (Clean Architecture)

```
+-------------------------------------------------------+
|                    Presentation Layer                 |
|   - Widgets / Screens (Hotspot Map, Profile, Pay)     |
|   - State Management (BLoC / Provider Controllers)    |
+---------------------------+---------------------------+
                            |
                            v
+-------------------------------------------------------+
|                      Domain Layer                     |
|   - Use Cases (SearchHotspots, ConnectWifi, PaySession)|
|   - Entities & Business Models                        |
+---------------------------+---------------------------+
                            |
                            v
+-------------------------------------------------------+
|                      Data Layer                       |
|   - Repositories Implementation                       |
|   - Remote Data Sources (Dio REST Client, WebSockets) |
|   - Local Data Sources (Secure Storage, SQLite/Hive)  |
+-------------------------------------------------------+
```

---

## 2. Key Modules & Plugins

| Module | Flutter Packages | Purpose |
| :--- | :--- | :--- |
| **State Management** | `flutter_bloc` / `provider` | Reactive state propagation |
| **Networking** | `dio`, `connectivity_plus` | HTTP REST client, offline detection |
| **Maps & Geo** | `google_maps_flutter`, `geolocator` | Interactive map display & geolocation |
| **WiFi Connection** | `wifi_iot`, `network_info_plus` | WiFi scanning & automatic SSID connection |
| **Secure Storage** | `flutter_secure_storage` | Storing JWTs and encryption keys |
| **Payments** | `razorpay_flutter` | In-app payment integration |
| **Push Notifications** | `firebase_messaging`, `flutter_local_notifications` | Push notification delivery |

---

## 3. Offline First & Sync Strategy
- Hotspots visited recently are cached locally in SQLite/Hive.
- Actions performed offline (e.g. pending reviews or disconnect metrics) are stored in an offline queue and synced to the API Gateway once connectivity is re-established.
