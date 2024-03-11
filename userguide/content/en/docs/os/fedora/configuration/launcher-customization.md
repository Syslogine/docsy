---
title: "Application Launcher Customization on Fedora Linux"
description: "The application launcher is a crucial part of your desktop environment, providing quick access to your frequently used applications. Customizing the application launcher can significantly improve your workflow efficiency by allowing you to organize applications, add custom entries, and even create keyboard shortcuts for rapid access. This tutorial will guide you through the process of customizing the application launcher on two popular desktop environments: GNOME and KDE Plasma."
icon: "code"
draft: false
toc: true
weight: 1
---

## GNOME Application Launcher Customization

GNOME is the default desktop environment for Fedora Workstation. The application launcher in GNOME is known as the "Activities Overview." Follow these steps to customize it:

### 1. Rearranging Application Icons

1. Open the Activities Overview by pressing the `Super` key (Windows key) or clicking the "Activities" icon in the top-left corner of the screen.
2. Right-click on an application icon and select "Move to Favorites" to add it to the dock at the left side of the screen.
3. To remove an application from the dock, right-click on its icon and select "Remove from Favorites."
4. You can rearrange the order of the icons in the dock by holding the `Super` key and dragging the icons to their desired positions.

### 2. Creating Custom Application Launchers

You can create custom application launchers for applications, scripts, or commands that are not present in the default list.

1. Open the `~/Desktop` directory in your file manager.
2. Right-click in the directory and select "Create New" -> "Desktop Entry."
3. In the new file, add the following content, replacing the placeholders with your desired values:

```
[Desktop Entry]
Type=Application
Name=Custom Application Name
Comment=A brief description of the application
Exec=/path/to/executable
Icon=/path/to/icon.png
Terminal=false
Categories=Utility;
```

4. Save the file with a `.desktop` extension (e.g., `custom-app.desktop`).
5. The custom application launcher should now appear in the Activities Overview.

### 3. Keyboard Shortcuts

GNOME allows you to set custom keyboard shortcuts for launching applications or performing specific actions.

1. Open the "Settings" application.
2. Navigate to "Keyboard" -> "Keyboard Shortcuts" -> "View and Customize Shortcuts."
3. Scroll down to the "Custom Shortcuts" section and click the "+" button to add a new shortcut.
4. Enter a descriptive name for the shortcut and the command to be executed (e.g., `/path/to/application`).
5. Click the "Set Shortcut" button and press the desired key combination.
6. The new shortcut will be listed in the "Custom Shortcuts" section.

## KDE Plasma Application Launcher Customization

KDE Plasma is another popular desktop environment available on Fedora. The application launcher in KDE Plasma is known as the "Application Launcher" or "Kickoff."

### 1. Rearranging Application Icons

1. Open the Application Launcher by clicking the "K" icon in the bottom-left corner of the screen or by pressing the `Super` key.
2. Right-click on an application icon and select "Add to Favorites" to add it to the favorite applications list.
3. To remove an application from the favorites list, right-click on its icon and select "Remove from Favorites."
4. You can rearrange the order of the icons in the favorites list by holding the `Super` key and dragging the icons to their desired positions.

### 2. Creating Custom Application Launchers

Similar to GNOME, you can create custom application launchers for applications, scripts, or commands that are not present in the default list.

1. Open the `~/.local/share/applications` directory in your file manager.
2. Right-click in the directory and select "Create New" -> "Text File."
3. In the new file, add the following content, replacing the placeholders with your desired values:

```
[Desktop Entry]
Type=Application
Name=Custom Application Name
Comment=A brief description of the application
Exec=/path/to/executable
Icon=/path/to/icon.png
Terminal=false
Categories=Utility;
```

4. Save the file with a `.desktop` extension (e.g., `custom-app.desktop`).
5. The custom application launcher should now appear in the Application Launcher.

### 3. Keyboard Shortcuts

KDE Plasma also allows you to set custom keyboard shortcuts for launching applications or performing specific actions.

1. Open the "System Settings" application.
2. Navigate to "Shortcuts" -> "Custom Shortcuts."
3. Click the "Edit" button next to "Custom Shortcuts."
4. Click the "New" button to create a new custom shortcut.
5. Enter a descriptive name for the shortcut and the command to be executed (e.g., `/path/to/application`).
6. Click the "None" button next to "Shortcut" and press the desired key combination.
7. Click "OK" to save the new shortcut.

## Additional Tips

- You can create categories or folders in the application launcher to better organize your applications. Right-click in an empty space and select "Create New" -> "Folder."
- Consider using keyboard shortcuts for frequently used applications to improve your productivity.
- Customize the appearance of the application launcher by changing themes or icon sets in your desktop environment's settings.
- Regularly review and remove unused application launchers to keep your launcher organized and clutter-free.

Customizing your application launcher can greatly enhance your desktop experience and workflow efficiency. By following the steps outlined in this tutorial, you can tailor the application launcher to suit your specific needs and preferences on Fedora Linux.