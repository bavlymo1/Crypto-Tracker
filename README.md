# 📱 CryptoTracker

A modern, scalable Android app for tracking cryptocurrency assets, built with Kotlin, Jetpack Compose, and Clean Architecture. CryptoTracker demonstrates a professional, feature-first modular structure designed for maintainability, testability, and easy scaling.

## 🚀 Key Features

- Real-time market data fetched from the CoinCap API v3
- Clean Architecture (Data / Domain / Presentation)
- Feature-first modularization (app, core, feature modules)
- Robust networking with Ktor and safeCall wrappers
- Strong error mapping (Network vs Serialization vs Server errors)
- Secure local configuration of API keys via `local.properties` and `BuildConfig`
- 100% Jetpack Compose UI with MVI-style state management

## 🛠️ Tech Stack

- Language: Kotlin
- UI: Jetpack Compose
- Networking: Ktor Client (JSON, Logging, Auth)
- DI: Koin
- Concurrency: Coroutines & Flow
- Serialization: Kotlinx Serialization
- Architecture: MVVM + Clean Architecture (Feature-First)

## 🏗️ Architecture Overview

Package-by-feature structure to maximize modularity and encapsulation:

```
com.plcoding.cryptotracker
├── core                  # Shared foundation (Networking, UI helpers, Utils)
│   ├── data              # HttpClientFactory, constructUrl, responseToResult
│   ├── domain            # Common Result type, Error interfaces
│   └── presentation      # Shared UI components and formatters
├── crypto                # Feature: Cryptocurrency Tracking
│   ├── data              # Repositories, DTOs, Mappers (Data -> Domain)
│   ├── domain            # Entities (Coin), Repository interfaces, Use Cases
│   └── presentation      # ViewModels (State), Compose Screens
└── app                   # DI modules, Application entry point
```

## ⚙️ Setup & Installation

This project uses the CoinCap API v3 which requires a free API key.

1. Clone the repository
   ```bash
   git clone https://github.com/bahboury/Crypto-Tracker.git
   cd Crypto-Tracker
   ```

2. Get an API Key
   - Sign up at https://coincap.io/ and generate a free API Key from your profile.

3. Configure the API key (local & secure)
   - Open `local.properties` in the project root (create it if it doesn't exist).
   - Add:
     ```
     API_KEY=your_api_key_here
     ```
   - The project expects the key to be exposed to the app via a `BuildConfig` field or similar gradle injection. Example (app-level Gradle): add a `buildConfigField` that reads the property and exposes it to `BuildConfig`. Keep `local.properties` out of version control.

4. Open the project in Android Studio
   - Sync Gradle.
   - Build and run on an emulator or physical device.

## 🛡️ Networking & Security

- HttpClientFactory in the `core` module configures Ktor with logging, JSON serialization, timeout settings, and default headers.
- The API key is injected into requests (e.g., `Authorization: Bearer <KEY>`) via a DI-configured interceptor or via the `BuildConfig`.
- A centralized `responseToResult` function maps HTTP codes (e.g., 408, 429, 5xx) and exceptions (No Internet, Parsing) into a type-safe `NetworkError` sealed class so callers receive structured errors instead of crashes.

## ✅ Error Handling

- Network, Serialization, and Server errors are mapped to a typed result (e.g., `Result<T>` / `Either`) preventing uncaught exceptions.
- Retries, backoff, and rate-limiting handling can be implemented at the repository or data-source layer.

## 🎨 UI

- Fully implemented with Jetpack Compose.
- Uses MVI-style state management inside ViewModels to keep UI predictable and testable.
- Shared UI utilities and formatters live in `core.presentation`.

## 🤝 Contributing

Contributions are welcome!

- Fork this repository
- Create a feature branch
- Open a pull request with a clear description and tests if applicable

Please follow the existing module and feature structure when adding new functionality.
