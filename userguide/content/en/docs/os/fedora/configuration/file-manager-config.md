---
title: "File Manager Configuration in Fedora Linux"
description: "The file manager in Fedora Linux, known as Nautilus, provides a user-friendly graphical interface for managing files and directories on your system. Nautilus offers a wide range of customization options, allowing you to tailor the file manager's appearance, behavior, and functionality to suit your preferences. In this tutorial, we'll explore various aspects of configuring Nautilus to enhance your file management experience."
icon: "code"
draft: false
toc: true
weight: 1
---

## Accessing Nautilus Preferences

Before diving into the configuration options, let's first understand how to access the Nautilus preferences:

1. Open the Nautilus file manager by clicking on the "Files" icon in the application launcher or by pressing the `Super` (Windows key) + `E` shortcut.
2. Once Nautilus is open, navigate to the "Edit" menu and select "Preferences" or press `Ctrl` + `Q`.

The Nautilus Preferences window will appear, providing you with several tabs to configure different aspects of the file manager.

## Behavior Tab

The "Behavior" tab allows you to customize how Nautilus handles various file operations and interactions.

### General Behavior

- **Single Click to Open Items**: Enable this option if you prefer to open files and folders with a single click instead of the default double-click behavior.
- **Thumbnails**: Configure the appearance of file and folder thumbnails. You can adjust the thumbnail size and choose whether to display thumbnails for specific file types.
- **Date Format**: Customize the date format used to display file and folder modification times.

### Executable Text Files

This section allows you to specify how Nautilus should handle executable text files, such as shell scripts or programming source code files. You can choose whether to display a warning dialog, run the executable file, or disable execution entirely.

### View

- **Sort Folders Before Files**: Enable this option to display folders before files when sorting items in a directory.
- **Show Hidden Files**: Toggle this option to show or hide hidden files and directories (those whose names begin with a period).

## Display Tab

The "Display" tab allows you to customize the appearance of Nautilus and how it displays files and folders.

### Icon View Defaults

- **Use Compact Layout**: Enable this option to display icons in a more compact layout, reducing the amount of white space between items.
- **Default Zoom Level**: Adjust the default zoom level for icon views.
- **Captions**: Configure the captions displayed beneath file and folder icons. You can choose from various options, such as showing the full file name, file type, or custom captions.

### List View Defaults

- **Default Zoom Level**: Adjust the default zoom level for list views.
- **Use Compact Layout**: Enable this option to display files and folders in a more compact list view.
- **Columns**: Customize the columns displayed in the list view by selecting or deselecting specific attributes, such as file name, size, type, and modification date.

### Other Previewable Files

In this section, you can specify which file types should be previewed in the Nautilus window. You can add or remove file types based on their MIME types or file extensions.

## Preview Tab

The "Preview" tab allows you to configure how Nautilus handles file previews and the associated plugins.

### File Contents

- **Preview Text Files**: Enable this option to display the contents of text files in the preview pane.
- **Preview Other Previewable Files**: Enable this option to preview other file types, such as images, PDF documents, and media files, in the preview pane.

### Plugins

Nautilus supports various plugins that extend its functionality. In this section, you can manage installed plugins and enable or disable them according to your preferences.

## Media Tab

The "Media" tab allows you to configure how Nautilus handles various media types, such as audio and video files.

### Multimedia

- **Automatic Run Multimedia Player**: Enable this option to automatically launch the default multimedia player when opening audio or video files.
- **Multimedia Viewer**: Select the preferred multimedia player for handling audio and video files.

### Removable Media

This section allows you to configure how Nautilus handles removable media, such as USB drives, external hard drives, and optical discs.

- **Media Automount on Hot Plug**: Enable this option to automatically mount removable media when connected to your system.
- **Autorun Behavior**: Specify how Nautilus should handle autorun features on removable media. You can choose to ignore autorun, prompt for action, or automatically run the autorun program.

## Context Menu Options

Nautilus provides a context menu (right-click menu) that offers additional options and actions for files and folders. You can customize the context menu by adding, removing, or modifying menu items.

To access the context menu configuration, follow these steps:

1. Open the Nautilus file manager.
2. Navigate to the "Edit" menu and select "Preferences" or press `Ctrl` + `Q`.
3. In the Preferences window, switch to the "Behavior" tab.
4. Scroll down to the "Context Menu" section.

In this section, you can enable or disable various context menu items by checking or unchecking the corresponding checkboxes. Some of the available options include:

- **Open in Terminal**: Add a menu item to open a terminal window in the current directory.
- **Scripts**: Enable or disable the display of user-defined scripts in the context menu.
- **Trash**: Add a menu item to move the selected file(s) or folder(s) to the trash.
- **Rename**: Add a menu item to rename the selected file or folder.
- **Compress**: Add a menu item to compress the selected file(s) or folder(s) into an archive.
- **Extract Here**: Add a menu item to extract compressed archives in the current directory.

You can also add custom context menu items by clicking the "Add" button and specifying the required details, such as the label, command, and conditions for displaying the menu item.

## File Associations

Nautilus allows you to associate specific file types with preferred applications, making it easier to open and manage different types of files. To configure file associations, follow these steps:

1. Open the Nautilus file manager.
2. Navigate to the "Edit" menu and select "Preferences" or press `Ctrl` + `Q`.
3. In the Preferences window, switch to the "Behavior" tab.
4. Scroll down to the "File Associations" section.

In the "File Associations" section, you'll find a list of registered file types and their associated applications. You can modify the default application for a file type by selecting it from the list and clicking the "Set Default Application" button.

Alternatively, you can add a new file association by clicking the "Add" button and providing the necessary details, such as the file type (MIME type or file extension) and the preferred application for opening files of that type.

By following this comprehensive tutorial, you'll be able to customize Nautilus, the default file manager in Fedora Linux, to suit your preferences and enhance your file management experience.