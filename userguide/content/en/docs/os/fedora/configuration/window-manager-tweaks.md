---
title: "Window Manager Tweaks on Fedora Linux"
description: "The window manager is a fundamental component of a desktop environment on Linux, responsible for managing the placement and appearance of application windows, as well as handling user interactions with these windows. Fedora Linux, like many other Linux distributions, offers a range of window managers to choose from, each with its own set of features and customization options."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

In this tutorial, we'll explore various tweaks and customizations you can apply to your window manager on Fedora Linux, enhancing your desktop experience and improving productivity. We'll cover window behavior, keyboard shortcuts, window decorations, and more.

## Prerequisites

Before diving into the tweaks, ensure that you have the following prerequisites:

- A working installation of Fedora Linux
- A desktop environment installed (e.g., GNOME, KDE Plasma, Xfce, or others)
- Basic knowledge of using the terminal and text editor

## Window Behavior

1. **Window Snapping and Tiling**

   Many window managers offer built-in features for snapping windows to the edges of the screen or tiling them in various layouts. These features can significantly improve your multitasking experience and workspace organization.

   - **GNOME**:
     - Enable the "Window Tiling" extension from the GNOME Extensions website or the built-in Tweaks tool.
     - Use keyboard shortcuts like `Super + Left/Right` to snap windows to the left or right half of the screen, or `Super + Up/Down` to maximize or restore windows.

   - **KDE Plasma**:
     - Navigate to "System Settings > Window Management > Window Behavior" and enable the "Window Tiling" option.
     - Use keyboard shortcuts like `Meta + Left/Right` to snap windows to the left or right half of the screen, or `Meta + Up/Down` to maximize or restore windows.

   - **Xfce**:
     - Install the "Window Tiling" plugin from the Xfce Panel's "Window Manager Tweaks" section.
     - Use keyboard shortcuts like `Super + Left/Right` to snap windows to the left or right half of the screen, or `Super + Up/Down` to maximize or restore windows.

2. **Window Focus and Raising**

   Customize how windows are focused and raised when clicked or hovered over.

   - **GNOME**:
     - Use the built-in Tweaks tool to adjust "Window Focus" settings, such as "Click to Focus" or "Focus on Hover."

   - **KDE Plasma**:
     - Navigate to "System Settings > Window Management > Window Behavior" and adjust the "Focus" and "Focus Stealing Prevention" options.

   - **Xfce**:
     - Navigate to "Settings > Window Manager Tweaks > Focus" and adjust the focus behavior settings.

3. **Window Placement and Positioning**

   Control how new windows are positioned and placed on the screen.

   - **GNOME**:
     - Use the built-in Tweaks tool to adjust "Window Tiling" and "Window Placement" settings.

   - **KDE Plasma**:
     - Navigate to "System Settings > Window Management > Window Behavior" and adjust the "Window Placement" and "Window Tiling" options.

   - **Xfce**:
     - Navigate to "Settings > Window Manager Tweaks > Placement" and adjust the window placement settings.

## Keyboard Shortcuts

Keyboard shortcuts can significantly enhance your productivity by allowing you to perform common tasks quickly without having to navigate through menus or use the mouse.

1. **Modifying Existing Shortcuts**

   Most desktop environments provide a way to view and modify existing keyboard shortcuts.

   - **GNOME**:
     - Use the built-in "Settings > Keyboard Shortcuts" tool to view and modify keyboard shortcuts for various actions, such as window management, launching applications, and more.

   - **KDE Plasma**:
     - Navigate to "System Settings > Shortcuts" to view and modify keyboard shortcuts for various components and actions.

   - **Xfce**:
     - Navigate to "Settings > Keyboard" to view and modify keyboard shortcuts for various actions.

2. **Creating Custom Shortcuts**

   In addition to modifying existing shortcuts, you can also create your own custom shortcuts for specific actions or commands.

   - **GNOME**:
     - Use the built-in "Settings > Keyboard Shortcuts" tool and click the "+" button to create a new custom shortcut.

   - **KDE Plasma**:
     - Navigate to "System Settings > Shortcuts > Custom Shortcuts" and click the "Edit" button to create a new custom shortcut.

   - **Xfce**:
     - Navigate to "Settings > Keyboard" and click the "Application Shortcuts" tab to create new custom shortcuts for specific applications or commands.

## Window Decorations

Window decorations refer to the visual elements surrounding application windows, such as the title bar, borders, and window control buttons (minimize, maximize, close). Customizing these decorations can give your desktop a fresh and personalized look.

1. **Changing the Window Theme**

   Most desktop environments provide a selection of pre-installed window themes or allow you to install additional themes from their respective repositories or online sources.

   - **GNOME**:
     - Use the built-in Tweaks tool or the "Settings > Appearance" tool to browse and apply different window themes.

   - **KDE Plasma**:
     - Navigate to "System Settings > Appearance > Window Decorations" to browse and apply different window decoration themes.

   - **Xfce**:
     - Navigate to "Settings > Window Manager > Style" to browse and apply different window themes.

2. **Customizing Window Decorations**

   Some window managers allow you to customize individual elements of the window decorations, such as the title bar layout, button placements, and more.

   - **GNOME**:
     - Use the built-in Tweaks tool or the "Settings > Appearance" tool to adjust various window decoration options, such as button layout and title bar appearance.

   - **KDE Plasma**:
     - Navigate to "System Settings > Appearance > Window Decorations" and click the "Configure Decoration..." button to customize various aspects of the window decorations.

   - **Xfce**:
     - Navigate to "Settings > Window Manager Tweaks > Window Decorations" to customize the appearance of window decorations.

3. **Using Custom Window Decoration Themes**

   If the pre-installed window decoration themes don't meet your needs, you can explore and install custom themes from online sources or create your own.

   - **GNOME**:
     - Search for and install custom GNOME Shell themes from the GNOME Extensions website or other online repositories.

   - **KDE Plasma**:
     - Search for and install custom KDE window decoration themes from online sources like the KDE Store or other repositories.

   - **Xfce**:
     - Search for and install custom Xfce window decoration themes from online sources or create your own by modifying the relevant configuration files.

## Advanced Tweaks

For more advanced users or those seeking even more customization options, there are additional tweaks and configurations you can explore.

1. **Editing Configuration Files**

   Most window managers store their configuration settings in text-based configuration files, typically located in the user's home directory or system-wide directories. By editing these files, you can fine-tune various aspects of the window manager's behavior and appearance.

   - **GNOME**:
     - GNOME settings are stored in the DConf database, which can be edited using the `dconf-editor` tool or by creating custom overrides in the `~/.config/dconf/user` directory.

   - **KDE Plasma**:
     - KDE settings are stored in various configuration files, typically located in the `~/.config/kdeglobals` and `~/.config/kwinrc` directories.

   - **Xfce**:
     - Xfce settings are stored in various configuration files, typically located in the `~/.config/xfce4` directory.

   **Note:** Exercise caution when editing configuration files directly, as incorrect modifications can potentially cause issues or undesired behavior.

2. **Using Advanced Configuration Tools**

   Some window managers provide advanced configuration tools or graphical utilities that allow for more extensive customization options.

   - **GNOME**:
     - The `gnome-tweaks` tool provides additional customization options for various GNOME Shell components, including window behavior and appearance.

   - **KDE Plasma**:
     - The "System Settings" application in KDE Plasma offers a wide range of configuration