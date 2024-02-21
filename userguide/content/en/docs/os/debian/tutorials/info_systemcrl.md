---
linktitle: systemctl services
title: systemctl service
tags: ["systemctl","service"]
weight: 1
description: >
 Master Debian services with these quick `systemctl` commands. From starting SSH to checking status, streamline your system management effortlessly.
---

## Usage Examples
In these examples, we'll use the SSH service to demonstrate the utilization of `systemctl` commands.

### Start Service:
```bash
sudo systemctl start ssh
```
Starts the SSH service, allowing remote connections to the system.

### Stop Service:
```bash
sudo systemctl stop ssh
```
Stops the SSH service, disconnecting any active remote connections.

### Restart Service:
```bash
sudo systemctl restart ssh
```
Restarts the SSH service, applying any changes made to its configuration.

### Reload Configuration:
```bash
sudo systemctl reload ssh
```
Reloads the SSH service configuration without restarting, useful for applying changes without disrupting active connections.

### Reload or Restart Service:
```bash
sudo systemctl reload-or-restart ssh
```
Reloads the configuration if possible; otherwise, restarts the SSH service.

### Check Service Status:
```bash
sudo systemctl status ssh
```
Displays the current status and essential information about the SSH service.

### Enable Service on Boot:
```bash
sudo systemctl enable ssh
```
Configures the SSH service to start automatically on system boot.

### Disable Service on Boot:
```bash
sudo systemctl disable ssh
```
Prevents the SSH service from starting automatically on system boot.

### Check if Service is Active:
```bash
sudo systemctl is-active ssh
```
Verifies if the SSH service is currently active.

### Check if Service is Enabled:
```bash
sudo systemctl is-enabled ssh
```
Checks if the SSH service is set to start automatically on system boot.

### Check if Service has Failed:
```bash
sudo systemctl is-failed ssh
```
Indicates whether the SSH service has encountered failure or errors.
