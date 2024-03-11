---
title: "User Account Setup"
description: "Walkthrough for creating user accounts and setting up user permissions during Debian installation, ensuring proper user management and security."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

This walkthrough provides step-by-step instructions for creating user accounts and setting up user permissions during Debian installation. Proper user management and security are essential for maintaining the integrity and security of your Debian system.

## Prerequisites

Before you begin, make sure you have the following:

- Debian installed on your system or virtual machine
- Administrator privileges to create and manage user accounts

## Step 1: Access User Account Setup

1. Log in to your Debian system with administrative privileges.
2. Open a terminal window or access the system settings menu.

## Step 2: Create a New User Account

1. Use the `adduser` command to create a new user account:
   ```
   sudo adduser username
   ```
   Replace `username` with the desired username for the new user.
2. Follow the prompts to set the user's password and provide additional information such as full name, phone number, etc. (optional).

## Step 3: Assign User to Groups

1. Use the `usermod` command to add the user to additional groups:
   ```
   sudo usermod -aG groupname username
   ```
   Replace `groupname` with the name of the group and `username` with the username of the user.
   Repeat this step for each group you want to add the user to.

## Step 4: Configure User Permissions

1. Use the `chown` command to change ownership of files or directories:
   ```
   sudo chown username:groupname filename
   ```
   Replace `username` with the username of the user, `groupname` with the name of the group, and `filename` with the name of the file or directory.
2. Use the `chmod` command to change file permissions:
   ```
   sudo chmod permissions filename
   ```
   Replace `permissions` with the desired permissions (e.g., `755` for read, write, and execute permissions for the owner and read and execute permissions for others) and `filename` with the name of the file or directory.

## Step 5: Test User Account

1. Switch to the newly created user account:
   ```
   su - username
   ```
   Replace `username` with the username of the newly created user.
2. Test the user account by performing various tasks and ensure that permissions are configured correctly.

## Conclusion

You have successfully set up a new user account and configured user permissions in Debian. Proper user management and security practices help ensure the integrity and security of your Debian system.
