---
title: "Installing Nginx on Windows 11"
description: "Complete guide to installing and configuring Nginx on Windows 11"
weight: 1
---

![alt text](images/os/windows/nginx.webp) 

## Prerequisites
- A Windows 11 machine with administrative privileges
- A stable internet connection
- At least 50MB of free disk space

## Step 1: Download Nginx
1. Open a web browser and go to the official Nginx website: [https://nginx.org/en/download.html](https://nginx.org/en/download.html)
2. Under the **Mainline version** section, download the latest stable Windows zip file (`nginx-x.x.x.zip`).
   - Note: The mainline version contains the latest features, while the stable version prioritizes reliability.

## Step 2: Extract the Nginx Files
1. Locate the downloaded zip file in your **Downloads** folder.
2. Right-click the file and select **Extract All...**.
3. Choose a destination folder (e.g., `C:\nginx`) and click **Extract**.
   - Tip: Avoid installing in folders with spaces in the path (like "Program Files") to prevent potential issues.

## Step 3: Configure Nginx
1. Navigate to the extracted folder (`C:\nginx`).
2. Open the `conf` folder and locate `nginx.conf`.
3. Open `nginx.conf` in a text editor like Notepad or VS Code.
4. Important settings you might want to modify:
   - `listen` directive (line ~36) to change the default port from 80
   - `server_name` directive to set your domain name
   - `root` directive to point to your website files
   - `worker_processes` (line ~2) to match your CPU cores for better performance

Example configuration for a basic website:
```nginx
server {
    listen       80;
    server_name  example.com www.example.com;
    
    location / {
        root   C:/websites/mysite;
        index  index.html index.htm;
    }
}
```

## Step 4: Start Nginx
1. Open **Command Prompt** as Administrator (right-click on Command Prompt and select "Run as administrator").
2. Navigate to the Nginx directory using the command:
   ```sh
   cd C:\nginx
   ```
3. Start the Nginx server with:
   ```sh
   start nginx
   ```
4. To verify that Nginx is running:
   - Open a web browser and go to `http://localhost`
   - You should see the Nginx welcome page
   - Alternatively, check if the Nginx process is running with `tasklist /fi "imagename eq nginx.exe"`

## Step 5: Manage Nginx
- **Stop Nginx**:
  ```sh
  nginx -s stop
  ```
- **Reload configuration** (after making changes):
  ```sh
  nginx -s reload
  ```
- **Quit gracefully** (wait for workers to finish):
  ```sh
  nginx -s quit
  ```
- **Test configuration validity**:
  ```sh
  nginx -t
  ```

## Step 6: Add Nginx to System Path
To run Nginx commands from any location:
1. Press **Win + X** and select **System**.
2. Click **Advanced system settings** on the right.
3. Click **Environment Variables** button.
4. Under **System Variables**, select `Path` and click **Edit**.
5. Click **New** and add the full path to your Nginx installation (e.g., `C:\nginx`).
6. Click **OK** to save all changes.

## Step 7: Set Up Nginx as a Windows Service (Recommended)
Installing Nginx as a service allows it to start automatically with Windows:

1. Download the Windows Service Wrapper (nssm) from [https://nssm.cc/download](https://nssm.cc/download)
2. Extract the zip file and navigate to the appropriate folder (32 or 64-bit)
3. Open Command Prompt as Administrator and navigate to the nssm folder
4. Install Nginx as a service:
   ```sh
   nssm install nginx
   ```
5. In the NSSM dialog:
   - Set the **Path** to `C:\nginx\nginx.exe`
   - Set **Startup directory** to `C:\nginx`
   - Click **Install service**
6. Now you can manage Nginx with:
   ```sh
   net start nginx
   net stop nginx
   ```

## Troubleshooting
- **Port 80 already in use**: Change the port in `nginx.conf` or stop the service using port 80 (often IIS or Skype)
- **Access denied errors**: Ensure you're running commands as Administrator
- **Configuration errors**: Run `nginx -t` to validate your configuration
- **Nginx won't start**: Check the error logs in `C:\nginx\logs\error.log`
- **404 errors**: Verify your path settings in the configuration and ensure files exist

## Security Considerations
- Change default error pages to avoid revealing server information
- Implement SSL/TLS for secure connections
- Limit access to sensitive directories
- Consider adding basic authentication for admin areas

## Conclusion
You have successfully installed and configured Nginx on Windows 11. You can now use it as a web server, reverse proxy, load balancer, or caching server for your applications.

## Further Resources
- [Official Nginx Documentation](https://nginx.org/en/docs/)
- [Nginx Windows-specific notes](https://nginx.org/en/docs/windows.html)
- [Nginx Beginners Guide](https://nginx.org/en/docs/beginners_guide.html)
