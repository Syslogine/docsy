---
title: "Application Defaults and Associations in Fedora Linux"
description: "In the world of Linux, you have the freedom to choose from a wide range of applications for various tasks. However, this freedom also means that you need to set up your system to associate specific file types, protocols, and MIME types with the applications you prefer. Setting up these associations properly can streamline your workflow and enhance your overall experience."
icon: "code"
draft: false
toc: true
weight: 1
---

## Understanding File Types, Protocols, and MIME Types

Before we dive into the details, let's briefly explain the key terms:

1. **File Types**: These refer to the extensions associated with files, such as `.txt` for text files, `.pdf` for PDF documents, or `.mp3` for audio files. File types help the operating system identify the appropriate application to handle a particular file.

2. **Protocols**: Protocols define the way data is transmitted over a network. Common examples include `http` for web browsing, `mailto` for email clients, and `ftp` for file transfers.

3. **MIME Types**: MIME (Multipurpose Internet Mail Extensions) types are a standardized way of identifying file formats on the internet. They are used by web servers and browsers to determine how to handle different types of content. For example, `text/plain` is a MIME type for plain text files, and `image/jpeg` is for JPEG images.

## Graphical Method: Using the Default Applications Tool

Fedora provides a graphical tool called "Default Applications" that allows you to manage application associations easily. Here's how to use it:

1. Open the "Activities" overview by clicking on the "Activities" icon in the top-left corner of your desktop or by pressing the `Super` (Windows) key.

2. Search for "Default Applications" and click on the corresponding entry.

3. The "Default Applications" window will open, displaying various categories such as "Web," "Mail," "Calendar," "Music," "Video," "Photos," "Terminal," and "Text Editor."

4. Click on a category to see the currently associated applications for that category.

5. To change the default application, click on the desired application from the list or click the "Other..." button to browse for an alternative application.

6. Once you've made your selections, click the "Set as Default" button to apply the changes.

This graphical tool provides a user-friendly way to manage application associations for common file types and protocols. However, it may not cover all possible associations, especially for more obscure file types or protocols.

## Command-Line Method: Using the `xdg-mime` and `xdg-open` Commands

For more advanced or specific associations, you can use the command-line utilities `xdg-mime` and `xdg-open`. These utilities are part of the Freedesktop.org standards and provide a consistent way to manage application associations across different desktop environments.

### Listing Current Associations

To list the current associations for a specific file type or MIME type, use the `xdg-mime` command with the `query` subcommand:

```
xdg-mime query default <file_extension>
```

For example, to check the default application for opening PDF files:

```
xdg-mime query default application/pdf
```

This command will display the currently associated application for the specified file type or MIME type.

### Setting New Associations

To set a new association for a file type or MIME type, use the `xdg-mime` command with the `default` subcommand:

```
xdg-mime default <desktop_file> <mime_type>
```

Replace `<desktop_file>` with the path to the `.desktop` file of the application you want to associate with the specified `<mime_type>`.

For example, to set the Evince document viewer as the default application for opening PDF files:

```
xdg-mime default /usr/share/applications/evince.desktop application/pdf
```

Note that you may need to run this command with `sudo` if you want to set system-wide associations.

### Opening Files with a Specific Application

If you want to open a file with a specific application without changing the default association, you can use the `xdg-open` command:

```
xdg-open <file_path> --app <desktop_file>
```

Replace `<file_path>` with the path to the file you want to open, and `<desktop_file>` with the path to the `.desktop` file of the application you want to use.

For example, to open a PDF file with the Okular document viewer:

```
xdg-open /path/to/document.pdf --app /usr/share/applications/org.kde.okular.desktop
```

### Resetting Associations to Default

If you want to reset the associations for a specific file type or MIME type to their default values, use the `xdg-mime` command with the `default` subcommand and the `--mode` option:

```
xdg-mime default <mime_type> --mode user
```

Replace `<mime_type>` with the MIME type you want to reset.

For example, to reset the associations for PDF files to their default values:

```
xdg-mime default application/pdf --mode user
```

This command will restore the default application associations for the specified MIME type for the current user.

## Managing Associations with Other Tools

While the graphical tool and command-line utilities mentioned above are the primary methods for managing application associations in Fedora, you can also use other tools depending on your desktop environment or preference.

For example, in the GNOME desktop environment, you can use the `dconf-editor` tool to modify application associations through the `org.gnome.desktop.applications` schema.

In the KDE Plasma desktop environment, you can use the "File Associations" tool to manage associations for different file types and MIME types.

Additionally, some applications may provide their own settings or preferences to associate file types with themselves.

## Conclusion

Managing application defaults and associations in Fedora Linux can greatly enhance your productivity and streamline your workflow. By understanding the concepts of file types, protocols, and MIME types, and using the appropriate tools, you can ensure that your system opens the right applications for the corresponding files or protocols.

Whether you prefer the graphical approach or the command-line utilities, this tutorial has provided you with the necessary knowledge and steps to take control of your application associations in Fedora Linux.

Remember, the freedom to choose and customize is one of the core principles of the Linux ecosystem, and managing application associations is an essential aspect of that freedom.