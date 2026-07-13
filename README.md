# 💬 Chat Application — Native Android Real-time Messaging Suite

> A modern, premium Android real-time chat application inspired by WhatsApp. Built with Java, Firebase Firestore, and Firebase Cloud Messaging (FCM) for instant messaging and push notifications.

🎬 **Watch the Demo Video — Chat Application:** *(add your YouTube link here)*

[![Android](https://img.shields.io/badge/Android-API_24%2B-3DDC84.svg?style=flat-square&logo=android)](https://developer.android.com/)
[![Java](https://img.shields.io/badge/Java-8-ED8B00.svg?style=flat-square&logo=openjdk)](https://www.java.com/)
[![Firebase Firestore](https://img.shields.io/badge/Firebase_Firestore-Cloud-FFCA28.svg?style=flat-square&logo=firebase)](https://firebase.google.com/)
[![FCM Push Notifications](https://img.shields.io/badge/FCM_Notifications-Push-FFCA28.svg?style=flat-square&logo=firebase)](https://firebase.google.com/)

---

## 🌟 Overview

The **Chat Application** is a high-performance, native Android real-time communication platform built on a Firebase Firestore database. The application is designed to simulate a professional messaging experience like WhatsApp or Telegram, enabling real-time conversations, user status updates, profile image sharing, and instant push notifications.

This project was developed as part of coursework at **TechNet Cloud** to demonstrate advanced Android architecture, cloud database integration (NoSQL), Retrofit-based HTTP messaging APIs, and background service lifecycle management.

---

## ✨ Features

- **📨 Real-Time Chatting**: Instantly send and receive messages with sub-second latency powered by Firestore snapshots and listeners.
- **🔔 FCM Push Notifications**: Push notifications are delivered to the recipient's system tray when a new message arrives, using Firebase Cloud Messaging and Retrofit REST APIs.
- **🟢 Active Availability Indicators**: Dynamic online/offline status indicators show when a user is active. Offline indicators also show when they were last active.
- **🔐 Secure Authentication & Signup**: Full user signup and sign-in functionality utilizing Firestore validation, password checks, and persistent preferences.
- **🖼️ Profile Customization**: Users can upload a custom profile picture (base64 encoded) during signup, which is rendered dynamically in message lists and chat interfaces.
- **💬 Recent Conversations Dashboard**: The home screen aggregates the latest messages for each active contact, showing the last message snippet, timestamp, sender, and profile preview.
- **🔍 Global Directory Search**: Find other registered users instantly using a fast-filter user list inside the app.
- **🎛️ Base Lifecycle Activity**: Uses a common `BaseActivity` class to automatically track and update the user's availability status in Firestore based on app foreground/background transitions.

---

## 🛠️ Tech Stack & Architecture

| Layer | Technology |
| :--- | :--- |
| **Language** | Java 8 |
| **UI Framework** | Android XML Layouts |
| **Realtime Database** | Google Firebase Cloud Firestore (NoSQL) |
| **Push Notifications** | Firebase Cloud Messaging (FCM) |
| **Networking** | Retrofit 2 & OkHttp (for sending FCM HTTP requests) |
| **Image Compression** | Custom Bitmap Base64 Encoder/Decoder |
| **State Persistence** | `SharedPreferences` (wrapped in `PreferenceManager`) |
| **Build System** | Gradle (Groovy DSL) |
| **IDE** | Android Studio |

### Core Architectural Classes

- **`BaseActivity`**: Standardizes availability tracking. Automatically toggles database status between Online (`1`) and Offline (`0`) when the app is paused or resumed.
- **`MessagingService`**: Extends `FirebaseMessagingService` to receive background push notifications and display native heads-up system alerts.
- **`RecentConversationAdapter`**: Dynamically binds recent chat summaries to a RecyclerView on the Dashboard.
- **`ChatAdapter`**: Renders bubble messages aligned right (for sender) and left (for receiver).
- **`ApiClient` & `ApiService`**: Interacts with the Firebase Cloud Messaging API to send notifications directly from client to client using a Retrofit service.

---

## 📁 Project Structure

```
ChatApp_AndroidStudio-main/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/daniilss18019262_cs6051_cw/
│   │       │   ├── activities/
│   │       │   │   ├── BaseActivity.java      # Base lifecycle tracker (online/offline)
│   │       │   │   ├── SignInActivity.java    # User login & validation
│   │       │   │   ├── SingUpActivity.java    # Account registration & profile image setup
│   │       │   │   ├── MainActivity.java      # Recent conversations & settings dashboard
│   │       │   │   ├── UsersActivity.java     # Search and launch chats with contacts
│   │       │   │   └── ChatActivity.java      # Active chat window with real-time listeners
│   │       │   │
│   │       │   ├── adapters/
│   │       │   │   ├── ChatAdapter.java       # Formats messages (sender vs receiver bubbles)
│   │       │   │   ├── RecentConversationAdapter.java  # Renders recent message previews
│   │       │   │   └── UsersAdapter.java      # Formats user cards in directory searches
│   │       │   │
│   │       │   ├── firebase/
│   │       │   │   ├── MessagingService.java  # Receives background push notifications
│   │       │   │   └── PreferenceManager.java # SharedPreference utility helper
│   │       │   │
│   │       │   ├── listeners/
│   │       │   │   ├── UserListener.java      # Click callbacks for contact cards
│   │       │   │   └── ConversionListener.java # Click callbacks for recent chat summaries
│   │       │   │
│   │       │   ├── models/
│   │       │   │   ├── User.java              # User data model (ID, name, image, email, availability)
│   │       │   │   └── ChatMessages.java      # Message data model (message, timestamp, sender/receiver)
│   │       │   │
│   │       │   ├── network/
│   │       │   │   ├── ApiClient.java         # Retrofit initialization client
│   │       │   │   └── ApiService.java        # Retrofit API interface for FCM requests
│   │       │   │
│   │       │   └── utilities/
│   │       │       └── Constants.java         # Database keys, keys/values, FCM API header config
│   │       │
│   │       ├── res/
│   │       │   ├── layout/                    # Layout XML templates
│   │       │   ├── drawable/                  # Icons and chat bubble shape drawables
│   │       │   ├── values/                    # Color schemes, styles, strings (Light)
│   │       │   └── values-night/              # Dark mode theme mappings
│   │       │
│   │       └── AndroidManifest.xml            # Services, activities, intent configurations
│   │
│   └── build.gradle                           # App-level dependencies and build configs
│
├── build.gradle                               # Project-level Gradle build configs
├── settings.gradle                            # Module listings
└── README.md
```

---

## 🚀 Setup & Installation

### Prerequisites
- **Android Studio** (Hedgehog or newer)
- **Android SDK** (API Level 24+)
- A **Firebase Account**

---

### Step-by-Step Setup Guide

**1. Clone the Repository:**
```bash
git clone https://github.com/AnasQ2003/Chat_Application.git
cd Chat_Application
```

**2. Setup Firebase Project:**
- Open the [Firebase Console](https://console.firebase.google.com/).
- Create a new project called **ChatApp**.
- Register your Android app using package name: `com.example.daniilss18019262_cs6051_cw`.
- Download the `google-services.json` file and place it inside the `app/` directory of this project.

**3. Configure Firestore Database:**
- In the Firebase Console, go to **Firestore Database** and click **Create Database**.
- Set security rules to test mode or configure custom write permissions.

**4. Setup FCM Server Key (Push Notifications):**
> **Note**: Push notification delivery from device-to-device requires configure headers in `Constants.java`.
- In Firebase Console, go to **Project Settings** (⚙️ icon) → **Cloud Messaging** tab.
- Copy the **Server Key**.
- Open `Constants.java` at `app/src/main/java/com/example/daniilss18019262_cs6051_cw/utilities/Constants.java`.
- Paste the Server Key inside the `getRemoteMsgHeaders()` helper block:
  ```java
  remoteMsgHeaders.put(
      REMOTE_MSG_AUTHORIZATION,
      "key=YOUR_SERVER_KEY_HERE"
  );
  ```

**5. Deploy & Run:**
- Connect a physical Android device or launch an AVD emulator (Android 11 or lower recommended for push notifications).
- Press **▶ Run** in Android Studio.

---

## ⚙️ Build Configuration

| Property | Value |
| :--- | :--- |
| Minimum SDK | API 24 (Android 7.0 Nougat) |
| Target SDK | API 31 (Android 12) |
| Compile SDK | 32 |
| Java Compatibility | Java 8 |
| Version Name | 1.0 |
| Application ID | `com.example.daniilss18019262_cs6051_cw` |

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Anas Ahmed Qureshi** — [@AnasQ2003](https://github.com/AnasQ2003)
*TechNet Cloud — Android Development Coursework*

---

<div align="center">
  <p>Built with ❤️ using <strong>Java & Firebase</strong></p>

  **⭐ If you found this project helpful, please star the repository!**
</div>
