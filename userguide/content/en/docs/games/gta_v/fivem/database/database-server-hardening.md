---
title: "Database Server Hardening"
description: "Harden your database server by disabling unnecessary services, enabling firewalls, implementing strong authentication, and enabling auditing and logging."
weight: 3
---

## Disable or Remove Unnecessary Services and Features

```sql
-- MySQL: Disable unnecessary components during installation
# For MySQL 8.0, add the following options during installation:
mysqld=--skip-profiling,--skip-perfschema

# For existing installations, you can disable components in the my.cnf file:
skip-perfschema
skip-profiling
```

```bash
# PostgreSQL: Disable unnecessary components during installation
# Add the following options to the postgresql.conf file:
shared_preload_libraries = '' # Disables all preloaded libraries
```

## Enable Database Server's Built-in Firewall

```sql
-- MySQL: Enable and configure the built-in firewall
# Enable the firewall
INSTALL SONAME 'MYSQLX_FIREWALL';

# Create a whitelist for allowed IP addresses
MYSQLX_FIREWALL_INSTALL(
    'WHITELIST_INET',
    'WHITELIST_USERS',
    'client_ip=192.168.1.0/24,127.0.0.1, user=fivem_viewer,fivem_entry,fivem_admin'
);

# Start the firewall
MYSQLX_FIREWALL_ACTIVATE();
```

```sql
-- PostgreSQL: Enable and configure the built-in firewall (pg_hba.conf)
# Allow connections from specific IP addresses
host    all             all             192.168.1.0/24            md5
host    all             all             127.0.0.1/32               md5

# Deny all other connections
host    all             all             0.0.0.0/0                 reject
```

## Implement Strong Authentication and Least Privilege

```sql
-- Create users with strong passwords and assign roles
CREATE USER 'fivem_viewer'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT fivem_read_only TO 'fivem_viewer'@'localhost';

CREATE USER 'fivem_entry'@'localhost' IDENTIFIED BY 'AnotherStrongPass!';
GRANT fivem_data_entry TO 'fivem_entry'@'localhost';

CREATE USER 'fivem_admin'@'localhost' IDENTIFIED BY 'SuperSecurePass123!';
GRANT fivem_manager TO 'fivem_admin'@'localhost';
```

## Enable Auditing and Logging

```sql
-- MySQL: Enable and configure audit logging
INSTALL SONAME 'server_audit';
SET GLOBAL server_audit_logging=ON;
SET GLOBAL server_audit_file_rotate_size=1000000; # Rotate log files at 1MB
SET GLOBAL server_audit_file_rotate_max_retained_files=10; # Keep 10 log files

-- Configure log events to capture
SET GLOBAL server_audit_events='CONNECT,QUERY';
```

```sql
-- PostgreSQL: Enable and configure logging
# Edit the postgresql.conf file
log_destination = 'csvlog'
logging_collector = on
log_directory = 'pg_log'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_truncate_on_rotation = off
log_rotation_age = 1d
log_rotation_size = 100000 # Rotate log files at 100MB
```
