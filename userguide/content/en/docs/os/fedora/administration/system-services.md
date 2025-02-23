---
title: "Managing System Services"
description: "In Fedora Linux, system services are managed using the `systemd` system and service manager. The `systemd` suite is responsible for initializing the system in the boot process and controlling system processes after boot. It provides a standard process for starting, stopping, restarting, enabling, and disabling system services."
icon: "code"
draft: false
toc: true
weight: 1
---

## Understanding Systemd Units

In systemd, services are represented as units, which are resources that the system knows how to manage. There are different unit types, but the most common are service units (.service) and socket units (.socket).

- **Service Units**: Represent system services, such as an HTTP server or a database server.
- **Socket Units**: Represent an inter-process communication (IPC) socket, which is used for activating services.

Each unit is defined in a unit file, typically located in the `/usr/lib/systemd/system/` or `/etc/systemd/system/` directories.

## Listing System Services

To list all available system services on your Fedora system, use the following command:

```
systemctl list-unit-files --type=service
```

This command will display a list of all installed service unit files, along with their state (enabled or disabled).

## Starting and Stopping Services

To start a service, use the following command:

```
sudo systemctl start service_name.service
```

Replace `service_name.service` with the name of the service you want to start. For example, to start the Apache HTTP Server, use:

```
sudo systemctl start httpd.service
```

To stop a running service, use the following command:

```
sudo systemctl stop service_name.service
```

You can also restart a service by using the `restart` command:

```
sudo systemctl restart service_name.service
```

## Enabling and Disabling Services

Enabling a service ensures that it starts automatically at system boot. To enable a service, use the following command:

```
sudo systemctl enable service_name.service
```

To disable an enabled service and prevent it from starting at boot, use the following command:

```
sudo systemctl disable service_name.service
```

## Checking Service Status

To check the current status of a service, use the following command:

```
systemctl status service_name.service
```

This command will display the service's current status (active, inactive, or failed), along with any recent log messages related to the service.

## Managing Services with systemctl

The `systemctl` command provides a powerful interface for managing system services. Here are some additional useful commands:

- `systemctl list-units`: List all currently loaded units.
- `systemctl list-units --type=service --state=active`: List all active services.
- `systemctl daemon-reload`: Reload systemd configuration files.
- `systemctl reset-failed`: Reset failed services to their default state.
- `systemctl mask service_name.service`: Mask (disable) a service, preventing it from being started.
- `systemctl unmask service_name.service`: Unmask (enable) a previously masked service.

## Modifying Service Configuration

Most service configuration files are located in the `/etc/systemd/system/` or `/usr/lib/systemd/system/` directories. You can modify these configuration files to change service behavior, such as environment variables or startup options.

However, it's generally recommended to create a new configuration file in the `/etc/systemd/system/` directory with your custom settings. This ensures that your changes won't be overwritten during system updates.

For example, to modify the Apache HTTP Server configuration, create a new file called `/etc/systemd/system/httpd.service.d/custom.conf` with your custom settings:

```
[Service]
Environment=APACHE_LOCK_DIR=/var/run/apache2/lock
```

After making changes to service configuration files, run the following command to reload the systemd configuration:

```
sudo systemctl daemon-reload
```

## Logging and Debugging

Systemd provides comprehensive logging capabilities for services. Service logs are typically stored in the `/var/log/` directory, and you can view them using the `journalctl` command.

To view all log entries for a specific service, use the following command:

```
journalctl -u service_name.service
```

You can also follow the log in real-time with the `-f` (follow) option:

```
journalctl -u service_name.service -f
```

If you encounter issues with a service, you can increase the logging verbosity by modifying the service configuration file and adding the following line:

```
[Service]
Environment=SYSTEMD_LOG_LEVEL=debug
```

After making this change, reload the systemd configuration and restart the service to enable debug logging.

## Conclusion

Managing system services in Fedora Linux with systemd is a powerful and flexible process. By understanding the basic commands and concepts, you can effectively start, stop, enable, disable, and manage services on your Fedora system. Additionally, systemd provides advanced features for service configuration, logging, and debugging, allowing you to tailor services to your specific needs.