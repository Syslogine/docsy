---
title: "Configuring APT Preferences"
description: "Instructions for configuring APT preferences to prioritize package versions, sources, and repositories."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

APT (Advanced Package Tool) preferences allow you to configure how APT selects and prioritizes package versions, sources, and repositories during package installation and upgrade processes. Configuring APT preferences is useful for managing software versions, pinning packages from specific repositories, and ensuring system stability. This guide provides step-by-step instructions for configuring APT preferences in Debian.

## Prerequisites

Before you begin, make sure you have:

- Access to a Debian system with administrative privileges
- Basic understanding of the command line interface

## Step 1: Understanding APT Preferences

APT preferences are defined in configuration files located in the `/etc/apt/preferences.d/` directory. Each preference file specifies rules for package selection and prioritization based on criteria such as package version, origin, and release.

## Step 2: Creating Preference Files

To configure APT preferences, create one or more preference files in the `/etc/apt/preferences.d/` directory using a text editor. Each preference file should have a `.pref` extension and contain one or more preference rules.

For example, create a file named `my-preferences.pref`:

```bash
sudo nano /etc/apt/preferences.d/my-preferences.pref
```

## Step 3: Adding Preference Rules

In the preference file, add preference rules using the following format:

```
Package: <package_name>
Pin: <pinning_criteria>
Pin-Priority: <priority>
```

Replace `<package_name>` with the name of the package, `<pinning_criteria>` with the criteria for pinning the package (e.g., version, origin), and `<priority>` with the pinning priority (0-1000).

For example, to prioritize package versions from a specific repository, you can use:

```
Package: *
Pin: release a=stable
Pin-Priority: 700
```

This rule assigns a priority of 700 to all packages from the stable release.

## Step 4: Understanding Pinning Criteria

Pinning criteria can include package version, distribution release, origin, and component. You can use wildcards (*) and regular expressions to match multiple packages or patterns.

## Step 5: Verifying Preference Settings

After creating preference files, verify the preference settings using the `apt-cache policy` command. For example:

```bash
apt-cache policy
```

This command will display the package versions and priorities according to the configured preferences.

## Conclusion

Configuring APT preferences allows you to customize package selection and prioritization to meet your specific requirements. By creating preference files and adding preference rules, you can prioritize package versions, sources, and repositories according to your preferences and ensure system stability and consistency.
