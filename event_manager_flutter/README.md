# Event Manager - Hybrid Mobile Application

**Module**: Web and Mobile Technologies (B9IS126)  
**Institution**: Dublin Business School  
**Assessment**: Hybrid Mobile Application Development  
**Framework**: Flutter  
**Language**: Dart  
**Platform**: Android

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Installation and Setup](#installation-and-setup)
- [Building and Testing](#building-and-testing)
- [Assignment Compliance](#assignment-compliance)
- [Authors](#authors)

---

## Overview

Event Manager is a hybrid mobile application developed using Flutter for the Web and Mobile Technologies module. The application provides a platform for event management, allowing organizers to create and manage events while enabling attendees to discover, register for, and check into events using QR code technology.

The application demonstrates the use of multiple native device features including GPS location services, camera access, and real-time database synchronization through Firebase Cloud Firestore.

### Purpose

The app addresses the need for efficient event management by providing:
- A dual-sided interface for event hosts and attendees
- Real-time event synchronization across devices
- Location-based event discovery
- QR code-based contactless check-in system

---

## Features

### Application Flow

1. **Splash Screen**: Displays the app logo and title on launch (2-second duration)
2. **Role Selection**: Users choose between Host, Attendee, or QR Check-in modes

### Host Features (Event Organizers)

- **Create Events**: Add events with the following details:
  - Title and description
  - Date and time selection
  - Category (Party, Sports, Meetup, Workshop)
  - Event capacity and pricing (optional)
  - Multiple images via camera or gallery
  - Location search using OpenStreetMap API
  - Public/private event toggle

- **Event Management**: View all created events in real-time with the ability to delete events

- **QR Code Check-in System**:
  - Scan attendee QR tickets using device camera
  - Validate ticket data (JSON format)
  - Display event and attendee information
  - Track number of check-ins
  - Camera controls (flash toggle, camera switch)

### Attendee Features (Event Participants)

- **Browse Events**: View all public events in real-time
- **Nearby Events**: Filter events by location (15km radius) using GPS
- **Event Registration**: Register for events with one tap
- **QR Ticket Generation**: Generate a QR code ticket containing event and user details for check-in

---

## Technology Stack

### Core Technologies

- **Framework**: Flutter 3.0+
- **Language**: Dart 2.18+
- **Backend**: Firebase Cloud Firestore (NoSQL real-time database)
- **UI Framework**: Material Design
- **Architecture**: Repository pattern with layered architecture

### Plugins and Native Features

The application integrates six native plugins to meet the assignment requirements:

1. **geolocator (^14.0.2)**: Provides GPS location services for filtering nearby events. Implements Haversine distance calculation to find events within a 15km radius.

2. **image_picker (^1.2.1)**: Enables photo capture via camera and image selection from gallery. Images are compressed (60% quality, 1280px max width) and encoded to Base64 for Firestore storage.

3. **mobile_scanner (^7.1.4)**: Real-time QR code scanning for check-in functionality. Includes camera controls and duplicate scan prevention.

4. **qr_flutter (^4.1.0)**: Generates QR code tickets for attendees containing event and user information in JSON format.

5. **permission_handler (^12.0.1)**: Manages runtime permissions for camera and location access on Android.

6. **cloud_firestore (^6.1.1)**: Firebase Firestore integration for real-time database operations and data synchronization.

### Additional Dependencies

- **http (^1.6.0)**: HTTP client for OpenStreetMap Nominatim API integration
- **shared_preferences (^2.0.15)**: Local storage for registration tracking
- **intl (^0.18.0)**: Date and time formatting
- **uuid (^4.5.2)**: Unique ID generation for events

---

## Project Structure

```
event_manager_flutter/
│
├── android/                          # Android platform configuration
│   ├── app/
│   │   ├── src/main/
│   │   │   ├── AndroidManifest.xml  # Permissions and app configuration
│   │   │   └── res/                 # App icons and splash screen assets
│   │   └── build.gradle             # Android build configuration
│   └── gradle.properties
│
├── ios/                              # iOS platform configuration
│   ├── Runner/
│   │   ├── Info.plist               # iOS permissions
│   │   └── Assets.xcassets/         # iOS icons
│   └── Podfile
│
├── lib/                              # Main application code
│   ├── main.dart                    # App entry point and Firebase initialization
│   ├── firebase_options.dart        # Firebase configuration
│   │
│   ├── models/                      # Data models
│   │   └── event.dart               # Event model with JSON serialization
│   │
│   ├── repository/                  # Data access layer
│   │   ├── event_repository.dart   # Firestore CRUD operations
│   │   └── map_repository.dart     # OpenStreetMap API integration
│   │
│   └── pages/                       # UI screens
│       ├── splash.dart              # Splash screen
│       ├── role_selection.dart      # Role selection screen
│       │
│       ├── host/                    # Host-side screens
│       │   ├── host_home.dart       # Event dashboard
│       │   ├── create_event.dart    # Event creation form
│       │   └── qrCodeScanner.dart   # QR check-in scanner
│       │
│       └── attendee/                # Attendee-side screens
│           ├── attendee_home.dart   # Event browser
│           └── event_detail_screen.dart  # Event details and ticket view
│
├── pubspec.yaml                      # Dependencies and project metadata
├── firebase.json                     # Firebase configuration
└── README.md                         # This file
```

### Code Organization

The project follows a layered architecture:

- **Models**: Data structures with serialization logic
- **Repository**: Abstraction layer for data access (Firestore and external APIs)
- **Pages**: UI components organized by user role (host/attendee)

---

## Installation and Setup

### Prerequisites

- Flutter SDK 3.0 or higher
- Android Studio or VS Code with Flutter plugin
- Git (for version control)

### Steps

1. **Navigate to project directory**:
   ```bash
   cd e:\event_manager_flutter
   ```

2. **Install dependencies**:
   ```bash
   flutter pub get
   ```

3. **Verify Flutter installation**:
   ```bash
   flutter doctor
   ```

4. **Firebase Configuration**: The project is already configured with Firebase. Configuration files are present in:
   - `lib/firebase_options.dart`
   - `android/app/google-services.json`

5. **Run the application**:
   ```bash
   flutter run
   ```

   For a specific device:
   ```bash
   flutter devices
   flutter run -d <device_id>
   ```

---

## Building and Testing

### Development Testing

The application was tested on:
- Android emulator (API level 30+)
- Physical Android device (OPPO Reno F11 5G)

### Build Commands

**Debug Build** (for testing):
```bash
flutter build apk --debug
```
Output: `build/app/outputs/flutter-apk/app-debug.apk`

**Release Build** (for submission):
```bash
flutter build apk --release
```
Output: `build/app/outputs/flutter-apk/app-release.apk`

### Installing APK on Device

```bash
adb install build/app/outputs/flutter-apk/app-release.apk
```

### Testing Performed

- Event creation with image upload and location search
- Real-time event synchronization across multiple devices
- QR code generation and scanning
- Location-based event filtering
- Camera and gallery permissions
- Form validation and error handling

---

## Assignment Compliance

This project meets all requirements for the Hybrid Mobile Application assessment:

### 1. Hybrid Mobile App Structure

- Built using Flutter, a cross-platform hybrid framework
- Supports Android and iOS platforms
- Proper folder structure with platform-specific configurations
- Uses Dart as the primary language

### 2. Two or More Plugins

The application integrates **six native plugins**:
- Geolocation (geolocator)
- Camera (image_picker)
- QR Scanner (mobile_scanner)
- QR Generator (qr_flutter)
- Permissions (permission_handler)
- Firebase Firestore (cloud_firestore)

All plugins are properly configured with required permissions in `AndroidManifest.xml`.

### 3. Splash Screen

- Custom splash screen implemented in `lib/pages/splash.dart`
- Displays app logo and title for 2 seconds
- Automatically navigates to role selection screen

### 4. App Icons

- Custom app icons configured for Android
- Icons provided in multiple densities (mdpi, hdpi, xhdpi, xxhdpi, xxxhdpi)
- Located in `android/app/src/main/res/mipmap-*/`

### 5. Build and Deployment

- Application successfully builds for Android platform
- APK generated and tested on physical device
- No build errors or warnings
- All dependencies properly resolved

### 6. User-Friendly Interface

- Material Design UI components
- Touch-optimized buttons and controls (minimum 48dp touch targets)
- Clear navigation flow
- Loading indicators for async operations
- Error messages and user feedback (snackbars, dialogs)
- Form validation with helpful error messages
- Responsive layouts

---

## Authors

**Group Members**:

Sohaib Sajjad(20053626)
Responsible for frontend development and user experience design, including attendee-side event browsing, GPS-based nearby event filtering, event registration workflow, QR ticket generation, UI consistency using Material Design principles, and usability testing.
Muhammad Husnain Haider(20067616)
Responsible for backend development and application architecture, including Firebase Firestore integration, repository pattern implementation, host-side event management, QR code scanning and validation, plugin configuration, and build/testing on Android devices.

**Module**: Web and Mobile Technologies (B9IS126)  
**Institution**: Dublin Business School  
**Year**: 2025
