# TheBoringHUDs Documentation

![TheBoringHUDs Build & Test](https://github.com/oorischubert/TheBoringWorker-HUD/actions/workflows/cicd.yml/badge.svg)

## Overview

`TheBoringHUDs` is a Swift-based macOS application that provides custom HUD (Heads-Up Display) management for system controls like volume, brightness, and other macOS features. It replaces the default system HUDs with a more customizable and integrated experience, designed to work seamlessly with the `boring.notch` interface system.

## Features

- **Custom HUD Management**: Replaces default macOS HUDs for volume, brightness, and other system controls
- **Volume Control**: Monitors and manages audio output levels and mute status
- **Brightness Control**: Handles display brightness adjustments
- **Keyboard Monitoring**: Observes key press events for system controls
- **Display Management**: Manages multiple display configurations
- **Integration with boring.notch**: Seamlessly works with the boring.notch notification system
- **Real-time Notifications**: Sends immediate updates to the notification system

## Prerequisites

- macOS 14 or later
- Xcode 15 or later

## Installation

1. **Clone the Repository**

   ```sh
   git clone https://github.com/oorischubert/TheBoringWorker-HUD.git
   cd TheBoringWorker-HUD
   ```

2. **Open the Project**

   Open the `TheBoringHUDs.xcodeproj` file in Xcode:

   ```sh
   open TheBoringHUDs.xcodeproj
   ```

3. **Build and Run**

   Build and run the project in Xcode. Ensure all necessary permissions are granted for:

   - Accessibility (for key monitoring)
   - Notifications (for HUD display)
   - System Events (for volume/brightness control)

## Core Components

### Managers

- **HUDManager**: Handles HUD notifications for brightness, volume, and other system controls
- **VolumeManager**: Manages audio volume levels and mute status using AppleScript
- **DisplayManager**: Controls display brightness and monitor configurations
- **KeyboardManager**: Monitors keyboard events for system control shortcuts
- **OSDUIManager**: Manages on-screen display elements

### Models

- **BoringViewModel**: Central view model that coordinates between different managers and the notification system

## Usage

### Initialize the HUD System

```swift
import TheBoringHUDs

let viewModel = BoringViewModel()
let hudManager = HUDManager(vm: viewModel)
```

### Send Volume Notifications

```swift
// Get current volume level (0.0 to 1.0)
let volume = VolumeManager.getOutputVolume()

// Check if muted
let isMuted = VolumeManager.isMuted()

// Send volume update notification
hudManager.sendVolumeNotification(value: volume, isMuted: isMuted)
```

### Send Brightness Notifications

```swift
// Send brightness update (0.0 to 1.0)
hudManager.sendBrightnessNotification(value: 0.75)
```

## Integration with boring.notch

`TheBoringHUDs` works in conjunction with the `boring.notch` system to provide a seamless HUD experience. The HUD manager sends notifications to the notch interface, which displays them in an elegant and unobtrusive way.

### How it Works

1. **System Event Detection**: The app monitors system events (volume changes, brightness adjustments, etc.)
2. **HUD Generation**: When an event occurs, the appropriate manager creates a HUD notification
3. **Notification Dispatch**: The notification is sent to `boring.notch` via the distributed notification system
4. **UI Display**: `boring.notch` receives the notification and displays the HUD in the notch area

For details on the UI components and integration, refer to the [boring.notch documentation](https://github.com/TheBoredTeam/boring.notch).

## Permissions Required

This app requires several macOS permissions to function properly:

- **Accessibility Access**: For monitoring keyboard events and system controls
- **Screen Recording**: For detecting display changes (may be required for some features)
- **Notifications**: For sending HUD notifications to the system

Grant these permissions in System Preferences > Security & Privacy when prompted.

## Contributing

1. **Fork the Repository**
2. **Create a Feature Branch**
3. **Commit Your Changes**
4. **Push to the Branch**
5. **Open a Pull Request**

For more details, please refer to our [contributing guidelines](CONTRIBUTING.md).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any issues or questions, please open an issue on [GitHub](https://github.com/oorischubert/TheBoringWorker-HUD/issues).
