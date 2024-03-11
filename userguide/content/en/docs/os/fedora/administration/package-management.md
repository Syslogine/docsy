---
title: "Package Management"
description: "In Fedora Linux, the default package management system is DNF (Dandified YUM or DNF Next Generation), which is the successor to the YUM package manager. DNF provides a powerful command-line interface for installing, updating, removing, and managing software packages on your Fedora system."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction to DNF

DNF stands for "Dandified YUM" or "DNF Next Generation." It is a modern and improved version of the YUM package manager, offering better performance, improved dependency handling, and additional features.

DNF is a command-line utility that interacts with the package repositories configured on your Fedora system. These repositories contain various software packages, along with their dependencies and metadata.

## Basic DNF Commands

Here are some of the most commonly used DNF commands:

### Installing Packages

To install a new package, use the following command:

```
sudo dnf install package_name
```

Replace `package_name` with the name of the package you want to install.

### Removing Packages

To remove an installed package, use the following command:

```
sudo dnf remove package_name
```

### Updating Packages

To update all installed packages to their latest available versions, run:

```
sudo dnf update
```

### Upgrading the System

To upgrade your entire Fedora system to the latest available version, use:

```
sudo dnf upgrade
```

### Searching for Packages

To search for a package in the configured repositories, use:

```
dnf search keyword
```

Replace `keyword` with the search term you're looking for.

### Listing Installed Packages

To list all installed packages on your system, run:

```
dnf list installed
```

### Getting Package Information

To get detailed information about a package, use:

```
dnf info package_name
```

### Cleaning Up

DNF maintains a cache of package metadata and headers. To clear this cache and free up disk space, run:

```
sudo dnf clean all
```

## Managing Repositories

DNF uses repository files located in the `/etc/yum.repos.d/` directory to determine where to look for packages. These files contain information about the repositories, such as the base URL, package groups, and GPG keys for package verification.

To enable or disable a repository, you can edit the corresponding `.repo` file in the `/etc/yum.repos.d/` directory and set the `enabled` option to `1` (enabled) or `0` (disabled).

You can also add new repositories by creating a new `.repo` file in the same directory. This is useful when you want to install packages from third-party repositories.

## Dependency Management

One of the key strengths of DNF is its ability to handle package dependencies automatically. When you install a package, DNF will automatically resolve and install any required dependencies, ensuring a consistent and functional system.

If a package you're trying to install has unmet dependencies, DNF will inform you about the missing packages and suggest a solution, such as installing additional packages to satisfy the dependencies.

## Additional DNF Features

DNF offers several additional features and options to enhance package management:

- **Groups**: Packages in Fedora are organized into groups based on their functionality. You can list, install, or remove entire groups of packages using the `dnf groups` command.
- **History**: DNF maintains a history of package transactions, allowing you to review and, if necessary, undo or redo previous actions.
- **Plugins**: DNF supports various plugins that extend its functionality, such as providing additional information about packages or enabling parallel downloads.
- **Configuration**: DNF's behavior can be customized by editing the `/etc/dnf/dnf.conf` configuration file or by using command-line options.

## Conclusion

Package management is a crucial aspect of maintaining a Linux system, and DNF is a powerful tool for managing packages in Fedora Linux. By understanding the basic DNF commands, managing repositories, and leveraging its dependency management capabilities, you can keep your Fedora system up-to-date, install new software, and ensure a consistent and functional software environment.

For more advanced usage and a comprehensive list of DNF commands and options, refer to the official DNF documentation or run `man dnf` in your terminal.