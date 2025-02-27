---
title: "MariaDB Installation on Windows"
description: "Complete guide to installing, configuring, and securing MariaDB database server on Windows desktop and server platforms"
weight: 1
---

![alt text](/images/os/windows/mariadb.webp) 

# MariaDB Installation and Configuration Guide for Windows

This comprehensive guide covers installing, configuring, and managing MariaDB database server specifically for Windows desktop and server environments.

## Table of Contents

- [System Requirements](#system-requirements)
- [Installation Process](#installation-process)
- [Initial Configuration](#initial-configuration)
- [Security Hardening](#security-hardening)
- [Performance Tuning](#performance-tuning)
- [Basic Administration](#basic-administration)
- [Troubleshooting](#troubleshooting)
- [Advanced Configuration](#advanced-configuration)

## System Requirements

### Minimum Requirements

- Windows 10/11 (64-bit) or Windows Server 2016/2019/2022
- 1GB RAM (4GB recommended for production)
- 1GB free disk space
- Administrative privileges

### Supported Windows Versions

| Windows Version | Support Level |
|-----------------|--------------|
| Windows 11 | Fully supported |
| Windows 10 | Fully supported |
| Windows Server 2022 | Fully supported |
| Windows Server 2019 | Fully supported |
| Windows Server 2016 | Fully supported |
| Windows 8.1 | Limited support |
| Windows Server 2012 R2 | Limited support |

## Installation Process

### Step 1: Download the Installer

1. Visit the [MariaDB Downloads page](https://mariadb.org/download/)
2. Select "Windows" as the platform
3. Choose the latest stable MSI package (e.g., MariaDB 10.11.x)
4. Select either x86_64 (64-bit) or x86 (32-bit) depending on your system
5. Download the MSI installer package

### Step 2: Run the Installer

1. Right-click the downloaded MSI file
2. Select "Run as administrator"
3. When the installation wizard appears, click "Next"

### Step 3: Accept License Agreement

1. Read the license agreement
2. Select "I accept the terms in the License Agreement"
3. Click "Next"

### Step 4: Choose Setup Type

1. Select one of the following:
   - "Typical" for standard installation (recommended for most users)
   - "Complete" to install all components
   - "Custom" to select specific components and installation location
2. Click "Next"

### Step 5: Set Root Password

1. Enter a strong password for the root user
   - Use a combination of uppercase, lowercase, numbers, and special characters
   - Minimum 12 characters recommended
2. **IMPORTANT**: Record this password securely
3. Optionally check "Use UTF8 as default server's character set" (recommended)
4. Click "Next"

### Step 6: Configure Service Settings

1. Ensure "Install as service" is checked (recommended)
   - Service Name: MariaDB (default)
2. Check "Enable networking" if you need remote connections
   - Port: 3306 (default)
3. Check "Start service after install" (recommended)
4. Click "Next"

### Step 7: Advanced Options

1. Optionally modify the data directory location
   - Default is C:\Program Files\MariaDB x.x\data
   - You may choose a different drive with more space for production servers
2. Click "Next"

### Step 8: Complete Installation

1. Click "Install" to begin the installation process
2. Wait for the installation to complete
3. Click "Finish"

## Initial Configuration

### Testing the Installation

1. Open Command Prompt as Administrator
2. Connect to MariaDB:
   ```cmd
   "C:\Program Files\MariaDB 10.11\bin\mysql.exe" -u root -p
   ```
3. Enter the root password when prompted
4. If you see the MariaDB prompt (`MariaDB [(none)]>`), the installation was successful
5. Test with a simple query:
   ```sql
   SHOW DATABASES;
   ```

### Configuration File Location

The main configuration file is located at:
- `C:\Program Files\MariaDB 10.11\data\my.ini`

Make a backup before editing:
```cmd
copy "C:\Program Files\MariaDB 10.11\data\my.ini" "C:\Program Files\MariaDB 10.11\data\my.ini.bak"
```

### Creating Your First Database

```sql
-- Create a new database
CREATE DATABASE myproject CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Create a new user
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'Strong_Password_123';

-- Grant privileges to the user
GRANT ALL PRIVILEGES ON myproject.* TO 'myuser'@'localhost';
FLUSH PRIVILEGES;

-- Verify the new database
SHOW DATABASES;

-- Switch to the new database
USE myproject;
```

### Service Management

You can manage the MariaDB service using:

1. **Services Management Console**:
   - Press Win+R, type `services.msc`, press Enter
   - Find "MariaDB" in the list
   - Right-click and select Start, Stop, or Restart

2. **Command Prompt** (as Administrator):
   ```cmd
   net start MariaDB
   net stop MariaDB
   ```

3. **PowerShell** (as Administrator):
   ```powershell
   Start-Service MariaDB
   Stop-Service MariaDB
   Restart-Service MariaDB
   Get-Service MariaDB
   ```

## Security Hardening

### Securing MariaDB on Windows

1. **Run the Security Script**:
   ```cmd
   "C:\Program Files\MariaDB 10.11\bin\mysql_secure_installation.exe"
   ```
   This will help you:
   - Remove anonymous users
   - Disallow root login remotely
   - Remove test database
   - Reload privilege tables

2. **Firewall Configuration**:
   - Open Windows Defender Firewall with Advanced Security
   - Create a new Inbound Rule:
     - Rule Type: Port
     - Protocol: TCP
     - Port: 3306
     - Action: Allow
     - Profile: Domain, Private (uncheck Public)
     - Name: "MariaDB Server"

3. **Create Limited Privilege Users**:
   ```sql
   -- Application user with limited privileges
   CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'Strong_App_Pwd_123';
   GRANT SELECT, INSERT, UPDATE, DELETE ON myproject.* TO 'appuser'@'localhost';
   
   -- Read-only user
   CREATE USER 'reporter'@'localhost' IDENTIFIED BY 'Strong_Report_Pwd_456';
   GRANT SELECT ON myproject.* TO 'reporter'@'localhost';
   
   -- Apply changes
   FLUSH PRIVILEGES;
   ```

4. **Limiting Network Access**:
   
   Edit `my.ini` and add or modify:
   ```ini
   [mysqld]
   # Bind to localhost only
   bind-address = 127.0.0.1
   ```

### Enabling SSL/TLS

1. **Generate SSL Certificates**:
   ```cmd
   cd "C:\Program Files\MariaDB 10.11\data"
   "C:\Program Files\MariaDB 10.11\bin\openssl.exe" genrsa 2048 > ca-key.pem
   "C:\Program Files\MariaDB 10.11\bin\openssl.exe" req -new -x509 -nodes -days 3650 -key ca-key.pem -out ca-cert.pem
   "C:\Program Files\MariaDB 10.11\bin\openssl.exe" req -newkey rsa:2048 -days 3650 -nodes -keyout server-key.pem -out server-req.pem
   "C:\Program Files\MariaDB 10.11\bin\openssl.exe" x509 -req -in server-req.pem -days 3650 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out server-cert.pem
   ```

2. **Configure SSL in my.ini**:
   ```ini
   [mysqld]
   ssl-ca=C:/Program Files/MariaDB 10.11/data/ca-cert.pem
   ssl-cert=C:/Program Files/MariaDB 10.11/data/server-cert.pem
   ssl-key=C:/Program Files/MariaDB 10.11/data/server-key.pem
   ```

3. **Require SSL for Users**:
   ```sql
   ALTER USER 'username'@'%' REQUIRE SSL;
   ```

## Performance Tuning

### Windows-Specific Optimizations

Edit the `my.ini` file with these recommended settings:

```ini
[mysqld]
# Memory Settings
innodb_buffer_pool_size = 1G         # 50% of RAM for dedicated servers
innodb_log_file_size = 256M          # Larger for write-heavy workloads

# Windows-Specific
innodb_flush_method = normal         # Windows doesn't support O_DIRECT
innodb_file_per_table = 1            # Separate file for each table

# InnoDB Settings
innodb_io_capacity = 1000            # For SSDs, lower for HDDs
innodb_flush_log_at_trx_commit = 1   # Safe setting, use 2 for better performance

# Connection Settings
max_connections = 100                # Adjust based on your application needs
table_open_cache = 2000              # Increase for many tables
table_definition_cache = 1400
```

### Performance Settings by Server Type

#### For Development Machines
```ini
[mysqld]
innodb_buffer_pool_size = 512M
max_connections = 50
table_open_cache = 400
```

#### For Production Servers (8GB RAM)
```ini
[mysqld]
innodb_buffer_pool_size = 4G
innodb_log_file_size = 512M
max_connections = 200
table_open_cache = 4000
```

#### For Dedicated Database Servers (16GB+ RAM)
```ini
[mysqld]
innodb_buffer_pool_size = 8G
innodb_log_file_size = 1G
innodb_buffer_pool_instances = 8
max_connections = 500
table_open_cache = 8000
```

## Basic Administration

### Backup and Restore

**Creating Backups**:

1. **Command Line Backup**:
   ```cmd
   "C:\Program Files\MariaDB 10.11\bin\mysqldump.exe" -u root -p --single-transaction --routines --triggers --events mydatabase > C:\backups\mydatabase.sql
   ```

2. **Scheduled Backups**:
   Create a batch file `backup.bat`:
   ```batch
   @echo off
   set BACKUP_DIR=C:\backups
   set DATE_FORMAT=%date:~-4,4%%date:~-10,2%%date:~-7,2%
   "C:\Program Files\MariaDB 10.11\bin\mysqldump.exe" -u root -p[password] --single-transaction --routines --triggers --events --all-databases > %BACKUP_DIR%\mariadb_backup_%DATE_FORMAT%.sql
   ```
   
   Then create a scheduled task in Windows Task Scheduler.

**Restoring Backups**:

```cmd
"C:\Program Files\MariaDB 10.11\bin\mysql.exe" -u root -p mydatabase < C:\backups\mydatabase.sql
```

### User Management

```sql
-- List all users
SELECT user, host FROM mysql.user;

-- Create new user
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

-- Grant privileges
GRANT ALL PRIVILEGES ON database.* TO 'username'@'localhost';

-- Change password
ALTER USER 'username'@'localhost' IDENTIFIED BY 'new_password';

-- Revoke privileges
REVOKE ALL PRIVILEGES ON database.* FROM 'username'@'localhost';

-- Delete user
DROP USER 'username'@'localhost';
```

### Database Operations

```sql
-- Create database
CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Show all databases
SHOW DATABASES;

-- Select a database
USE mydatabase;

-- Create a table
CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- List all tables
SHOW TABLES;

-- View table structure
DESCRIBE customers;

-- Drop a database
DROP DATABASE mydatabase;
```

## Troubleshooting

### Common Issues on Windows

#### Service Won't Start

1. **Check Error Logs**:
   - Look in `C:\Program Files\MariaDB 10.11\data\COMPUTERNAME.err`

2. **Check Windows Event Viewer**:
   - Press Win+R, type `eventvwr`, press Enter
   - Navigate to Windows Logs > Application
   - Look for events from source "MariaDB"

3. **Port Conflict**:
   - Check if port 3306 is already in use:
     ```cmd
     netstat -ano | findstr 3306
     ```
   - If in use, edit `my.ini` and change the port number

4. **Insufficient Permissions**:
   - Ensure the service account has proper permissions to the data directory
   - Right-click the MariaDB data folder, go to Properties > Security

#### Connection Issues

1. **Cannot connect with root from another computer**:
   - By default, root can only connect from localhost
   - Create a new admin user for remote connections:
     ```sql
     CREATE USER 'admin'@'%' IDENTIFIED BY 'StrongPassword';
     GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';
     FLUSH PRIVILEGES;
     ```

2. **Access denied errors**:
   - Check username, password, and hostname
   - Verify user has correct privileges:
     ```sql
     SHOW GRANTS FOR 'username'@'hostname';
     ```

3. **Windows firewall blocking**:
   - Check Windows Firewall settings
   - Verify MariaDB has an inbound rule for port 3306

### Fixing Corrupted Data

```cmd
REM Stop the MariaDB service
net stop MariaDB

REM Run myisamchk on all tables (for MyISAM tables)
"C:\Program Files\MariaDB 10.11\bin\myisamchk.exe" -r "C:\Program Files\MariaDB 10.11\data\database\*.MYI"

REM For InnoDB recovery, modify my.ini and add:
REM [mysqld]
REM innodb_force_recovery = 1

REM Start the service
net start MariaDB
```

## Advanced Configuration

### Creating Windows Services for Multiple Instances

To run multiple MariaDB instances on one Windows server:

1. **Install the first instance normally**

2. **Create a second instance**:
   - Create new data and configuration directories:
     ```cmd
     mkdir C:\MariaDB-Second\data
     mkdir C:\MariaDB-Second\etc
     ```
   
   - Copy and modify configuration:
     ```cmd
     copy "C:\Program Files\MariaDB 10.11\data\my.ini" "C:\MariaDB-Second\etc\my.ini"
     ```
   
   - Edit `C:\MariaDB-Second\etc\my.ini`:
     ```ini
     [mysqld]
     datadir=C:/MariaDB-Second/data
     port=3307  # Different port
     socket=MySQL2
     
     [client]
     port=3307
     socket=MySQL2
     ```
   
   - Create the service:
     ```cmd
     "C:\Program Files\MariaDB 10.11\bin\mysqld.exe" --install-manual MariaDB2 --defaults-file=C:\MariaDB-Second\etc\my.ini
     ```

3. **Initialize and start the second instance**:
   ```cmd
   "C:\Program Files\MariaDB 10.11\bin\mysql_install_db.exe" --datadir=C:\MariaDB-Second\data
   net start MariaDB2
   ```

### Integrating with Windows Authentication

MariaDB on Windows can be configured to use Windows Authentication (NTLM):

1. **Enable the plugin**:
   Edit `my.ini`:
   ```ini
   [mysqld]
   plugin-load-add=auth_windows.dll
   ```

2. **Restart the service**:
   ```cmd
   net stop MariaDB
   net start MariaDB
   ```

3. **Create users with Windows authentication**:
   ```sql
   CREATE USER 'DOMAIN\\username'@'localhost' IDENTIFIED WITH auth_windows;
   GRANT ALL PRIVILEGES ON *.* TO 'DOMAIN\\username'@'localhost';
   ```

4. **Connect using Windows authentication**:
   ```cmd
   "C:\Program Files\MariaDB 10.11\bin\mysql.exe" --default-auth=auth_windows
   ```

## Resources

- [Official MariaDB Documentation](https://mariadb.com/kb/en/documentation/)
- [MariaDB Windows-Specific Documentation](https://mariadb.com/kb/en/installing-mariadb-on-windows/)
- [MariaDB Server GitHub](https://github.com/MariaDB/server)
- [Windows Performance Tuning Guide](https://mariadb.com/kb/en/optimizing-mariadb-for-windows/)

---

This guide covers the essentials of installing, configuring, and managing MariaDB on Windows platforms. For advanced topics like replication, clustering, or enterprise features, please refer to the official documentation.
