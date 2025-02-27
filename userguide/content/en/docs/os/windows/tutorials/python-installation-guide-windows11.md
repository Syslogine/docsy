---
title: "Installing Python on Windows 11"
description: "Guide to installing and managing multiple Python versions on Windows 11"
weight: 1
---

![alt text](images/os/windows/python.webp) 

## Prerequisites
- A Windows 11 machine with administrative privileges
- A stable internet connection
- At least 100MB of free disk space

## Method 1: Standard Installation

### Step 1: Download Python
1. Open a web browser and go to the official Python website: [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. Click on the "Download Python X.X.X" button (the latest version)
   - Alternatively, scroll down to "Looking for a specific release?" to select an older version
3. Choose the appropriate installer:
   - Windows installer (64-bit) is recommended for most users
   - Windows installer (32-bit) for older systems

### Step 2: Run the Installer
1. Locate the downloaded file (typically in your Downloads folder)
2. Right-click the installer and select "Run as administrator"
3. **Important**: Check the box that says "Add Python X.X to PATH"
4. Select "Customize installation" for more options (recommended)

### Step 3: Customize the Installation
1. In the "Optional Features" screen, ensure these options are selected:
   - pip
   - tcl/tk and IDLE
   - Python test suite
   - py launcher
2. Click "Next" to continue
3. In the "Advanced Options" screen, select:
   - Install for all users
   - Associate files with Python
   - Create shortcuts for installed applications
   - Add Python to environment variables
   - Precompile standard library
4. Customize the installation location if desired (e.g., `C:\Python310`)
5. Click "Install" to begin the installation process

### Step 4: Verify the Installation
1. Open Command Prompt (Win + R, type "cmd", press Enter)
2. Type the following commands to verify Python and pip are installed:
   ```cmd
   python --version
   pip --version
   ```
3. If both commands return version numbers, Python is installed correctly

## Method 2: Using Windows Store (Easier but Limited)

1. Open the Microsoft Store app
2. Search for "Python"
3. Select the version you want to install
4. Click "Get" or "Install"
5. Once installed, you can verify by opening Command Prompt and typing:
   ```cmd
   python --version
   ```

## Method 3: Managing Multiple Python Versions

### Option A: Using Python Launcher (py)

The Python Launcher is installed by default with modern Python installations and helps manage multiple versions.

1. Install multiple Python versions using the standard installation method
2. Use the `py` command with specific version flags:
   ```cmd
   py -3.9 script.py    # Runs with Python 3.9
   py -3.10 script.py   # Runs with Python 3.10
   py -3.11 script.py   # Runs with Python 3.11
   ```
3. Check available versions:
   ```cmd
   py --list
   ```
4. Set a default version:
   ```cmd
   py -3.10 -m pip install --upgrade pip
   ```

### Option B: Using Virtual Environments (Recommended for Projects)

1. Install at least one version of Python using the standard method
2. Create project-specific virtual environments:
   ```cmd
   # Create a virtual environment with the default Python version
   python -m venv project_env

   # Create a virtual environment with a specific Python version
   C:\Python39\python.exe -m venv project_env_py39
   ```
3. Activate the virtual environment:
   ```cmd
   # For Command Prompt
   project_env\Scripts\activate.bat

   # For PowerShell
   project_env\Scripts\Activate.ps1
   ```
4. Install project-specific packages in the activated environment:
   ```cmd
   pip install package_name
   ```
5. Deactivate when done:
   ```cmd
   deactivate
   ```

### Option C: Using Conda (Best for Data Science)

1. Download and install Miniconda from [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
2. Open Anaconda Prompt from the Start menu
3. Create environments with specific Python versions:
   ```cmd
   conda create -n py39env python=3.9
   conda create -n py310env python=3.10
   ```
4. Activate an environment:
   ```cmd
   conda activate py39env
   ```
5. Install packages:
   ```cmd
   conda install numpy pandas
   # or
   pip install package_name
   ```
6. Switch between environments as needed:
   ```cmd
   conda deactivate
   conda activate py310env
   ```

## Option D: Using pyenv-win (Developer-Friendly)

1. Install pyenv-win using PowerShell:
   ```powershell
   Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
   ```
2. Restart your terminal
3. Install Python versions:
   ```cmd
   pyenv install 3.9.13
   pyenv install 3.10.11
   pyenv install 3.11.7
   ```
4. Set a global version:
   ```cmd
   pyenv global 3.10.11
   ```
5. Set a local version for a specific project:
   ```cmd
   cd my_project
   pyenv local 3.9.13
   ```

## Troubleshooting Common Issues

### "Python is not recognized as an internal or external command"
1. Verify Python is added to PATH:
   - Press Win + X and select "System"
   - Click "Advanced system settings"
   - Click "Environment Variables"
   - Under "System variables", find and edit "Path"
   - Ensure Python paths (e.g., `C:\Python310` and `C:\Python310\Scripts`) are included
2. If missing, add them manually and restart Command Prompt

### Permission Issues
- Always run the installer as administrator
- If using pip gives permission errors, try:
  ```cmd
  pip install --user package_name
  ```

### Multiple Python Versions Conflict
- Use full paths to Python executables:
  ```cmd
  C:\Python39\python.exe script.py
  C:\Python310\python.exe script.py
  ```
- Or use the Python Launcher (py) with version flags as described above

## Best Practices

1. **Use virtual environments for all projects**
   - Keeps dependencies isolated
   - Prevents version conflicts
   - Makes projects portable

2. **Keep Python updated**
   ```cmd
   pip install --upgrade pip
   ```

3. **Document Python version requirements**
   - Create a `requirements.txt` file for each project:
     ```cmd
     pip freeze > requirements.txt
     ```

4. **Consider using .python-version files**
   - Create a file named `.python-version` in your project directory
   - Add the Python version you need (e.g., `3.9.13`)
   - Tools like pyenv-win will automatically use that version

## Conclusion

You now have multiple options for installing and managing different Python versions on Windows 11. Choose the approach that best fits your workflow:
- Standard installation for casual use
- Python Launcher for simple version switching
- Virtual environments for project isolation
- Conda for data science work
- pyenv-win for more advanced version management

By properly managing Python versions, you can ensure compatibility with different projects and libraries while maintaining a clean development environment.