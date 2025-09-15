---
title: "Python Development Guide for Windows 11 Enterprise"
description: "Complete guide for setting up and using Python on Windows 11 Enterprise environments"
date: 2025-09-15
weight: 10
draft: false
toc: true
tags: ["python", "windows", "enterprise", "development"]
categories: ["Development", "Windows"]
---

# Python Development Guide for Windows 11 Enterprise

## Overview

This comprehensive guide covers the complete process of installing, configuring, and using Python in Windows 11 Enterprise environments. From basic installation to advanced development setups, this documentation will help system administrators and developers establish robust Python environments.

## Prerequisites

- Windows 11 Enterprise (build 22000 or higher)
- Administrator privileges for system-wide installation
- Minimum 4GB free disk space
- Internet connectivity for downloads
- Corporate network access (if behind proxy/firewall)

## Installation Methods

### Method 1: Official Python.org Installer (Recommended)

The official Python installer provides the most control and compatibility for enterprise environments.

**Step-by-step installation:**

1. **Download Python**
   ```powershell
   # Navigate to https://python.org/downloads/windows/
   # Download the latest stable release (3.11+ recommended)
   ```

2. **Installation Configuration**
   - ✅ Check "Add Python to PATH"
   - ✅ Choose "Customize installation"
   - ✅ Select all Optional Features:
     - Documentation
     - pip
     - tcl/tk and IDLE
     - Python test suite
     - py launcher
   - ✅ Advanced Options:
     - Install for all users
     - Associate files with Python
     - Create shortcuts for installed applications
     - Add Python to environment variables
     - Precompile standard library

3. **Verification**
   ```cmd
   python --version
   pip --version
   py --version
   ```

### Method 2: Microsoft Store

Suitable for users without administrator privileges.

```powershell
# Search "Python 3.11" in Microsoft Store
# Click "Get" or "Install"
```

**Advantages:**
- Automatic updates
- Sandboxed installation
- No administrator privileges required

**Limitations:**
- Restricted system access
- Limited package installation capabilities
- May have PATH issues

### Method 3: Windows Package Manager (winget)

Ideal for automated deployments and system management.

```powershell
# Run as Administrator
winget search Python.Python
winget install Python.Python.3.11

# Verify installation
winget list | findstr Python
```

### Method 4: Chocolatey

For organizations using Chocolatey package management.

```powershell
# Install Chocolatey first (if not present)
# Run as Administrator
choco install python --version=3.11.5

# Verify
python --version
```

## Environment Configuration

### Python Launcher Configuration

The Python Launcher (`py.exe`) helps manage multiple Python versions.

**Create py.ini** in `%LOCALAPPDATA%\py.ini`:
```ini
[defaults]
python=3.11-64

[commands]
3.11-64=C:\Python311\python.exe
3.10-64=C:\Python310\python.exe
```

**Usage examples:**
```cmd
py -3.11 script.py        # Use Python 3.11
py -3.10 -m pip install  # Use pip from Python 3.10
py -0                     # List installed versions
```

### Virtual Environments

Virtual environments are essential for project isolation and dependency management.

#### Using venv (Built-in)

```cmd
# Create virtual environment
python -m venv project_env

# Activate (Windows)
project_env\Scripts\activate

# Activate (PowerShell)
project_env\Scripts\Activate.ps1

# Deactivate
deactivate

# Remove environment
rmdir /s project_env
```

#### Using virtualenv (Third-party)

```cmd
# Install virtualenv
pip install virtualenv

# Create environment with specific Python version
virtualenv -p python3.11 myproject

# Advanced options
virtualenv --system-site-packages myproject  # Inherit global packages
virtualenv --clear myproject                 # Clear existing environment
```

#### Using conda (Data Science)

```cmd
# Install Miniconda first
# Create environment
conda create -n myproject python=3.11

# Activate
conda activate myproject

# Install packages
conda install numpy pandas matplotlib

# Export environment
conda env export > environment.yml

# Create from file
conda env create -f environment.yml
```

### PATH Configuration

**Check current PATH:**
```cmd
echo %PATH%
where python
where pip
```

**Manual PATH configuration:**
1. Open "Environment Variables" (Windows + R → `sysdm.cpl` → Advanced → Environment Variables)
2. Edit System PATH variable
3. Add Python paths:
   - `C:\Python311\`
   - `C:\Python311\Scripts\`

**PowerShell PATH modification:**
```powershell
# Temporary (current session)
$env:PATH += ";C:\Python311;C:\Python311\Scripts"

# Permanent (user level)
[Environment]::SetEnvironmentVariable("Path", $env:PATH + ";C:\Python311;C:\Python311\Scripts", "User")
```

## Package Management

### pip Configuration

**Global pip configuration** (`%APPDATA%\pip\pip.ini`):
```ini
[global]
timeout = 60
index-url = https://pypi.org/simple/
trusted-host = pypi.org
                pypi.python.org
                files.pythonhosted.org

[install]
upgrade = true
user = false
```

**Basic pip commands:**
```cmd
# Upgrade pip
python -m pip install --upgrade pip

# Install package
pip install requests

# Install specific version
pip install django==4.2.5

# Install from requirements file
pip install -r requirements.txt

# Generate requirements file
pip freeze > requirements.txt

# Show package information
pip show requests

# List installed packages
pip list
pip list --outdated

# Uninstall package
pip uninstall requests

# Install in user directory
pip install --user package_name
```

### Enterprise Proxy Configuration

Many enterprises use corporate proxies that require special configuration.

**Command line proxy:**
```cmd
pip install --proxy http://user:password@proxy.company.com:8080 requests
```

**Permanent proxy configuration** (in pip.ini):
```ini
[global]
proxy = http://proxy.company.com:8080
trusted-host = proxy.company.com
               pypi.org
               pypi.python.org
               files.pythonhosted.org
```

**Environment variables:**
```cmd
set HTTP_PROXY=http://proxy.company.com:8080
set HTTPS_PROXY=http://proxy.company.com:8080
set NO_PROXY=localhost,127.0.0.1,.company.com
```

### SSL Certificate Issues

Corporate environments often have custom SSL certificates.

**Temporary SSL bypass:**
```cmd
pip install --trusted-host pypi.org --trusted-host pypi.python.org requests
```

**Python script certificate handling:**
```python
import ssl
import certifi

# Get certificate bundle location
print(certifi.where())

# Disable SSL verification (NOT recommended for production)
ssl._create_default_https_context = ssl._create_unverified_context
```

## Development Tools

### Code Editors and IDEs

#### Visual Studio Code

```powershell
# Install via winget
winget install Microsoft.VisualStudioCode

# Or via Chocolatey
choco install vscode
```

**Essential Python extensions:**
- Python (Microsoft)
- Python Docstring Generator
- Python Type Hint
- Python Test Explorer
- GitLens
- Python Environment Manager

**VS Code Python settings** (`.vscode/settings.json`):
```json
{
    "python.defaultInterpreterPath": "./venv/Scripts/python.exe",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.formatting.provider": "black",
    "python.testing.pytestEnabled": true,
    "python.testing.unittestEnabled": false,
    "files.associations": {
        "*.py": "python"
    }
}
```

#### PyCharm

```powershell
# Community Edition (Free)
winget install JetBrains.PyCharm.Community

# Professional Edition
winget install JetBrains.PyCharm.Professional
```

### Debugging Configuration

**VS Code debugging** (`.vscode/launch.json`):
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "cwd": "${workspaceFolder}",
            "env": {
                "PYTHONPATH": "${workspaceFolder}"
            }
        },
        {
            "name": "Python: Module",
            "type": "python",
            "request": "launch",
            "module": "main",
            "console": "integratedTerminal",
            "cwd": "${workspaceFolder}"
        }
    ]
}
```

**Built-in Python debugger:**
```python
import pdb

def problematic_function():
    x = 10
    pdb.set_trace()  # Debugger will stop here
    y = x * 2
    return y

# Alternative: post-mortem debugging
import sys
import traceback

try:
    problematic_function()
except:
    type, value, tb = sys.exc_info()
    traceback.print_exc()
    pdb.post_mortem(tb)
```

### Testing Frameworks

#### pytest Setup

```cmd
pip install pytest pytest-cov pytest-html

# Create test structure
mkdir tests
echo. > tests\__init__.py
echo. > tests\test_example.py
```

**Basic test example** (`tests/test_example.py`):
```python
import pytest
from src.calculator import Calculator

def test_addition():
    calc = Calculator()
    assert calc.add(2, 3) == 5

def test_division_by_zero():
    calc = Calculator()
    with pytest.raises(ZeroDivisionError):
        calc.divide(10, 0)

@pytest.fixture
def sample_data():
    return {"name": "test", "value": 42}

def test_with_fixture(sample_data):
    assert sample_data["name"] == "test"
    assert sample_data["value"] == 42
```

**pytest configuration** (`pytest.ini`):
```ini
[tool:pytest]
testpaths = tests
python_files = test_*.py *_test.py
python_classes = Test*
python_functions = test_*
addopts = 
    --verbose
    --cov=src
    --cov-report=html
    --cov-report=term-missing
    --html=reports/report.html
    --self-contained-html
```

**Running tests:**
```cmd
# Run all tests
pytest

# Run specific test file
pytest tests/test_example.py

# Run with coverage
pytest --cov=src tests/

# Run with HTML report
pytest --html=report.html --self-contained-html
```

#### unittest (Built-in)

```python
import unittest
from src.calculator import Calculator

class TestCalculator(unittest.TestCase):
    
    def setUp(self):
        self.calc = Calculator()
    
    def test_addition(self):
        result = self.calc.add(2, 3)
        self.assertEqual(result, 5)
    
    def test_subtraction(self):
        result = self.calc.subtract(10, 5)
        self.assertEqual(result, 5)
    
    def tearDown(self):
        # Cleanup after each test
        pass

if __name__ == '__main__':
    unittest.main()
```

## Enterprise Considerations

### Security Best Practices

#### Certificate Management

**Corporate certificate integration:**
```python
import requests
import ssl
import certifi

# Add corporate certificates to certifi bundle
def add_corporate_certs():
    ca_bundle = certifi.where()
    with open(ca_bundle, 'a') as f:
        with open('corporate-cert.pem', 'r') as corp_cert:
            f.write(corp_cert.read())

# Use corporate proxy with authentication
proxies = {
    'http': 'http://username:password@proxy.company.com:8080',
    'https': 'https://username:password@proxy.company.com:8080'
}

response = requests.get('https://api.example.com', proxies=proxies)
```

#### Secure Package Installation

```cmd
# Verify package signatures
pip install --only-binary=all package_name

# Install from trusted sources only
pip install --index-url https://pypi.company.com/simple/ package_name

# Hash verification
pip install --require-hashes -r requirements.txt
```

**requirements.txt with hashes:**
```
requests==2.31.0 \
    --hash=sha256:58cd2187c01e70e6e26505bca751777aa9f2ee0b7f4300988b709f44e013003f \
    --hash=sha256:942c5a758f98d790eaed1a29cb6eefc7ffb0d1cf7af05c3d2791656dbd6ad1e1
```

### Group Policy Configuration

**Relevant GPO settings for Python deployment:**

1. **Software Installation**
   - Computer Configuration → Software Settings → Software Installation
   - Deploy Python MSI packages via GPO

2. **Script Execution Policies**
   - Computer Configuration → Administrative Templates → Windows Components → Windows PowerShell
   - Set execution policy for PowerShell scripts

3. **Application Control**
   - Use AppLocker or Windows Defender Application Control
   - Allow Python interpreters and approved packages

### Antivirus Exclusions

**Add these paths to antivirus exclusions:**
- `C:\Python*\` (Python installation directories)
- `%USERPROFILE%\AppData\Local\Programs\Python\`
- `%USERPROFILE%\venv\` (virtual environments)
- `*.py` files
- `*.pyc` files (compiled bytecode)
- Project development directories

**PowerShell script for exclusions:**
```powershell
# Run as Administrator
Add-MpPreference -ExclusionPath "C:\Python311"
Add-MpPreference -ExclusionPath "$env:USERPROFILE\venv"
Add-MpPreference -ExclusionExtension ".py"
Add-MpPreference -ExclusionExtension ".pyc"
```

### Network Security

**Firewall rules for Python applications:**
```cmd
# Allow Python through Windows Firewall
netsh advfirewall firewall add rule name="Python" dir=in action=allow program="C:\Python311\python.exe"

# Allow pip to access PyPI
netsh advfirewall firewall add rule name="Python pip" dir=out action=allow program="C:\Python311\Scripts\pip.exe"
```

## Performance Optimization

### Compiler Tools

Many Python packages require compilation of C extensions.

**Microsoft C++ Build Tools:**
```powershell
# Install via winget
winget install Microsoft.VisualStudio.2022.BuildTools

# Or download from Microsoft
# https://visualstudio.microsoft.com/visual-cpp-build-tools/
```

**Alternative: Microsoft Visual C++ Redistributable:**
```powershell
winget install Microsoft.VCRedist.2015+.x64
```

### Memory and Performance Tuning

**Memory profiling:**
```cmd
pip install memory-profiler psutil

# Profile memory usage
python -m memory_profiler script.py
```

**Performance monitoring:**
```python
import psutil
import time

def monitor_performance():
    # CPU usage
    cpu_percent = psutil.cpu_percent(interval=1)
    
    # Memory usage
    memory = psutil.virtual_memory()
    memory_percent = memory.percent
    
    # Disk usage
    disk = psutil.disk_usage('/')
    disk_percent = disk.percent
    
    print(f"CPU: {cpu_percent}%")
    print(f"Memory: {memory_percent}%")
    print(f"Disk: {disk_percent}%")

# Garbage collection optimization
import gc
gc.set_threshold(700, 10, 10)  # Tune garbage collection thresholds
```

### Python Optimization

**Bytecode compilation:**
```cmd
# Compile all .py files to .pyc
python -m compileall src/

# Optimize bytecode (-O removes assert statements, -OO removes docstrings)
python -O script.py
python -OO script.py
```

## Common Issues and Troubleshooting

### SSL Certificate Errors

**Problem:** `SSL: CERTIFICATE_VERIFY_FAILED` errors when using pip or requests.

**Solutions:**
```cmd
# Method 1: Upgrade certificates
pip install --upgrade certifi

# Method 2: Use trusted hosts
pip install --trusted-host pypi.org --trusted-host pypi.python.org package_name

# Method 3: Configure pip permanently
pip config set global.trusted-host "pypi.org pypi.python.org files.pythonhosted.org"
```

**Corporate environment solution:**
```python
import os
import ssl
import certifi

# Point to corporate certificate bundle
os.environ['SSL_CERT_FILE'] = r'C:\path\to\corporate\cacert.pem'
os.environ['REQUESTS_CA_BUNDLE'] = r'C:\path\to\corporate\cacert.pem'
```

### Module Import Errors

**Problem:** `ModuleNotFoundError` even though package is installed.

**Diagnostics:**
```python
import sys
print("Python executable:", sys.executable)
print("Python path:", sys.path)

# Check if module is in site-packages
import site
print("Site packages:", site.getsitepackages())
```

**Solutions:**
```cmd
# Check if in correct environment
pip list | findstr package_name

# Reinstall package
pip uninstall package_name
pip install package_name

# Install in development mode
pip install -e .

# Add to PYTHONPATH
set PYTHONPATH=%PYTHONPATH%;C:\path\to\modules
```

### Permission Errors

**Problem:** `PermissionError` during package installation.

**Solutions:**
```cmd
# Install for current user only
pip install --user package_name

# Use virtual environment
python -m venv venv
venv\Scripts\activate
pip install package_name

# Run as administrator (not recommended)
# Right-click command prompt → "Run as administrator"
```

### Encoding Issues

**Problem:** `UnicodeDecodeError` or `UnicodeEncodeError`.

**Solutions:**
```python
# Set encoding in script header
# -*- coding: utf-8 -*-

# Set environment variable
import os
os.environ['PYTHONIOENCODING'] = 'utf-8'

# Open files with explicit encoding
with open('file.txt', 'r', encoding='utf-8') as f:
    content = f.read()

# Set default encoding (Python 3.7+)
import locale
locale.setlocale(locale.LC_ALL, 'en_US.UTF-8')
```

### Path Length Limitations

**Problem:** Windows path length limit (260 characters) causing issues.

**Solutions:**
```cmd
# Enable long paths in Group Policy
# Computer Configuration → Administrative Templates → System → Filesystem
# Enable "Enable Win32 long paths"

# Registry modification (requires admin)
reg add HKLM\SYSTEM\CurrentControlSet\Control\FileSystem /v LongPathsEnabled /t REG_DWORD /d 1
```

**Python workaround:**
```python
import os

# Use UNC paths for long paths
long_path = r"\\?\C:\very\long\path\to\file.txt"

# Or use pathlib (Python 3.4+)
from pathlib import Path
path = Path(r"C:\very\long\path")
```

## Best Practices

### Project Structure

**Standard Python project layout:**
```
my_project/
├── src/
│   └── my_package/
│       ├── __init__.py
│       ├── main.py
│       └── utils.py
├── tests/
│   ├── __init__.py
│   ├── test_main.py
│   └── test_utils.py
├── docs/
│   ├── index.md
│   └── api.md
├── scripts/
│   └── deploy.py
├── requirements/
│   ├── base.txt
│   ├── dev.txt
│   └── prod.txt
├── .gitignore
├── .env.example
├── README.md
├── setup.py
├── pyproject.toml
└── tox.ini
```

### Dependency Management

**requirements.txt structure:**
```
# base.txt - Core dependencies
requests>=2.28.0,<3.0.0
click>=8.0.0
pydantic>=1.10.0

# dev.txt - Development dependencies
-r base.txt
pytest>=7.0.0
black>=22.0.0
flake8>=5.0.0
mypy>=0.991
pre-commit>=2.20.0

# prod.txt - Production dependencies
-r base.txt
gunicorn>=20.1.0
```

**Using pyproject.toml (modern approach):**
```toml
[build-system]
requires = ["setuptools>=45", "wheel", "setuptools_scm[toml]>=6.2"]
build-backend = "setuptools.build_meta"

[project]
name = "my-project"
version = "0.1.0"
description = "My awesome Python project"
authors = [{name = "Your Name", email = "your.email@company.com"}]
license = {file = "LICENSE"}
readme = "README.md"
requires-python = ">=3.9"
dependencies = [
    "requests>=2.28.0",
    "click>=8.0.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0.0",
    "black>=22.0.0",
    "flake8>=5.0.0",
    "mypy>=0.991",
]

[project.scripts]
my-cli = "my_package.main:cli"

[tool.black]
line-length = 88
target-version = ['py39']

[tool.isort]
profile = "black"
line_length = 88

[tool.mypy]
python_version = "3.9"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true
```

### Code Quality Tools

**Install code quality tools:**
```cmd
pip install black isort flake8 mypy bandit safety pre-commit
```

**Black (code formatting):**
```cmd
# Format all Python files
black src/ tests/

# Check without modifying
black --check src/ tests/

# Configuration in pyproject.toml
[tool.black]
line-length = 88
target-version = ['py39', 'py310', 'py311']
```

**isort (import sorting):**
```cmd
# Sort imports
isort src/ tests/

# Check without modifying
isort --check-only src/ tests/

# Configuration in pyproject.toml
[tool.isort]
profile = "black"
line_length = 88
```

**flake8 (linting):**
```cmd
# Lint code
flake8 src/ tests/

# Configuration in setup.cfg
[flake8]
max-line-length = 88
extend-ignore = E203, W503
```

**mypy (type checking):**
```cmd
# Type check
mypy src/

# Configuration in pyproject.toml
[tool.mypy]
python_version = "3.9"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true
```

**pre-commit hooks:**
```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/psf/black
    rev: 22.12.0
    hooks:
      - id: black
        language_version: python3.11

  - repo: https://github.com/pycqa/isort
    rev: 5.11.4
    hooks:
      - id: isort

  - repo: https://github.com/pycqa/flake8
    rev: 6.0.0
    hooks:
      - id: flake8

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v0.991
    hooks:
      - id: mypy
        additional_dependencies: [types-all]

  - repo: https://github.com/PyCQA/bandit
    rev: 1.7.4
    hooks:
      - id: bandit
        args: ['-r', 'src/']
```

**Install pre-commit:**
```cmd
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

### Documentation

**Sphinx documentation:**
```cmd
pip install sphinx sphinx-rtd-theme sphinx-autodoc-typehints

# Initialize documentation
sphinx-quickstart docs

# Build documentation
cd docs
make html
```

**Sphinx configuration** (`docs/conf.py`):
```python
import os
import sys
sys.path.insert(0, os.path.abspath('../src'))

project = 'My Project'
copyright = '2025, Your Name'
author = 'Your Name'

extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.viewcode',
    'sphinx.ext.napoleon',
    'sphinx_rtd_theme',
    'sphinx_autodoc_typehints',
]

html_theme = 'sphinx_rtd_theme'
```

**Docstring standards:**
```python
def calculate_area(length: float, width: float) -> float:
    """Calculate the area of a rectangle.
    
    Args:
        length: The length of the rectangle in meters.
        width: The width of the rectangle in meters.
        
    Returns:
        The area of the rectangle in square meters.
        
    Raises:
        ValueError: If length or width is negative.
        
    Example:
        >>> calculate_area(5.0, 3.0)
        15.0
    """
    if length < 0 or width < 0:
        raise ValueError("Length and width must be non-negative")
    return length * width
```

## Deployment Strategies

### Packaging Applications

#### PyInstaller

**Install and basic usage:**
```cmd
pip install pyinstaller

# Create single executable
pyinstaller --onefile --windowed app.py

# Advanced options
pyinstaller --onefile --windowed --icon=app.ico --name=MyApp app.py

# With additional data files
pyinstaller --onefile --add-data "templates;templates" --add-data "static;static" app.py
```

**PyInstaller spec file** (`app.spec`):
```python
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(
    ['src/main.py'],
    pathex=[],
    binaries=[],
    datas=[('templates', 'templates'), ('static', 'static')],
    hiddenimports=['pkg_resources.py2_warn'],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    win_no_prefer_redirects=False,
    win_private_assemblies=False,
    cipher=block_cipher,
    noarchive=False,
)

pyz = PYZ(a.pure, a.zipped_data, cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    a.binaries,
    a.zipfiles,
    a.datas,
    [],
    name='MyApp',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    upx_exclude=[],
    runtime_tmpdir=None,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon='app.ico'
)
```

#### cx_Freeze

```cmd
pip install cx_Freeze

# Create setup.py
python setup.py build
```

**cx_Freeze setup.py:**
```python
from cx_Freeze import setup, Executable

build_options = {
    'packages': [],
    'excludes': [],
    'include_files': ['templates/', 'static/']
}

executables = [
    Executable('src/main.py', target_name='MyApp.exe', icon='app.ico')
]

setup(
    name='MyApp',
    version='1.0',
    description='My Python Application',
    options={'build_exe': build_options},
    executables=executables
)
```

### Docker Containerization

**Dockerfile for Python application:**
```dockerfile
# Use official Python runtime as base image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONPATH=/app

# Install system dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY src/ ./src/
COPY tests/ ./tests/

# Create non-root user
RUN useradd --create-home --shell /bin/bash app \
    && chown -R app:app /app
USER app

# Expose port
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

# Run application
CMD ["python", "-m", "src.main"]
```

**Multi-stage build for smaller images:**
```dockerfile
# Build stage
FROM python:3.11-slim as builder

WORKDIR /app

# Install build dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt

# Production stage
FROM python:3.11-slim

WORKDIR /app

# Copy Python dependencies from builder
COPY --from=builder /root/.local /root/.local

# Copy application
COPY src/ ./src/

# Create non-root user
RUN useradd --create-home --shell /bin/bash app
USER app

# Make sure scripts in .local are usable
ENV PATH=/root/.local/bin:$PATH

CMD ["python", "-m", "src.main"]
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8000:8000"
    environment:
      - ENVIRONMENT=production
      - DATABASE_URL=postgresql://user:pass@db:5432/myapp
    volumes:
      - app_logs:/app/logs
    depends_on:
      - db
      - redis
    restart: unless-stopped

  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  redis:
    image: redis:7-alpine
    restart: unless-stopped

volumes:
  postgres_data:
  app_logs:
```

### Windows Services

**Creating a Windows service with pywin32:**
```cmd
pip install pywin32
```

**Service implementation:**
```python
import win32serviceutil
import win32service
import win32event
import servicemanager
import socket
import sys
import logging

class AppService(win32serviceutil.ServiceFramework):
    _svc_name_ = "MyPythonService"
    _svc_display_name_ = "My Python Application Service"
    _svc_description_ = "Python application running as Windows service"

    def __init__(self, args):
        win32serviceutil.ServiceFramework.__init__(self, args)
        self.hWaitStop = win32event.CreateEvent(None, 0, 0, None)
        socket.setdefaulttimeout(60)
        self.is_alive = True

    def SvcStop(self):
        self.ReportServiceStatus(win32service.SERVICE_STOP_PENDING)
        win32event.SetEvent(self.hWaitStop)
        self.is_alive = False

    def SvcDoRun(self):
        servicemanager.LogMsg(servicemanager.EVENTLOG_INFORMATION_TYPE,
                            servicemanager.PYS_SERVICE_STARTED,
                            (self._svc_name_, ''))
        self.main()

    def main(self):
        # Your application logic here
        import time
        while self.is_alive:
            # Do work
            time.sleep(30)

if __name__ == '__main__':
    win32serviceutil.HandleCommandLine(AppService)
```

**Install and manage service:**
```cmd
# Install service
python app_service.py install

# Start service
python app_service.py start

# Stop service
python app_service.py stop

# Remove service
python app_service.py remove
```

## Monitoring and Logging

### Logging Configuration

**Advanced logging setup:**
```python
import logging
import logging.config
import logging.handlers
import os
from pathlib import Path

# Create logs directory
log_dir = Path("logs")
log_dir.mkdir(exist_ok=True)

LOGGING_CONFIG = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'standard': {
            'format': '%(asctime)s [%(levelname)s] %(name)s: %(message)s'
        },
        'detailed': {
            'format': '%(asctime)s [%(levelname)s] %(name)s [%(filename)s:%(lineno)d]: %(message)s'
        },
        'json': {
            'format': '{"timestamp": "%(asctime)s", "level": "%(levelname)s", "logger": "%(name)s", "message": "%(message)s"}'
        }
    },
    'handlers': {
        'console': {
            'level': 'INFO',
            'class': 'logging.StreamHandler',
            'formatter': 'standard',
            'stream': 'ext://sys.stdout'
        },
        'file': {
            'level': 'DEBUG',
            'class': 'logging.handlers.RotatingFileHandler',
            'formatter': 'detailed',
            'filename': 'logs/app.log',
            'maxBytes': 10485760,  # 10MB
            'backupCount': 5
        },
        'error_file': {
            'level': 'ERROR',
            'class': 'logging.handlers.RotatingFileHandler',
            'formatter': 'detailed',
            'filename': 'logs/error.log',
            'maxBytes': 10485760,
            'backupCount': 3
        },
        'syslog': {
            'level': 'INFO',
            'class': 'logging.handlers.SysLogHandler',
            'formatter': 'standard',
            'address': ('localhost', 514)
        }
    },
    'loggers': {
        '': {  # root logger
            'handlers': ['console', 'file', 'error_file'],
            'level': 'DEBUG',
            'propagate': False
        },
        'urllib3': {
            'level': 'WARNING'
        },
        'requests': {
            'level': 'WARNING'
        }
    }
}

# Apply logging configuration
logging.config.dictConfig(LOGGING_CONFIG)

# Usage example
logger = logging.getLogger(__name__)

def example_function():
    logger.info("Application started")
    try:
        # Some operation
        result = 10 / 0
    except ZeroDivisionError:
        logger.error("Division by zero error", exc_info=True)
    except Exception as e:
        logger.exception("Unexpected error occurred")
```

**Windows Event Log integration:**
```python
import logging
import logging.handlers

# Configure Windows Event Log handler
event_log_handler = logging.handlers.NTEventLogHandler(
    appname="MyPythonApp",
    logtype="Application"
)
event_log_handler.setLevel(logging.ERROR)

formatter = logging.Formatter(
    '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
event_log_handler.setFormatter(formatter)

# Add to logger
logger = logging.getLogger()
logger.addHandler(event_log_handler)
```

### Performance Monitoring

**Application performance monitoring:**
```python
import time
import psutil
import threading
from dataclasses import dataclass
from typing import Dict, Any

@dataclass
class SystemMetrics:
    cpu_percent: float
    memory_percent: float
    disk_usage_percent: float
    network_io: Dict[str, int]
    timestamp: float

class PerformanceMonitor:
    def __init__(self, interval: int = 60):
        self.interval = interval
        self.running = False
        self.metrics_history = []
        
    def start_monitoring(self):
        self.running = True
        monitor_thread = threading.Thread(target=self._monitor_loop)
        monitor_thread.daemon = True
        monitor_thread.start()
        
    def stop_monitoring(self):
        self.running = False
        
    def _monitor_loop(self):
        while self.running:
            metrics = self._collect_metrics()
            self.metrics_history.append(metrics)
            
            # Keep only last 24 hours of data (assuming 60s interval)
            if len(self.metrics_history) > 1440:
                self.metrics_history.pop(0)
                
            time.sleep(self.interval)
            
    def _collect_metrics(self) -> SystemMetrics:
        # CPU usage
        cpu_percent = psutil.cpu_percent(interval=1)
        
        # Memory usage
        memory = psutil.virtual_memory()
        memory_percent = memory.percent
        
        # Disk usage
        disk = psutil.disk_usage('/')
        disk_percent = disk.percent
        
        # Network I/O
        network_io = psutil.net_io_counters()._asdict()
        
        return SystemMetrics(
            cpu_percent=cpu_percent,
            memory_percent=memory_percent,
            disk_usage_percent=disk_percent,
            network_io=network_io,
            timestamp=time.time()
        )
        
    def get_current_metrics(self) -> SystemMetrics:
        return self._collect_metrics()
        
    def get_average_metrics(self, last_minutes: int = 10) -> Dict[str, float]:
        if not self.metrics_history:
            return {}
            
        cutoff_time = time.time() - (last_minutes * 60)
        recent_metrics = [m for m in self.metrics_history if m.timestamp >= cutoff_time]
        
        if not recent_metrics:
            return {}
            
        return {
            'avg_cpu_percent': sum(m.cpu_percent for m in recent_metrics) / len(recent_metrics),
            'avg_memory_percent': sum(m.memory_percent for m in recent_metrics) / len(recent_metrics),
            'avg_disk_percent': sum(m.disk_usage_percent for m in recent_metrics) / len(recent_metrics)
        }

# Usage
monitor = PerformanceMonitor(interval=30)
monitor.start_monitoring()

# Get current system state
current = monitor.get_current_metrics()
print(f"CPU: {current.cpu_percent}%, Memory: {current.memory_percent}%")

# Get averages
averages = monitor.get_average_metrics(last_minutes=5)
print(f"5-min averages: {averages}")
```

**Memory profiling with memory_profiler:**
```cmd
pip install memory-profiler psutil matplotlib
```

```python
from memory_profiler import profile
import matplotlib.pyplot as plt

@profile
def memory_intensive_function():
    # Create large list
    data = [i for i in range(1000000)]
    
    # Process data
    processed = [x * 2 for x in data]
    
    # Clean up
    del data
    return processed

# Run with memory profiling
# python -m memory_profiler script.py

# Plot memory usage over time
from memory_profiler import mprofile
# mprofile run script.py
# mprofile plot
```

## Advanced Configuration

### Environment Management

**Environment variables:**
```python
import os
from pathlib import Path
from typing import Optional

class Config:
    """Application configuration from environment variables."""
    
    def __init__(self):
        self.debug = self._get_bool('DEBUG', False)
        self.database_url = self._get_str('DATABASE_URL', 'sqlite:///app.db')
        self.secret_key = self._get_str('SECRET_KEY', self._generate_secret_key())
        self.log_level = self._get_str('LOG_LEVEL', 'INFO')
        self.redis_url = self._get_str('REDIS_URL', 'redis://localhost:6379/0')
        
    def _get_str(self, key: str, default: str = '') -> str:
        return os.environ.get(key, default)
        
    def _get_bool(self, key: str, default: bool = False) -> bool:
        value = os.environ.get(key, '').lower()
        return value in ('true', '1', 'yes', 'on')
        
    def _get_int(self, key: str, default: int = 0) -> int:
        try:
            return int(os.environ.get(key, default))
        except ValueError:
            return default
            
    def _generate_secret_key(self) -> str:
        import secrets
        return secrets.token_urlsafe(32)

# Load configuration
config = Config()
```

**.env file support:**
```cmd
pip install python-dotenv
```

```python
from dotenv import load_dotenv
import os

# Load environment variables from .env file
load_dotenv()

# Now environment variables are available
database_url = os.getenv('DATABASE_URL')
debug_mode = os.getenv('DEBUG', 'False').lower() == 'true'
```

**.env file example:**
```env
# .env
DEBUG=True
DATABASE_URL=postgresql://user:pass@localhost/myapp
SECRET_KEY=your-secret-key-here
LOG_LEVEL=DEBUG
REDIS_URL=redis://localhost:6379/0

# Email configuration
EMAIL_HOST=smtp.company.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_USER=app@company.com
EMAIL_PASSWORD=password

# API Keys
OPENAI_API_KEY=sk-...
STRIPE_SECRET_KEY=sk_test_...
```

### Configuration Management

**YAML configuration:**
```cmd
pip install PyYAML
```

```yaml
# config.yaml
app:
  name: "My Application"
  version: "1.0.0"
  debug: false

database:
  host: "localhost"
  port: 5432
  name: "myapp"
  user: "app_user"
  password: "secure_password"

logging:
  level: "INFO"
  format: "%(asctime)s [%(levelname)s] %(name)s: %(message)s"
  handlers:
    - console
    - file

redis:
  host: "localhost"
  port: 6379
  db: 0

features:
  enable_analytics: true
  enable_caching: true
  max_file_size: 10485760  # 10MB
```

```python
import yaml
from pathlib import Path
from typing import Dict, Any

class ConfigManager:
    def __init__(self, config_file: str = "config.yaml"):
        self.config_file = Path(config_file)
        self.config = self._load_config()
        
    def _load_config(self) -> Dict[str, Any]:
        if not self.config_file.exists():
            raise FileNotFoundError(f"Configuration file {self.config_file} not found")
            
        with open(self.config_file, 'r', encoding='utf-8') as f:
            return yaml.safe_load(f)
            
    def get(self, key: str, default: Any = None) -> Any:
        """Get configuration value using dot notation (e.g., 'database.host')"""
        keys = key.split('.')
        value = self.config
        
        for k in keys:
            if isinstance(value, dict) and k in value:
                value = value[k]
            else:
                return default
                
        return value
        
    def set(self, key: str, value: Any) -> None:
        """Set configuration value using dot notation"""
        keys = key.split('.')
        config_ref = self.config
        
        for k in keys[:-1]:
            if k not in config_ref:
                config_ref[k] = {}
            config_ref = config_ref[k]
            
        config_ref[keys[-1]] = value
        
    def save(self) -> None:
        """Save configuration back to file"""
        with open(self.config_file, 'w', encoding='utf-8') as f:
            yaml.dump(self.config, f, default_flow_style=False, indent=2)

# Usage
config = ConfigManager('config.yaml')

# Get values
db_host = config.get('database.host', 'localhost')
app_name = config.get('app.name', 'Unknown App')
debug_mode = config.get('app.debug', False)

# Set values
config.set('app.debug', True)
config.set('features.new_feature', True)
config.save()
```

### Secrets Management

**Windows Credential Manager integration:**
```cmd
pip install keyring
```

```python
import keyring
from typing import Optional

class SecretManager:
    def __init__(self, service_name: str = "MyPythonApp"):
        self.service_name = service_name
        
    def store_secret(self, key: str, value: str) -> None:
        """Store a secret in Windows Credential Manager"""
        keyring.set_password(self.service_name, key, value)
        
    def get_secret(self, key: str) -> Optional[str]:
        """Retrieve a secret from Windows Credential Manager"""
        return keyring.get_password(self.service_name, key)
        
    def delete_secret(self, key: str) -> None:
        """Delete a secret from Windows Credential Manager"""
        try:
            keyring.delete_password(self.service_name, key)
        except keyring.errors.PasswordDeleteError:
            pass  # Secret doesn't exist

# Usage
secrets = SecretManager()

# Store API key
secrets.store_secret('openai_api_key', 'sk-...')

# Retrieve API key
api_key = secrets.get_secret('openai_api_key')

# Delete when no longer needed
secrets.delete_secret('old_api_key')
```

**Azure Key Vault integration:**
```cmd
pip install azure-keyvault-secrets azure-identity
```

```python
from azure.keyvault.secrets import SecretClient
from azure.identity import DefaultAzureCredential
import os

class AzureSecretManager:
    def __init__(self, vault_url: str):
        credential = DefaultAzureCredential()
        self.client = SecretClient(vault_url=vault_url, credential=credential)
        
    def get_secret(self, secret_name: str) -> str:
        try:
            secret = self.client.get_secret(secret_name)
            return secret.value
        except Exception as e:
            raise ValueError(f"Failed to retrieve secret '{secret_name}': {e}")
            
    def set_secret(self, secret_name: str, secret_value: str) -> None:
        try:
            self.client.set_secret(secret_name, secret_value)
        except Exception as e:
            raise ValueError(f"Failed to store secret '{secret_name}': {e}")

# Usage
vault_url = "https://your-keyvault.vault.azure.net/"
azure_secrets = AzureSecretManager(vault_url)

# Get secret
database_password = azure_secrets.get_secret("database-password")
```

## Resources and Further Reading

### Official Documentation
- **Python.org**: [https://docs.python.org/](https://docs.python.org/)
- **Python Package Index (PyPI)**: [https://pypi.org/](https://pypi.org/)
- **Python Enhancement Proposals (PEPs)**: [https://www.python.org/dev/peps/](https://www.python.org/dev/peps/)

### Enterprise Development
- **Poetry**: [https://python-poetry.org/](https://python-poetry.org/) - Modern dependency management
- **Pipenv**: [https://pipenv.pypa.io/](https://pipenv.pypa.io/) - Virtual environments and package management
- **Conda**: [https://docs.conda.io/](https://docs.conda.io/) - Package and environment management

### Testing and Quality
- **pytest**: [https://docs.pytest.org/](https://docs.pytest.org/)
- **pytest-cov**: [https://pytest-cov.readthedocs.io/](https://pytest-cov.readthedocs.io/)
- **Black**: [https://black.readthedocs.io/](https://black.readthedocs.io/)
- **isort**: [https://pycqa.github.io/isort/](https://pycqa.github.io/isort/)
- **mypy**: [https://mypy.readthedocs.io/](https://mypy.readthedocs.io/)

### Deployment and Packaging
- **PyInstaller**: [https://pyinstaller.readthedocs.io/](https://pyinstaller.readthedocs.io/)
- **Docker**: [https://docs.docker.com/](https://docs.docker.com/)
- **cx_Freeze**: [https://cx-freeze.readthedocs.io/](https://cx-freeze.readthedocs.io/)

### Windows-Specific Resources
- **pywin32**: [https://github.com/mhammond/pywin32](https://github.com/mhammond/pywin32)
- **Windows Python FAQ**: [https://docs.python.org/3/faq/windows.html](https://docs.python.org/3/faq/windows.html)

### Learning Resources
- **Real Python**: [https://realpython.com/](https://realpython.com/)
- **Python Weekly**: [https://pythonweekly.com/](https://pythonweekly.com/)
- **Python.org Tutorial**: [https://docs.python.org/3/tutorial/](https://docs.python.org/3/tutorial/)

### Enterprise Security
- **OWASP Python Security**: [https://owasp.org/www-project-python-security/](https://owasp.org/www-project-python-security/)
- **Bandit Security Linter**: [https://bandit.readthedocs.io/](https://bandit.readthedocs.io/)
- **Safety**: [https://pyup.io/safety/](https://pyup.io/safety/)

---

## Conclusion

This guide provides comprehensive coverage of Python development on Windows 11 Enterprise, from basic installation to advanced deployment strategies. The enterprise focus ensures compatibility with corporate security policies, proxy configurations, and deployment requirements.

For additional support or questions specific to your environment, consult your IT department or visit the [syslogine.cloud](https://syslogine.cloud) documentation portal.

---

*Last updated: September 15, 2025*  
*Document version: 1.0*  
*For updates and corrections, please visit: [https://syslogine.cloud/docs/os/windows/tutorials/php/python-windows-guide](https://syslogine.cloud/docs/os/windows/tutorials/php/python-windows-guide)*