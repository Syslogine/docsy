---
title: "PHP Development Guide for Windows 11 Enterprise"
description: "Complete guide for setting up and using PHP in Windows 11 Enterprise environments"
date: 2025-09-15
weight: 10
draft: false
toc: true
tags: ["php", "windows", "enterprise", "development", "iis", "apache"]
categories: ["Development", "Windows", "Web Development"]
---

# PHP Development Guide for Windows 11 Enterprise

## Overview

This comprehensive guide covers the complete process of installing, configuring, and using PHP in Windows 11 Enterprise environments. From basic installation to advanced web server configurations, this documentation will help system administrators and developers establish robust PHP development environments.

## Prerequisites

- Windows 11 Enterprise (build 22000 or higher)
- Administrator privileges for system-wide installation
- Minimum 4GB free disk space
- Internet connectivity for downloads
- Corporate network access (if behind proxy/firewall)

## Installation Methods

### Method 1: Official PHP Downloads (Recommended)

The official PHP builds provide the most flexibility and are ideal for enterprise environments.

**Download PHP:**
1. Visit [https://windows.php.net/download/](https://windows.php.net/download/)
2. Choose the latest stable version (PHP 8.2+ recommended)
3. Select **Thread Safe** version for Apache or **Non Thread Safe** for IIS/FastCGI

**Installation steps:**
```cmd
# Create PHP directory
mkdir C:\php

# Extract downloaded ZIP to C:\php
# Add C:\php to system PATH
```

**Add to PATH:**
```powershell
# Temporary (current session)
$env:PATH += ";C:\php"

# Permanent (system-wide, run as Administrator)
[Environment]::SetEnvironmentVariable("Path", $env:PATH + ";C:\php", "Machine")
```

**Verify installation:**
```cmd
php --version
php -m  # List loaded modules
php --ini  # Show configuration file locations
```

### Method 2: Chocolatey Package Manager

Ideal for automated deployments and package management.

```powershell
# Install Chocolatey first (if not present)
# Run PowerShell as Administrator
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install PHP
choco install php --version=8.2.12

# Verify installation
php --version
```

### Method 3: Windows Package Manager (winget)

```powershell
# Search for available PHP packages
winget search php

# Install PHP
winget install shivammathur.php

# Verify installation
php --version
```

### Method 4: XAMPP (Development Environment)

For quick development setup with Apache, MySQL, and phpMyAdmin.

```powershell
# Via Chocolatey
choco install xampp-81

# Or via winget
winget install ApacheFriends.Xampp.8.2

# Or download from https://www.apachefriends.org/
```

## Web Server Configuration

### IIS Configuration (Recommended for Enterprise)

Internet Information Services (IIS) is the preferred web server for Windows enterprise environments.

#### Enable IIS Features

```powershell
# Run as Administrator
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerRole
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServer
Enable-WindowsOptionalFeature -Online -FeatureName IIS-CommonHttpFeatures
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpErrors
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpLogging
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpRedirect
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ApplicationDevelopment
Enable-WindowsOptionalFeature -Online -FeatureName IIS-NetFxExtensibility45
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HealthAndDiagnostics
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpCompressionStatic
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Security
Enable-WindowsOptionalFeature -Online -FeatureName IIS-RequestFiltering
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Performance
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerManagementTools
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementConsole
Enable-WindowsOptionalFeature -Online -FeatureName IIS-IIS6ManagementCompatibility
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Metabase
Enable-WindowsOptionalFeature -Online -FeatureName IIS-CGI
```

#### Install PHP Manager for IIS

```powershell
# Download PHP Manager for IIS from Microsoft
# https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10
```

#### Configure PHP with IIS

1. **Open IIS Manager**
   - Windows + R → `inetmgr`

2. **Add PHP as FastCGI Module**
   - Select server node
   - Double-click "FastCGI Settings"
   - Click "Add Application..."
   - Set Full Path: `C:\php\php-cgi.exe`
   - Set Arguments: (leave empty)
   - Click OK

3. **Add Handler Mapping**
   - Select website or application
   - Double-click "Handler Mappings"
   - Click "Add Module Mapping..."
   - Request path: `*.php`
   - Module: `FastCgiModule`
   - Executable: `C:\php\php-cgi.exe`
   - Name: `PHP_via_FastCGI`

#### IIS web.config for PHP

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <handlers>
            <remove name="PHP_via_FastCGI" />
            <add name="PHP_via_FastCGI" 
                 path="*.php" 
                 verb="GET,HEAD,POST" 
                 modules="FastCgiModule" 
                 scriptProcessor="C:\php\php-cgi.exe" 
                 resourceType="Either" 
                 requireAccess="Script" />
        </handlers>
        <defaultDocument>
            <files>
                <remove name="index.php" />
                <add value="index.php" />
            </files>
        </defaultDocument>
        <rewrite>
            <rules>
                <rule name="Pretty URLs" stopProcessing="true">
                    <match url="^(.*)$" />
                    <conditions>
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php/{R:1}" />
                </rule>
            </rules>
        </rewrite>
        <security>
            <requestFiltering>
                <fileExtensions>
                    <remove fileExtension=".php" />
                    <add fileExtension=".php" allowed="true" />
                </fileExtensions>
            </requestFiltering>
        </security>
    </system.webServer>
</configuration>
```

### Apache HTTP Server Configuration

For development environments or when Apache is preferred.

#### Install Apache

```powershell
# Via Chocolatey
choco install apache-httpd

# Or download from https://httpd.apache.org/download.cgi
```

#### Configure Apache with PHP

**httpd.conf modifications:**
```apache
# Load PHP module
LoadModule php_module "C:/php/php8apache2_4.dll"

# Add PHP handler
<FilesMatch \.php$>
    SetHandler application/x-httpd-php
</FilesMatch>

# Set PHP configuration file location
PHPIniDir "C:/php"

# Add index.php to directory index
<IfModule dir_module>
    DirectoryIndex index.html index.php
</IfModule>

# Configure PHP file handling
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```

**Virtual Host configuration:**
```apache
<VirtualHost *:80>
    DocumentRoot "C:/www/myproject"
    ServerName myproject.local
    ServerAlias www.myproject.local
    
    <Directory "C:/www/myproject">
        AllowOverride All
        Require local
    </Directory>
    
    ErrorLog "logs/myproject_error.log"
    CustomLog "logs/myproject_access.log" common
</VirtualHost>

<VirtualHost *:443>
    DocumentRoot "C:/www/myproject"
    ServerName myproject.local
    
    SSLEngine on
    SSLCertificateFile "conf/ssl/myproject.crt"
    SSLCertificateKeyFile "conf/ssl/myproject.key"
    
    <Directory "C:/www/myproject">
        AllowOverride All
        Require local
    </Directory>
</VirtualHost>
```

#### .htaccess for Pretty URLs

```apache
RewriteEngine On

# Handle Angular and other frontend routes
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [QSA,L]

# Security headers
Header always set X-Content-Type-Options nosniff
Header always set X-Frame-Options DENY
Header always set X-XSS-Protection "1; mode=block"
Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set Content-Security-Policy "default-src 'self'"

# Cache static files
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType text/css "access plus 1 year"
    ExpiresByType application/javascript "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType image/jpg "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/gif "access plus 1 year"
    ExpiresByType image/svg+xml "access plus 1 year"
</IfModule>
```

## PHP Configuration

### php.ini Configuration

**Basic production configuration** (`C:\php\php.ini`):
```ini
[PHP]
; Engine Settings
engine = On
short_open_tag = Off
precision = 14
output_buffering = 4096
zlib.output_compression = Off
implicit_flush = Off
serialize_precision = -1

; Error Handling
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = Off
display_startup_errors = Off
log_errors = On
error_log = "C:\php\logs\php_errors.log"

; Data Handling
post_max_size = 32M
auto_globals_jit = On
auto_prepend_file =
auto_append_file =
default_mimetype = "text/html"
default_charset = "UTF-8"

; File Uploads
file_uploads = On
upload_max_filesize = 32M
max_file_uploads = 20

; Fopen wrappers
allow_url_fopen = On
allow_url_include = Off

; Dynamic Extensions
extension_dir = "C:\php\ext"

; Core Extensions (uncomment as needed)
extension=curl
extension=fileinfo
extension=gd
extension=intl
extension=mbstring
extension=openssl
extension=pdo_mysql
extension=pdo_sqlite
extension=pdo_pgsql
extension=redis
extension=zip

; Session Configuration
session.save_handler = files
session.save_path = "C:\php\sessions"
session.use_strict_mode = 1
session.use_cookies = 1
session.use_only_cookies = 1
session.name = PHPSESSID
session.auto_start = 0
session.cookie_lifetime = 0
session.cookie_path = /
session.cookie_domain =
session.cookie_httponly = 1
session.cookie_secure = 1
session.cookie_samesite = "Strict"
session.serialize_handler = php

; Security
expose_php = Off
max_execution_time = 60
max_input_time = 60
memory_limit = 256M

; Date/Time
date.timezone = "UTC"

; OPcache (recommended for production)
[opcache]
opcache.enable = 1
opcache.enable_cli = 1
opcache.memory_consumption = 128
opcache.interned_strings_buffer = 8
opcache.max_accelerated_files = 4000
opcache.revalidate_freq = 2
opcache.fast_shutdown = 1
opcache.validate_timestamps = 1
```

**Development configuration differences:**
```ini
; Development overrides
error_reporting = E_ALL
display_errors = On
display_startup_errors = On
log_errors = On

; Disable OPcache for development
opcache.enable = 0
opcache.validate_timestamps = 1
opcache.revalidate_freq = 0

; Extended memory for debugging
memory_limit = 512M
max_execution_time = 300

; XDebug configuration (if installed)
[xdebug]
xdebug.mode = debug
xdebug.start_with_request = yes
xdebug.client_host = localhost
xdebug.client_port = 9003
```

### Create Required Directories

```cmd
mkdir C:\php\logs
mkdir C:\php\sessions
mkdir C:\php\uploads

# Set appropriate permissions
icacls C:\php\logs /grant "IIS_IUSRS:(OI)(CI)F"
icacls C:\php\sessions /grant "IIS_IUSRS:(OI)(CI)F"
icacls C:\php\uploads /grant "IIS_IUSRS:(OI)(CI)F"
```

## Composer Package Management

### Install Composer

```powershell
# Method 1: Download installer
# Visit https://getcomposer.org/download/
# Run Composer-Setup.exe

# Method 2: Via Chocolatey
choco install composer

# Method 3: Via winget
winget install Composer.Composer

# Verify installation
composer --version
composer diagnose
```

### Global Composer Configuration

**composer.json for global packages:**
```json
{
    "require": {
        "laravel/installer": "^4.0",
        "symfony/console": "^6.0",
        "phpunit/phpunit": "^10.0",
        "squizlabs/php_codesniffer": "^3.7",
        "friendsofphp/php-cs-fixer": "^3.0",
        "phpstan/phpstan": "^1.0"
    }
}
```

**Install global packages:**
```cmd
composer global require laravel/installer
composer global require phpunit/phpunit
composer global require squizlabs/php_codesniffer
composer global require friendsofphp/php-cs-fixer
composer global require phpstan/phpstan

# Add Composer global bin to PATH
# %APPDATA%\Composer\vendor\bin
```

### Corporate Proxy Configuration

**Configure Composer for corporate proxy:**
```cmd
# Set proxy globally
composer config -g repos.packagist composer https://packagist.org
composer config -g http-basic.packagist.org username password

# Set HTTP proxy
composer config -g http-proxy http://proxy.company.com:8080

# Set HTTPS proxy
composer config -g https-proxy https://proxy.company.com:8080

# Configure authentication for private repositories
composer config -g http-basic.private-repo.com username token
```

**composer.json with corporate repository:**
```json
{
    "repositories": [
        {
            "type": "composer",
            "url": "https://repo.company.com/packages/"
        },
        {
            "type": "vcs",
            "url": "https://github.com/company/private-package"
        }
    ],
    "require": {
        "company/private-package": "^1.0",
        "monolog/monolog": "^3.0",
        "guzzlehttp/guzzle": "^7.0"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.0",
        "mockery/mockery": "^1.5"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/",
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "test": "phpunit",
        "cs-fix": "php-cs-fixer fix",
        "analyse": "phpstan analyse src"
    },
    "config": {
        "optimize-autoloader": true,
        "sort-packages": true,
        "allow-plugins": {
            "composer/package-versions-deprecated": true
        }
    }
}
```

## Development Tools

### Code Editors and IDEs

#### PhpStorm (Recommended)

```powershell
# Install via winget
winget install JetBrains.PhpStorm

# Or via Chocolatey
choco install phpstorm
```

**PhpStorm configuration for Windows:**
- Set PHP interpreter: `C:\php\php.exe`
- Configure Composer: `C:\ProgramData\ComposerSetup\bin\composer.bat`
- Set up XDebug for debugging
- Configure code style (PSR-12)

#### Visual Studio Code

```powershell
winget install Microsoft.VisualStudioCode
```

**Essential PHP extensions for VS Code:**
```json
{
    "recommendations": [
        "bmewburn.vscode-intelephense-client",
        "xdebug.php-debug",
        "junstyle.php-cs-fixer",
        "recca0120.vscode-phpunit",
        "neilbrayfield.php-docblocker",
        "onecentlin.laravel-blade",
        "bradlc.vscode-tailwindcss"
    ]
}
```

**VS Code settings.json for PHP:**
```json
{
    "php.validate.executablePath": "C:\\php\\php.exe",
    "php.executablePath": "C:\\php\\php.exe",
    "intelephense.environment.phpVersion": "8.2.0",
    "intelephense.files.maxSize": 5000000,
    "editor.formatOnSave": true,
    "php-cs-fixer.executablePath": "${extensionPath}\\php-cs-fixer.phar",
    "php-cs-fixer.rules": "@PSR12",
    "phpunit.php": "C:\\php\\php.exe",
    "phpunit.phpunit": ".\\vendor\\bin\\phpunit.bat"
}
```

### XDebug Configuration

**Install XDebug:**
```cmd
# Download from https://xdebug.org/download
# Copy php_xdebug.dll to C:\php\ext\

# Add to php.ini
zend_extension=xdebug

[xdebug]
xdebug.mode = debug
xdebug.start_with_request = yes
xdebug.client_host = localhost
xdebug.client_port = 9003
xdebug.log = "C:\php\logs\xdebug.log"
xdebug.idekey = PHPSTORM
xdebug.max_nesting_level = 512
```

**VS Code launch.json for XDebug:**
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}"
            }
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9003,
            "runtimeArgs": [
                "-dxdebug.start_with_request=yes"
            ]
        }
    ]
}
```

### Testing Framework Setup

#### PHPUnit

**Install PHPUnit:**
```cmd
composer require --dev phpunit/phpunit
```

**phpunit.xml configuration:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="https://schema.phpunit.de/10.0/phpunit.xsd"
         bootstrap="vendor/autoload.php"
         colors="true"
         processIsolation="false"
         stopOnFailure="false"
         executionOrder="random"
         failOnWarning="true"
         failOnRisky="true"
         failOnEmptyTestSuite="true"
         beStrictAboutOutputDuringTests="true"
         cacheDirectory=".phpunit.cache"
         backupStaticProperties="false">
    
    <testsuites>
        <testsuite name="Unit">
            <directory suffix="Test.php">./tests/Unit</directory>
        </testsuite>
        <testsuite name="Feature">
            <directory suffix="Test.php">./tests/Feature</directory>
        </testsuite>
    </testsuites>
    
    <coverage>
        <include>
            <directory suffix=".php">./src</directory>
        </include>
        <exclude>
            <directory>./src/Config</directory>
            <file>./src/bootstrap.php</file>
        </exclude>
        <report>
            <html outputDirectory="./coverage-html"/>
            <clover outputFile="./coverage.xml"/>
        </report>
    </coverage>
    
    <logging>
        <junit outputFile="./tests-results.xml"/>
    </logging>
</phpunit>
```

**Example test:**
```php
<?php

namespace Tests\Unit;

use PHPUnit\Framework\TestCase;
use App\Calculator;

class CalculatorTest extends TestCase
{
    private Calculator $calculator;
    
    protected function setUp(): void
    {
        $this->calculator = new Calculator();
    }
    
    public function testAddition(): void
    {
        $result = $this->calculator->add(2, 3);
        $this->assertEquals(5, $result);
    }
    
    public function testDivisionByZero(): void
    {
        $this->expectException(\InvalidArgumentException::class);
        $this->calculator->divide(10, 0);
    }
    
    /**
     * @dataProvider additionProvider
     */
    public function testAdditionWithDataProvider($a, $b, $expected): void
    {
        $result = $this->calculator->add($a, $b);
        $this->assertEquals($expected, $result);
    }
    
    public static function additionProvider(): array
    {
        return [
            [1, 2, 3],
            [5, 5, 10],
            [-1, 1, 0],
            [0, 0, 0]
        ];
    }
}
```

## Database Configuration

### MySQL Configuration

**Install MySQL:**
```powershell
# Via Chocolatey
choco install mysql

# Or download from https://dev.mysql.com/downloads/mysql/
```

**PHP MySQL extension configuration:**
```ini
; Enable in php.ini
extension=pdo_mysql
extension=mysqli

; MySQL connection settings
mysql.default_host = localhost
mysql.default_user = 
mysql.default_password = 
mysql.default_port = 3306
```

**PDO connection example:**
```php
<?php

class Database
{
    private static ?PDO $connection = null;
    
    public static function getConnection(): PDO
    {
        if (self::$connection === null) {
            $dsn = "mysql:host=localhost;dbname=myapp;charset=utf8mb4";
            $options = [
                PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
                PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
                PDO::ATTR_EMULATE_PREPARES => false,
                PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci"
            ];
            
            self::$connection = new PDO($dsn, 'username', 'password', $options);
        }
        
        return self::$connection;
    }
}

// Usage
$pdo = Database::getConnection();
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?");
$stmt->execute([$email]);
$user = $stmt->fetch();
```

### SQL Server Configuration

**Install SQL Server drivers:**
```cmd
# Download Microsoft Drivers for PHP for SQL Server
# https://docs.microsoft.com/en-us/sql/connect/php/download-drivers-php-sql-server

# Copy php_sqlsrv.dll and php_pdo_sqlsrv.dll to C:\php\ext\
```

**Enable in php.ini:**
```ini
extension=sqlsrv
extension=pdo_sqlsrv
```

**SQL Server connection example:**
```php
<?php

class SqlServerDatabase
{
    private static ?PDO $connection = null;
    
    public static function getConnection(): PDO
    {
        if (self::$connection === null) {
            $serverName = "localhost\\SQLEXPRESS";
            $database = "MyDatabase";
            
            // Windows Authentication
            $dsn = "sqlsrv:Server={$serverName};Database={$database}";
            
            // SQL Server Authentication
            // $dsn = "sqlsrv:Server={$serverName};Database={$database}";
            // $username = "sa";
            // $password = "password";
            
            $options = [
                PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
                PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC
            ];
            
            self::$connection = new PDO($dsn, $username ?? '', $password ?? '', $options);
        }
        
        return self::$connection;
    }
}
```

## Enterprise Security

### SSL/TLS Configuration

**Generate self-signed certificate for development:**
```cmd
# Create certificate directory
mkdir C:\certificates

# Generate private key and certificate (requires OpenSSL)
openssl req -x509 -newkey rsa:4096 -keyout C:\certificates\localhost.key -out C:\certificates\localhost.crt -days 365 -nodes -subj "/CN=localhost"
```

**IIS SSL configuration:**
1. Open IIS Manager
2. Select server node
3. Double-click "Server Certificates"
4. Click "Import..." in Actions panel
5. Select certificate file
6. Select website
7. Click "Bindings..." in Actions panel
8. Add HTTPS binding with certificate

### Authentication and Authorization

**Windows Authentication with IIS:**
```xml
<!-- web.config -->
<system.webServer>
    <security>
        <authentication>
            <windowsAuthentication enabled="true" />
            <anonymousAuthentication enabled="false" />
        </authentication>
        <authorization>
            <add accessType="Allow" users="DOMAIN\user1,DOMAIN\user2" />
            <add accessType="Deny" users="*" />
        </authorization>
    </security>
</system.webServer>
```

**PHP Windows Authentication:**
```php
<?php

class WindowsAuth
{
    public static function getCurrentUser(): ?string
    {
        // Get Windows authenticated user
        if (isset($_SERVER['AUTH_USER'])) {
            return $_SERVER['AUTH_USER'];
        }
        
        if (isset($_SERVER['REMOTE_USER'])) {
            return $_SERVER['REMOTE_USER'];
        }
        
        return null;
    }
    
    public static function isUserInGroup(string $user, string $group): bool
    {
        // Check if user is in specific Windows group
        // This requires additional LDAP or COM extensions
        return false; // Implement based on requirements
    }
}

// Usage
$currentUser = WindowsAuth::getCurrentUser();
if ($currentUser) {
    echo "Authenticated as: " . $currentUser;
} else {
    http_response_code(401);
    echo "Authentication required";
}
```

### Input Validation and Security

**Security configuration:**
```php
<?php

class SecurityHelper
{
    public static function sanitizeInput(string $input): string
    {
        // Remove null bytes
        $input = str_replace(chr(0), '', $input);
        
        // Trim whitespace
        $input = trim($input);
        
        // Convert special characters
        return htmlspecialchars($input, ENT_QUOTES | ENT_HTML5, 'UTF-8');
    }
    
    public static function validateEmail(string $email): bool
    {
        return filter_var($email, FILTER_VALIDATE_EMAIL) !== false;
    }
    
    public static function generateCsrfToken(): string
    {
        if (!isset($_SESSION['csrf_token'])) {
            $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
        }
        
        return $_SESSION['csrf_token'];
    }
    
    public static function validateCsrfToken(string $token): bool
    {
        return isset($_SESSION['csrf_token']) && 
               hash_equals($_SESSION['csrf_token'], $token);
    }
    
    public static function hashPassword(string $password): string
    {
        return password_hash($password, PASSWORD_ARGON2ID, [
            'memory_cost' => 65536,
            'time_cost' => 4,
            'threads' => 3
        ]);
    }
    
    public static function verifyPassword(string $password, string $hash): bool
    {
        return password_verify($password, $hash);
    }
}
```

## Performance Optimization

### OPcache Configuration

**Optimal OPcache settings:**
```ini
[opcache]
; Enable OPcache
opcache.enable = 1
opcache.enable_cli = 1

; Memory settings
opcache.memory_consumption = 256
opcache.interned_strings_buffer = 16
opcache.max_accelerated_files = 20000

; Validation settings
opcache.validate_timestamps = 0  ; Disable for production
opcache.revalidate_freq = 0

; Optimization settings
opcache.save_comments = 0
opcache.fast_shutdown = 1
opcache.enable_file_override = 1

; JIT compilation (PHP 8.0+)
opcache.jit_buffer_size = 100M
opcache.jit = tracing
```

**OPcache monitoring script:**
```php
<?php

function getOpcacheStatus(): array
{
    if (!extension_loaded('Zend OPcache')) {
        return ['error' => 'OPcache not loaded'];
    }
    
    $status = opcache_get_status(false);
    $config = opcache_get_configuration();
    
    return [
        'enabled' => $status['opcache_enabled'],
        'memory_usage' => $status['memory_usage'],
        'hit_rate' => round($status['opcache_statistics']['opcache_hit_rate'], 2),
        'cached_files' => $status['opcache_statistics']['num_cached_scripts'],
        'max_cached_files' => $config['directives']['opcache.max_accelerated_files'],
        'memory_consumption' => $config['directives']['opcache.memory_consumption'],
        'free_memory' => $status['memory_usage']['free_memory'],
        'used_memory' => $status['memory_usage']['used_memory'],
        'wasted_memory' => $status['memory_usage']['wasted_memory']
    ];
}

// Display OPcache status
$opcache = getOpcacheStatus();
echo "<h2>OPcache Status</h2>";
echo "<pre>" . print_r($opcache, true) . "</pre>";

// Clear OPcache (use carefully in production)
if (isset($_GET['clear']) && $_GET['clear'] === 'opcache') {
    opcache_reset();
    echo "OPcache cleared!";
}
?>
```

### Caching Strategies

**File-based caching:**
```php
<?php

class FileCache
{
    private string $cacheDir;
    
    public function __construct(string $cacheDir = 'cache')
    {
        $this->cacheDir = rtrim($cacheDir, '/\\') . DIRECTORY_SEPARATOR;
        
        if (!is_dir($this->cacheDir)) {
            mkdir($this->cacheDir, 0755, true);
        }
    }
    
    public function get(string $key): mixed
    {
        $filename = $this->getFilename($key);
        
        if (!file_exists($filename)) {
            return null;
        }
        
        $data = unserialize(file_get_contents($filename));
        
        // Check expiration
        if ($data['expires'] < time()) {
            unlink($filename);
            return null;
        }
        
        return $data['value'];
    }
    
    public function set(string $key, mixed $value, int $ttl = 3600): bool
    {
        $filename = $this->getFilename($key);
        $data = [
            'value' => $value,
            'expires' => time() + $ttl
        ];
        
        return file_put_contents($filename, serialize($data), LOCK_EX) !== false;
    }
    
    public function delete(string $key): bool
    {
        $filename = $this->getFilename($key);
        
        if (file_exists($filename)) {
            return unlink($filename);
        }
        
        return true;
    }
    
    public function clear(): bool
    {
        $files = glob($this->cacheDir . '*.cache');
        
        foreach ($files as $file) {
            unlink($file);
        }
        
        return true;
    }
    
    private function getFilename(string $key): string
    {
        return $this->cacheDir . md5($key) . '.cache';
    }
}

// Usage
$cache = new FileCache('C:/php/cache');

// Store data
$cache->set('user_123', ['name' => 'John', 'email' => 'john@example.com'], 1800);

// Retrieve data
$userData = $cache->get('user_123');
```

**Redis caching (if Redis is available):**
```php
<?php

class RedisCache
{
    private Redis $redis;
    
    public function __construct(string $host = 'localhost', int $port = 6379)
    {
        $this->redis = new Redis();
        $this->redis->connect($host, $port);
    }
    
    public function get(string $key): mixed
    {
        $value = $this->redis->get($key);
        return $value !== false ? unserialize($value) : null;
    }
    
    public function set(string $key, mixed $value, int $ttl = 3600): bool
    {
        return $this->redis->setex($key, $ttl, serialize($value));
    }
    
    public function delete(string $key): bool
    {
        return $this->redis->del($key) > 0;
    }
    
    public function clear(): bool
    {
        return $this->redis->flushDB();
    }
}
```

### Database Optimization

**Connection pooling and optimization:**
```php
<?php

class DatabasePool
{
    private array $connections = [];
    private array $config;
    private int $maxConnections;
    
    public function __construct(array $config, int $maxConnections = 10)
    {
        $this->config = $config;
        $this->maxConnections = $maxConnections;
    }
    
    public function getConnection(): PDO
    {
        // Reuse existing connection if available
        foreach ($this->connections as $key => $connection) {
            if ($this->isConnectionAlive($connection)) {
                unset($this->connections[$key]);
                return $connection;
            }
        }
        
        // Create new connection if under limit
        if (count($this->connections) < $this->maxConnections) {
            return $this->createConnection();
        }
        
        throw new Exception('Maximum connections reached');
    }
    
    public function releaseConnection(PDO $connection): void
    {
        if (count($this->connections) < $this->maxConnections) {
            $this->connections[] = $connection;
        }
    }
    
    private function createConnection(): PDO
    {
        $dsn = sprintf(
            'mysql:host=%s;dbname=%s;charset=utf8mb4',
            $this->config['host'],
            $this->config['database']
        );
        
        $options = [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
            PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
            PDO::ATTR_EMULATE_PREPARES => false,
            PDO::ATTR_PERSISTENT => true,
            PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci"
        ];
        
        return new PDO($dsn, $this->config['username'], $this->config['password'], $options);
    }
    
    private function isConnectionAlive(PDO $connection): bool
    {
        try {
            $connection->query('SELECT 1');
            return true;
        } catch (PDOException $e) {
            return false;
        }
    }
}
```

## Common Issues and Troubleshooting

### PHP Installation Issues

**Problem:** PHP not found in PATH

**Solution:**
```cmd
# Check current PATH
echo %PATH%

# Add PHP to PATH permanently
setx PATH "%PATH%;C:\php" /M

# Verify PHP installation
php --version
where php
```

**Problem:** Extensions not loading

**Solution:**
```ini
; Check php.ini location
php --ini

; Verify extension_dir setting
extension_dir = "C:\php\ext"

; Enable extensions (remove semicolon)
extension=curl
extension=gd
extension=mbstring

; Check if extension file exists
dir C:\php\ext\php_curl.dll
```

### IIS Configuration Issues

**Problem:** HTTP 500 errors with PHP

**Diagnostics:**
```cmd
# Check IIS logs
type C:\inetpub\logs\LogFiles\W3SVC1\*.log

# Check PHP error logs
type C:\php\logs\php_errors.log

# Test PHP CLI
php -v
php -m
```

**Solution:**
1. Verify FastCGI configuration
2. Check file permissions
3. Ensure php-cgi.exe is accessible
4. Validate php.ini settings

**Problem:** File upload issues

**Solution:**
```ini
; Increase upload limits in php.ini
upload_max_filesize = 32M
post_max_size = 32M
memory_limit = 256M
max_execution_time = 60

; Create upload directory
mkdir C:\php\uploads

; Set permissions
icacls C:\php\uploads /grant "IIS_IUSRS:(OI)(CI)F"
```

### Performance Issues

**Problem:** Slow page load times

**Diagnostics:**
```php
<?php
// Enable timing
$startTime = microtime(true);

// Your application code here

$endTime = microtime(true);
$executionTime = ($endTime - $startTime) * 1000; // Convert to milliseconds

echo "Execution time: " . round($executionTime, 2) . " ms";

// Memory usage
echo "Memory usage: " . round(memory_get_usage(true) / 1024 / 1024, 2) . " MB";
echo "Peak memory: " . round(memory_get_peak_usage(true) / 1024 / 1024, 2) . " MB";
?>
```

**Solutions:**
1. Enable OPcache
2. Implement caching
3. Optimize database queries
4. Use connection pooling
5. Enable compression

### Security Issues

**Problem:** Session security

**Solution:**
```php
<?php
// Secure session configuration
ini_set('session.cookie_httponly', 1);
ini_set('session.cookie_secure', 1);
ini_set('session.cookie_samesite', 'Strict');
ini_set('session.use_strict_mode', 1);

// Regenerate session ID
session_start();
session_regenerate_id(true);

// Session timeout
if (isset($_SESSION['last_activity']) && 
    (time() - $_SESSION['last_activity'] > 1800)) {
    session_unset();
    session_destroy();
}
$_SESSION['last_activity'] = time();
?>
```

## Best Practices

### Project Structure

**Standard PHP project layout:**
```
my-php-project/
├── public/
│   ├── index.php
│   ├── .htaccess
│   └── assets/
│       ├── css/
│       ├── js/
│       └── images/
├── src/
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   ├── Services/
│   └── Config/
├── tests/
│   ├── Unit/
│   └── Integration/
├── vendor/
├── config/
│   ├── database.php
│   └── app.php
├── storage/
│   ├── logs/
│   ├── cache/
│   └── uploads/
├── .env
├── .env.example
├── .gitignore
├── composer.json
├── composer.lock
├── phpunit.xml
└── README.md
```

### Code Standards

**PSR-12 compliant code:**
```php
<?php

declare(strict_types=1);

namespace App\Controllers;

use App\Models\User;
use App\Services\EmailService;
use Psr\Log\LoggerInterface;

class UserController
{
    private LoggerInterface $logger;
    private EmailService $emailService;
    
    public function __construct(
        LoggerInterface $logger,
        EmailService $emailService
    ) {
        $this->logger = $logger;
        $this->emailService = $emailService;
    }
    
    public function createUser(array $userData): User
    {
        try {
            $user = new User();
            $user->setName($userData['name']);
            $user->setEmail($userData['email']);
            $user->setPassword(password_hash($userData['password'], PASSWORD_ARGON2ID));
            
            $user->save();
            
            $this->emailService->sendWelcomeEmail($user);
            $this->logger->info('User created successfully', ['user_id' => $user->getId()]);
            
            return $user;
        } catch (\Exception $e) {
            $this->logger->error('Failed to create user', [
                'error' => $e->getMessage(),
                'userData' => $userData
            ]);
            throw $e;
        }
    }
    
    public function getUserById(int $id): ?User
    {
        return User::find($id);
    }
    
    public function updateUser(int $id, array $userData): bool
    {
        $user = $this->getUserById($id);
        
        if (!$user) {
            return false;
        }
        
        foreach ($userData as $field => $value) {
            match ($field) {
                'name' => $user->setName($value),
                'email' => $user->setEmail($value),
                default => null
            };
        }
        
        return $user->save();
    }
}
```

### Configuration Management

**Environment-based configuration:**
```php
<?php

class Config
{
    private static array $config = [];
    private static bool $loaded = false;
    
    public static function load(string $environment = 'production'): void
    {
        if (self::$loaded) {
            return;
        }
        
        $configFile = __DIR__ . "/config/{$environment}.php";
        
        if (!file_exists($configFile)) {
            throw new \RuntimeException("Configuration file not found: {$configFile}");
        }
        
        self::$config = require $configFile;
        self::$loaded = true;
    }
    
    public static function get(string $key, $default = null)
    {
        if (!self::$loaded) {
            self::load();
        }
        
        $keys = explode('.', $key);
        $value = self::$config;
        
        foreach ($keys as $k) {
            if (!isset($value[$k])) {
                return $default;
            }
            $value = $value[$k];
        }
        
        return $value;
    }
    
    public static function set(string $key, $value): void
    {
        $keys = explode('.', $key);
        $config = &self::$config;
        
        foreach ($keys as $k) {
            if (!isset($config[$k])) {
                $config[$k] = [];
            }
            $config = &$config[$k];
        }
        
        $config = $value;
    }
}

// config/production.php
return [
    'database' => [
        'host' => $_ENV['DB_HOST'] ?? 'localhost',
        'database' => $_ENV['DB_NAME'] ?? 'myapp',
        'username' => $_ENV['DB_USER'] ?? 'root',
        'password' => $_ENV['DB_PASS'] ?? '',
        'port' => $_ENV['DB_PORT'] ?? 3306,
        'charset' => 'utf8mb4',
        'options' => [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
            PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
            PDO::ATTR_EMULATE_PREPARES => false,
        ]
    ],
    'cache' => [
        'driver' => $_ENV['CACHE_DRIVER'] ?? 'file',
        'path' => $_ENV['CACHE_PATH'] ?? 'storage/cache',
        'ttl' => $_ENV['CACHE_TTL'] ?? 3600,
    ],
    'logging' => [
        'level' => $_ENV['LOG_LEVEL'] ?? 'INFO',
        'path' => $_ENV['LOG_PATH'] ?? 'storage/logs/app.log',
        'max_files' => 30,
    ],
    'security' => [
        'encryption_key' => $_ENV['APP_KEY'],
        'hash_algo' => 'sha256',
        'session_lifetime' => 1800,
    ]
];
```

### Error Handling

**Global error handler:**
```php
<?php

class ErrorHandler
{
    private LoggerInterface $logger;
    private bool $displayErrors;
    
    public function __construct(LoggerInterface $logger, bool $displayErrors = false)
    {
        $this->logger = $logger;
        $this->displayErrors = $displayErrors;
        
        set_error_handler([$this, 'handleError']);
        set_exception_handler([$this, 'handleException']);
        register_shutdown_function([$this, 'handleShutdown']);
    }
    
    public function handleError(int $severity, string $message, string $file, int $line): bool
    {
        if (!(error_reporting() & $severity)) {
            return false;
        }
        
        $errorInfo = [
            'severity' => $severity,
            'message' => $message,
            'file' => $file,
            'line' => $line,
            'trace' => debug_backtrace(DEBUG_BACKTRACE_IGNORE_ARGS)
        ];
        
        $this->logger->error('PHP Error', $errorInfo);
        
        if ($this->displayErrors) {
            echo "<pre>";
            print_r($errorInfo);
            echo "</pre>";
        }
        
        return true;
    }
    
    public function handleException(\Throwable $exception): void
    {
        $errorInfo = [
            'message' => $exception->getMessage(),
            'file' => $exception->getFile(),
            'line' => $exception->getLine(),
            'trace' => $exception->getTraceAsString()
        ];
        
        $this->logger->critical('Uncaught Exception', $errorInfo);
        
        if ($this->displayErrors) {
            echo "<h1>Uncaught Exception</h1>";
            echo "<pre>" . $exception . "</pre>";
        } else {
            http_response_code(500);
            echo "Internal Server Error";
        }
    }
    
    public function handleShutdown(): void
    {
        $error = error_get_last();
        
        if ($error !== null && $error['type'] === E_ERROR) {
            $this->logger->critical('Fatal Error', $error);
            
            if ($this->displayErrors) {
                echo "<h1>Fatal Error</h1>";
                echo "<pre>" . print_r($error, true) . "</pre>";
            }
        }
    }
}

// Initialize error handler
$logger = new Logger('app');
$errorHandler = new ErrorHandler($logger, Config::get('app.debug', false));
```

## Deployment Strategies

### IIS Deployment

**Web.config for production:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <handlers>
            <remove name="PHP_via_FastCGI" />
            <add name="PHP_via_FastCGI" 
                 path="*.php" 
                 verb="GET,HEAD,POST,PUT,DELETE,PATCH,OPTIONS" 
                 modules="FastCgiModule" 
                 scriptProcessor="C:\php\php-cgi.exe" 
                 resourceType="Either" 
                 requireAccess="Script" />
        </handlers>
        
        <defaultDocument>
            <files>
                <clear />
                <add value="index.php" />
                <add value="index.html" />
            </files>
        </defaultDocument>
        
        <rewrite>
            <rules>
                <rule name="Hide sensitive files" stopProcessing="true">
                    <match url="^(\.env|composer\.(json|lock)|\.git)" />
                    <action type="CustomResponse" statusCode="403" statusReason="Forbidden" />
                </rule>
                
                <rule name="Pretty URLs" stopProcessing="true">
                    <match url="^(.*)$" />
                    <conditions>
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php?route={R:1}" />
                </rule>
            </rules>
        </rewrite>
        
        <security>
            <requestFiltering>
                <fileExtensions>
                    <add fileExtension=".php" allowed="true" />
                </fileExtensions>
                <hiddenSegments>
                    <add segment="vendor" />
                    <add segment="storage" />
                    <add segment="config" />
                </hiddenSegments>
            </requestFiltering>
        </security>
        
        <httpCompression>
            <dynamicTypes>
                <add mimeType="text/css" enabled="true" />
                <add mimeType="application/javascript" enabled="true" />
                <add mimeType="application/json" enabled="true" />
            </dynamicTypes>
        </httpCompression>
        
        <httpErrors>
            <remove statusCode="404" />
            <error statusCode="404" path="/404.php" responseMode="ExecuteURL" />
        </httpErrors>
    </system.webServer>
</configuration>
```

### Docker Deployment

**Dockerfile for PHP application:**
```dockerfile
# Use official PHP image with Apache
FROM php:8.2-apache

# Set working directory
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    unzip

# Install PHP extensions
RUN docker-php-ext-install \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    zip

# Enable Apache modules
RUN a2enmod rewrite headers ssl

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy application files
COPY . .

# Install PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Set permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
RUN chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache

# Apache configuration
COPY docker/apache/000-default.conf /etc/apache2/sites-available/000-default.conf

# PHP configuration
COPY docker/php/php.ini /usr/local/etc/php/conf.d/app.ini

# Expose port
EXPOSE 80 443

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost/health || exit 1

# Start Apache
CMD ["apache2-foreground"]
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./storage/logs:/var/www/html/storage/logs
      - ./storage/uploads:/var/www/html/storage/uploads
    environment:
      - APP_ENV=production
      - DB_HOST=database
      - DB_DATABASE=myapp
      - DB_USERNAME=root
      - DB_PASSWORD=secret
    depends_on:
      - database
      - redis
    restart: unless-stopped

  database:
    image: mysql:8.0
    environment:
      - MYSQL_DATABASE=myapp
      - MYSQL_ROOT_PASSWORD=secret
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"
    restart: unless-stopped

  redis:
    image: redis:7-alpine
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./docker/nginx/nginx.conf:/etc/nginx/conf.d/default.conf
      - ./public:/var/www/html/public
    depends_on:
      - app
    restart: unless-stopped

volumes:
  mysql_data:
  redis_data:
```

### Automated Deployment

**PowerShell deployment script:**
```powershell
# deploy.ps1
param(
    [string]$Environment = "production",
    [string]$Branch = "main"
)

Write-Host "Starting deployment to $Environment..." -ForegroundColor Green

try {
    # Pull latest code
    Write-Host "Pulling latest code from $Branch..." -ForegroundColor Yellow
    git fetch origin
    git checkout $Branch
    git pull origin $Branch
    
    # Install/update dependencies
    Write-Host "Installing dependencies..." -ForegroundColor Yellow
    composer install --no-dev --optimize-autoloader
    
    # Run database migrations
    if ($Environment -eq "production") {
        Write-Host "Running database migrations..." -ForegroundColor Yellow
        php artisan migrate --force
    }
    
    # Clear and rebuild cache
    Write-Host "Rebuilding cache..." -ForegroundColor Yellow
    php artisan cache:clear
    php artisan config:cache
    php artisan route:cache
    php artisan view:cache
    
    # Clear OPcache
    Write-Host "Clearing OPcache..." -ForegroundColor Yellow
    # You can call a script endpoint that clears OPcache
    # Invoke-WebRequest -Uri "https://yourapp.com/clear-opcache" -Method POST
    
    # Restart IIS Application Pool (if using IIS)
    Write-Host "Restarting application pool..." -ForegroundColor Yellow
    Import-Module WebAdministration
    Restart-WebAppPool -Name "YourAppPool"
    
    Write-Host "Deployment completed successfully!" -ForegroundColor Green
    
} catch {
    Write-Host "Deployment failed: $($_.Exception.Message)" -ForegroundColor Red
    exit 1
}
```

## Monitoring and Maintenance

### Application Monitoring

**Health check endpoint:**
```php
<?php
// public/health.php

header('Content-Type: application/json');

$health = [
    'status' => 'ok',
    'timestamp' => date('c'),
    'checks' => []
];

try {
    // Database check
    $pdo = new PDO($dsn, $username, $password);
    $pdo->query('SELECT 1');
    $health['checks']['database'] = 'ok';
} catch (Exception $e) {
    $health['checks']['database'] = 'error';
    $health['status'] = 'error';
}

// File system check
if (is_writable('storage/logs')) {
    $health['checks']['filesystem'] = 'ok';
} else {
    $health['checks']['filesystem'] = 'error';
    $health['status'] = 'error';
}

// Memory check
$memoryUsage = memory_get_usage(true);
$memoryLimit = ini_get('memory_limit');
$memoryLimitBytes = return_bytes($memoryLimit);

if ($memoryUsage < ($memoryLimitBytes * 0.8)) {
    $health['checks']['memory'] = 'ok';
} else {
    $health['checks']['memory'] = 'warning';
}

$health['metrics'] = [
    'memory_usage' => round($memoryUsage / 1024 / 1024, 2) . ' MB',
    'memory_limit' => $memoryLimit,
    'php_version' => PHP_VERSION,
    'server_time' => date('Y-m-d H:i:s')
];

function return_bytes($val) {
    $val = trim($val);
    $last = strtolower($val[strlen($val)-1]);
    $val = (int)$val;
    switch($last) {
        case 'g': $val *= 1024;
        case 'm': $val *= 1024;
        case 'k': $val *= 1024;
    }
    return $val;
}

http_response_code($health['status'] === 'ok' ? 200 : 503);
echo json_encode($health, JSON_PRETTY_PRINT);
?>
```

### Log Management

**Automated log rotation script:**
```powershell
# log-rotation.ps1
param(
    [string]$LogDirectory = "C:\php\logs",
    [int]$MaxFiles = 30,
    [int]$MaxSizeMB = 100
)

$ErrorActionPreference = "Stop"

Write-Host "Starting log rotation for $LogDirectory" -ForegroundColor Green

try {
    $logFiles = Get-ChildItem -Path $LogDirectory -Filter "*.log"
    
    foreach ($logFile in $logFiles) {
        $fileSizeMB = [math]::Round($logFile.Length / 1MB, 2)
        
        # Rotate if file is too large
        if ($fileSizeMB -gt $MaxSizeMB) {
            $timestamp = Get-Date -Format "yyyyMMdd_HHmmss"
            $rotatedName = "$($logFile.BaseName)_$timestamp.log"
            $rotatedPath = Join-Path $LogDirectory $rotatedName
            
            Move-Item -Path $logFile.FullName -Destination $rotatedPath
            Write-Host "Rotated $($logFile.Name) to $rotatedName ($fileSizeMB MB)" -ForegroundColor Yellow
            
            # Create new empty log file
            New-Item -Path $logFile.FullName -ItemType File
        }
    }
    
    # Clean up old rotated files
    $pattern = "*_*.log"
    $oldFiles = Get-ChildItem -Path $LogDirectory -Filter $pattern | 
                Sort-Object LastWriteTime -Descending | 
                Select-Object -Skip $MaxFiles
    
    foreach ($oldFile in $oldFiles) {
        Remove-Item -Path $oldFile.FullName
        Write-Host "Removed old log file: $($oldFile.Name)" -ForegroundColor Red
    }
    
    Write-Host "Log rotation completed successfully" -ForegroundColor Green
    
} catch {
    Write-Host "Log rotation failed: $($_.Exception.Message)" -ForegroundColor Red
    exit 1
}
```

## Resources and Documentation

### Official Resources
- **PHP Official Documentation**: [https://www.php.net/docs.php](https://www.php.net/docs.php)
- **PHP.net Windows Documentation**: [https://www.php.net/manual/en/install.windows.php](https://www.php.net/manual/en/install.windows.php)
- **Composer Documentation**: [https://getcomposer.org/doc/](https://getcomposer.org/doc/)

### Framework Documentation
- **Laravel**: [https://laravel.com/docs](https://laravel.com/docs)
- **Symfony**: [https://symfony.com/doc/current/index.html](https://symfony.com/doc/current/index.html)
- **CodeIgniter**: [https://codeigniter.com/user_guide/](https://codeigniter.com/user_guide/)
- **Zend Framework/Laminas**: [https://docs.laminas.dev/](https://docs.laminas.dev/)

### Windows-Specific Resources
- **IIS Documentation**: [https://docs.microsoft.com/en-us/iis/](https://docs.microsoft.com/en-us/iis/)
- **PHP Manager for IIS**: [https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10](https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10)
- **Microsoft SQL Server PHP Drivers**: [https://docs.microsoft.com/en-us/sql/connect/php/](https://docs.microsoft.com/en-us/sql/connect/php/)

### Development Tools
- **PhpStorm**: [https://www.jetbrains.com/phpstorm/documentation/](https://www.jetbrains.com/phpstorm/documentation/)
- **Visual Studio Code PHP**: [https://code.visualstudio.com/docs/languages/php](https://code.visualstudio.com/docs/languages/php)
- **XDebug**: [https://xdebug.org/docs/](https://xdebug.org/docs/)

### Testing and Quality
- **PHP_CodeSniffer**: [https://github.com/squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- **PHPStan**: [https://phpstan.org/user-guide/getting-started](https://phpstan.org/user-guide/getting-started)
- **Psalm**: [https://psalm.dev/docs/](https://psalm.dev/docs/)

### Security Resources
- **OWASP PHP Security**: [https://owasp.org/www-project-php-security-cheat-sheet/](https://owasp.org/www-project-php-security-cheat-sheet/)
- **PHP Security Guide**: [https://phpsec.org/](https://phpsec.org/)
- **Securify PHP**: [https://github.com/securifybv/PHP-Security-Audit](https://github.com/securifybv/PHP-Security-Audit)

### Performance and Optimization
- **PHP Benchmarks**: [https://www.techempower.com/benchmarks/](https://www.techempower.com/benchmarks/)
- **Blackfire.io**: [https://blackfire.io/docs/introduction](https://blackfire.io/docs/introduction)
- **New Relic PHP**: [https://docs.newrelic.com/docs/agents/php-agent/](https://docs.newrelic.com/docs/agents/php-agent/)

### Community and Learning
- **PHP The Right Way**: [https://phptherightway.com/](https://phptherightway.com/)
- **PHP Weekly Newsletter**: [https://www.phpweekly.com/](https://www.phpweekly.com/)
- **PHP Reddit Community**: [https://reddit.com/r/PHP](https://reddit.com/r/PHP)
- **PHP Discord Server**: [https://discord.gg/php](https://discord.gg/php)
- **PHP Conferences**: [https://php.net/conferences/](https://php.net/conferences/)

### Enterprise Integration
- **Active Directory Authentication**: [https://www.php.net/manual/en/book.ldap.php](https://www.php.net/manual/en/book.ldap.php)
- **Windows Services with PHP**: [https://github.com/mnapoli/silly](https://github.com/mnapoli/silly)
- **Enterprise Patterns**: [https://martinfowler.com/eaaCatalog/](https://martinfowler.com/eaaCatalog/)

---

## Quick Reference

### Essential PHP Commands

```cmd
# Version and configuration
php --version
php --ini
php -m                    # List loaded modules
php -i                    # phpinfo() from command line

# Syntax checking
php -l script.php         # Check syntax
php -f script.php         # Execute script

# Development server
php -S localhost:8000     # Start built-in server
php -S localhost:8000 -t public  # With document root

# Composer commands
composer install          # Install dependencies
composer update           # Update dependencies  
composer dump-autoload    # Regenerate autoloader
composer require package  # Add new package
composer show             # List installed packages
```

### Common php.ini Settings

```ini
# Production settings
display_errors = Off
log_errors = On
error_log = "C:\php\logs\php_errors.log"
memory_limit = 256M
post_max_size = 32M
upload_max_filesize = 32M
max_execution_time = 60
session.cookie_httponly = 1
session.cookie_secure = 1
opcache.enable = 1

# Development settings  
display_errors = On
error_reporting = E_ALL
memory_limit = 512M
max_execution_time = 300
opcache.enable = 0
xdebug.mode = debug
```

### IIS FastCGI Configuration

```xml
<configuration>
  <system.webServer>
    <handlers>
      <add name="PHP_via_FastCGI" 
           path="*.php" 
           verb="*" 
           modules="FastCgiModule" 
           scriptProcessor="C:\php\php-cgi.exe" 
           resourceType="Either" />
    </handlers>
  </system.webServer>
</configuration>
```

### Security Checklist

- [ ] Disable `display_errors` in production
- [ ] Enable `log_errors` and configure error log
- [ ] Set secure session cookies (`httponly`, `secure`, `samesite`)
- [ ] Use prepared statements for database queries
- [ ] Validate and sanitize all user input
- [ ] Keep PHP and extensions updated
- [ ] Configure proper file permissions
- [ ] Use HTTPS for all data transmission
- [ ] Implement CSRF protection
- [ ] Set appropriate HTTP security headers

---

## Conclusion

This comprehensive guide provides everything needed to set up and maintain PHP development environments on Windows 11 Enterprise. From basic installation through advanced enterprise deployment strategies, the documentation covers security considerations, performance optimization, and best practices specific to corporate environments.

The enterprise focus ensures compatibility with corporate security policies, Active Directory integration, proxy configurations, and deployment requirements that are common in large organizations.

For additional support or questions specific to your environment, consult your IT department or visit the [syslogine.cloud](https://syslogine.cloud) documentation portal for updates and additional resources.

---

*Last updated: September 15, 2025*  
*Document version: 1.0*  
*For updates and corrections, please visit: [https://syslogine.cloud/docs/os/windows/tutorials/php/php-windows-guide](https://syslogine.cloud/docs/os/windows/tutorials/php/php-windows-guide)*