# 📱 CryptoTracker

![Kotlin](https://img.shields.io/badge/Kotlin-1.9.0%2B--7952FF?style=flat&square&logo=kotlin&logoColor=white)
![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-1EDA8B?style=flat-square&logo=android&logoColor=white)
![Architecture](https://img.shields.io/badge/Architecture-Clean%20Arch-69B4F0?style=flat-square)

A modern, scalable Android app for tracking cryptocurrency assets in real time, built with Kotlin, Jetpack Compose, and Clean Architecture. Demonstrates a professional, feature-first modular structure designed for maintainability, testability, and easy scaling.

---

## 📋 Screenshots

> 📍 Screenshots coming soon. Run the app locally to see it in action.

---

## 🚀 Features

- Real-time cryptocurrency prices fetched from the CoinCap API v3
- Clean Architecture: Data / Domain / Presentation layers
- Feature-first modularization (app, core, feature modules)
- Robust networking with Ktor and safeCall wrappers
- Strong error mapping: Network vs Serialization vs Server errors
- Secure API key handling via `local.properties` + `BuildConfig`
- 100% Jetpack Compose UI with MVI-style state management

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| Language | Kotlin |
| UI | Jetpack Compose |
| Architecture | MVVM + Clean Architecture (Feature-First) |
| Networking | Ktor Client (JSON, Logging, Auth) |
| DI | Koin |
| Concurrency | Coroutines & Flow |
| Serialization | Kotlinx Serialization |
| State Management | MVI |

---

## 🏗️ Architecture Overview

Package-by-feature structure to maximize modularity and encapsulation:

```
com.plcoding.cryptotracker
├── core                 # Shared foundation (Networking, UI helpers, Utils)
│   ├── data             # HttpClientFactory, constructUrl, responseToResult
│   ├── domain            # Common Result type, Error interfaces
│   └── presentation      # Shared UI components and formatters
├── crypto               # Feature: Cryptocurrency Tracking
│   ├── data             # Repositories, DTOs, Mappers
│   ├── domain           # Entities, Repository interfaces, Use Cases
│   └── presentation     # ViewModels (State), Compose Screens
└── app                  # DI modules, Application entry point
```

---

## ♚️ Getting Started

### Prerequisites

- Android Studio Hedgehog (2023.1.1) or newer
- JDK 17+
- Android SDK 35+

### Setup

1. Clone the repository
   ```bash
   git clone https://github.com/bavlymo1/Crypto-Tracker.git
   cd Crypto-Tracker
   ```

2. Get a free API key
   - Sign up at [coincap.io](https://coincap.io/) and generate an API key from your profile.

3. Configure the API key
   - Open or create `local.properties` in the project root
   - Add:
     ```
     API_KEY=your_api_key_here
     ```
   - The key is exposed to the app via `BuildConfig` - keep `local.properties` out of version control.

4. Open in Android Studio
   - Sync Gradle
   - Build and run on an emulator or physical device

---

## 🛡️ Networking & Security

- `HttpClientFactory` in the `core` module configures Ktor with logging, JSON serialization, timeout settings, and default headers
- API key is injected via `BuildConfig` - never hardcoded
- Centralized `responseToResult` maps HTTP codes (408, 429, 5xx) and exceptions into a type-safe `NetworkError` sealed class

---

## ✅ Error Handling

- Network, Serialization, and Server errors are mapped to a typed `Result<T>` preventing uncaught exceptions
- Retries, backoff, and rate-limiting handling can be added at the repository layer

---

## 🎨 UI

- Fully implemented with Jetpack Compose
- MVI state management inside ViewModels for predictable, testable UI
- Shared UI utilities and formatters live in `core.presentation`

---

## 🤝❡❪ Contributing

Contributions are welcome!

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'feat: add some feature'`
4. Push and open a Pull Request with a clear description and tests if applicable

Please follow the existing module and feature structure when adding new functionality.

---

## 📼 License

This project is open source for learning and demonstration purposes.

---

Made by [Bahy Mohy](https://github.com/bavlymo1) | [LinkedIn](https://www.linkedin.com/in/bahy-mohy-0b5ab6407/)