# FiveM Server Setup Guide

Before setting up your FiveM server, ensure that you have the following prerequisites in place.

## Prerequisites

- **Git**: Required if you choose to follow the recommended method of cloning the base server data.
- **xz or xz-utils package**: Needed for extracting server builds.

## Installation

Follow these steps to install and set up your FiveM server:

1. **Create Server Directory**:

   - Create a new directory where you want to set up your FiveM server. For example:
     ```bash
     mkdir -p ~/FXServer/server
     ```

2. **Download Server Build**:

   - Go to the [Linux server build listing](https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/7290-a654bcc2adfa27c4e020fc915a1a6343c3b4f921/fx.tar.xz).
   - Copy the URL for the `fx.tar.xz` file from the listing.
   - Use `wget` to download the server build into your server directory. Replace `<server-build-url>` with the copied URL:
     ```bash
     cd ~/FXServer/server
     wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/7290-a654bcc2adfa27c4e020fc915a1a6343c3b4f921/fx.tar.xz
     ```

3. **Extract Server Build**:

   - Extract the downloaded server build to your server directory. Make sure you have the `xz` package installed (on Debian/Ubuntu, it's in the `xz-utils` package):
     ```bash
     cd ~/FXServer/server
     tar xf fx.tar.xz
     ```

4. **Clone cfx-server-data**:

   - Clone the `cfx-server-data` repository into a separate folder, not within your server binaries folder:
     ```bash
     git clone https://github.com/citizenfx/cfx-server-data.git ~/FXServer/server-data
     ```

5. **Create server.cfg File**:

   - In your `server-data` folder, create a `server.cfg` file. You can copy the example `server.cfg` below into that file.

     ```plaintext
     # This is an example server configuration file.
     # sv_licenseKey should be replaced with your actual license key.

     sv_licenseKey "licenseKeyGoesHere"
     ```

6. **Set License Key**:

   - Open your `server.cfg` file and set the license key using the `sv_licenseKey` parameter.

7. **Run the Server**:

   - Start your FiveM server from the `server-data` folder using the following command:

     ```bash
     cd ~/FXServer/server-data
     bash ~/FXServer/server/run.sh +exec server.cfg
     ```

These steps will set up your FiveM server with the necessary server build, configuration, and license key. You can now run your server using the provided command.
