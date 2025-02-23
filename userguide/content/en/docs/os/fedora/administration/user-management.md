---
title: "User Management"
description: "This detailed tutorial provides instructions for linux fedora  on the topic: 'User Management in Fedora'. Learn how to create, modify, and delete user accounts in Fedora, as well as manage user permissions and groups."
icon: "code"
draft: false
toc: true
weight: 1
---

## Creating a New User Account

To create a new user account in Fedora, use the `useradd` command. The basic syntax is:

```bash
sudo useradd [options] username
```

Here are some common options:

- `-c "Comment"`: Adds a comment or description for the user.
- `-d /home/directory`: Specifies the user's home directory (default is `/home/username`).
- `-g group`: Sets the primary group for the user.
- `-G groups`: Adds the user to supplementary groups.
- `-s shell`: Specifies the user's login shell (default is `/bin/bash`).

Example:

```bash
sudo useradd -c "John Doe" -m johndoe
```

This command creates a new user account named "johndoe" with a comment "John Doe" and creates a home directory `/home/johndoe`.

## Setting a Password for a User

After creating a user account, you need to set a password for the user. Use the `passwd` command:

```bash
sudo passwd username
```

You will be prompted to enter and confirm the new password.

## Modifying an Existing User Account

To modify an existing user account, use the `usermod` command. The syntax is similar to `useradd`:

```bash
sudo usermod [options] username
```

Some common options include:

- `-c "Comment"`: Changes the user's comment or description.
- `-d /home/directory`: Changes the user's home directory.
- `-g group`: Changes the user's primary group.
- `-G groups`: Adds or removes the user from supplementary groups.
- `-l new_username`: Changes the user's login name.
- `-L`: Locks the user account (prevents login).
- `-U`: Unlocks the user account.

Example:

```bash
sudo usermod -c "John A. Doe" -G developers johndoe
```

This command changes the comment for the user "johndoe" to "John A. Doe" and adds the user to the "developers" group.

## Deleting a User Account

To delete a user account, use the `userdel` command:

```bash
sudo userdel [options] username
```

Common options include:

- `-r`: Removes the user's home directory and mail spool.
- `-f`: Forces the removal of the user account, even if the user is currently logged in.

Example:

```bash
sudo userdel -r johndoe
```

This command removes the user account "johndoe" and the associated home directory.

## User Groups

In addition to managing individual user accounts, Fedora Linux allows you to organize users into groups for better permission management and collaboration.

### Creating a New Group

To create a new group, use the `groupadd` command:

```bash
sudo groupadd groupname
```

Example:

```bash
sudo groupadd developers
```

This command creates a new group named "developers".

### Adding Users to a Group

To add an existing user to a group, use the `usermod` command with the `-G` option:

```bash
sudo usermod -aG groupname username
```

The `-a` option appends the user to the specified group without removing them from their existing groups.

Example:

```bash
sudo usermod -aG developers johndoe
```

This command adds the user "johndoe" to the "developers" group.

### Removing Users from a Group

To remove a user from a group, use the `gpasswd` command:

```bash
sudo gpasswd -d username groupname
```

Example:

```bash
sudo gpasswd -d johndoe developers
```

This command removes the user "johndoe" from the "developers" group.

### Deleting a Group

To delete an existing group, use the `groupdel` command:

```bash
sudo groupdel groupname
```

Example:

```bash
sudo groupdel developers
```

This command deletes the "developers" group from the system.

## User Permissions and File Ownership

In Linux, each file and directory has permissions that determine who can read, write, or execute the file or directory. These permissions are controlled by the owner of the file or directory and the associated group.

### Changing File and Directory Ownership

To change the owner of a file or directory, use the `chown` command:

```bash
sudo chown [options] user[:group] file/directory
```

Common options include:

- `-R`: Recursively changes ownership for directories and their contents.

Example:

```bash
sudo chown johndoe:developers project.txt
```

This command changes the owner of the file `project.txt` to "johndoe" and the group to "developers".

### Changing File and Directory Permissions

To change the permissions of a file or directory, use the `chmod` command:

```bash
sudo chmod [options] mode file/directory
```

The `mode` parameter specifies the new permissions using symbolic or numeric notation. Common symbolic notations include:

- `u` (user), `g` (group), `o` (other)
- `+` (add permission), `-` (remove permission), `=` (set exact permission)
- `r` (read), `w` (write), `x` (execute)

Example:

```bash
sudo chmod u+x script.sh
```

This command adds the execute permission for the owner of the file `script.sh`.

Numeric notation uses a three-digit octal number, where each digit represents the permissions for the owner, group, and others, respectively. For example:

- `755`: Owner has read, write, and execute permissions; group and others have read and execute permissions.
- `644`: Owner has read and write permissions; group and others have read permissions.

Example:

```bash
sudo chmod 644 project.txt
```

This command sets the permissions of the file `project.txt` to read and write for the owner, and read-only for the group and others.

## Conclusion

User management is a critical aspect of system administration in Fedora Linux. This tutorial covered the essential commands and procedures for creating, modifying, and deleting user accounts, managing user groups, and controlling file and directory permissions. By following the best practices outlined in this tutorial, you can ensure secure and efficient user management on your Fedora Linux system.