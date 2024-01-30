---
title: "Setting Up a FiveM Server on Debian"
linktitle: "Debian FiveM Setup"
draft: false
description: "A comprehensive guide to setting up a FiveM server on a Debian-based system."
---

# Setting Up a FiveM Server on Debian

Creating a FiveM server on a Debian server involves several steps. This guide will walk you through the process from start to finish.

## Prerequisites

- A server running Debian or a Debian-based Linux distribution.
- Root or sudo access on the server.
- Basic knowledge of Linux command-line interface.

## Step 1: Installing Dependencies

Before installing the FiveM server, you need to install the required dependencies.

1. Update your package lists:
   ```bash
   sudo apt update
   ```

2. Install the necessary packages:
   ```bash
   sudo apt install git curl screen xz-utils wget -y
   ```

## Step 2: Creating a User for FiveM

It's a good practice to run services like FiveM under a separate user.

1. Create a new user:
   ```bash
   sudo adduser fivem
   ```

2. Switch to the new user:
   ```bash
   su - fivem
   ```

## Step 3: Downloading and Preparing FiveM Server Files

1. Download the latest server artifact:
   ```bash
   wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/latest.tar.xz
   ```

2. Extract the server files:
   ```bash
   tar xf latest.tar.xz
   ```

3. Clone the `cfx-server-data` repository from GitHub. This repository contains essential data for your FiveM server:
   ```bash
   git clone https://github.com/citizenfx/cfx-server-data.git
   ```

4. Move the `resources` folder from `cfx-server-data` to your main FiveM server directory:
   ```bash
   mv cfx-server-data/resources /home/fivem/
   ```

5. Remove the now-empty `resources` directory from `cfx-server-data`:
   ```bash
   rm -rf cfx-server-data/resources
   ```

## Step 4: Configuring the Server

1. Create a new configuration file (`server.cfg`):
   ```bash
   nano server.cfg
   ```

   ```cfg
   # Only change the IP if you're using a server with multiple network interfaces, otherwise change the port only.
   endpoint_add_tcp "0.0.0.0:30120"
   endpoint_add_udp "0.0.0.0:30120"

   # These resources will start by default.
   ensure mapmanager
   ensure chat
   ensure spawnmanager
   ensure sessionmanager
   ensure basic-gamemode
   ensure hardcap
   ensure rconlog

   # This allows players to use scripthook-based plugins such as the legacy Lambda Menu.
   # Set this to 1 to allow scripthook. Do note that this does _not_ guarantee players won't be able to use external plugins.
   sv_scriptHookAllowed 0

   # Uncomment this and set a password to enable RCON. Make sure to change the password - it should look like rcon_password "YOURPASSWORD"
   #rcon_password ""

   # A comma-separated list of tags for your server.
   # For example:
   # - sets tags "drifting, cars, racing"
   # Or:
   # - sets tags "roleplay, military, tanks"
   sets tags "default"

   # A valid locale identifier for your server's primary language.
   # For example "en-US", "fr-CA", "nl-NL", "de-DE", "en-GB", "pt-BR"
   sets locale "root-AQ" 
   # please DO replace root-AQ on the line ABOVE with a real language! :)

   # Set an optional server info and connecting banner image url.
   # Size doesn't matter, any banner sized image will be fine.
   #sets banner_detail "https://url.to/image.png"
   #sets banner_connecting "https://url.to/image.png"

   # Set your server's hostname. This is not usually shown anywhere in listings.
   sv_hostname "FXServer, but unconfigured"

   # Set your server's Project Name
   sets sv_projectName "My FXServer Project"

   # Set your server's Project Description
   sets sv_projectDesc "Default FXServer requiring configuration"

   # Set Game Build (https://docs.fivem.net/docs/server-manual/server-commands/#sv_enforcegamebuild-build)
   #sv_enforceGameBuild 2802

   # Nested configs!
   #exec server_internal.cfg

   # Loading a server icon (96x96 PNG file)
   #load_server_icon myLogo.png

   # convars which can be used in scripts
   set temp_convar "hey world!"

   # Remove the `#` from the below line if you want your server to be listed as 'private' in the server browser.
   # Do not edit it if you *do not* want your server listed as 'private'.
   # Check the following url for more detailed information about this:
   # https://docs.fivem.net/docs/server-manual/server-commands/#sv_master1-newvalue
   #sv_master1 ""

   # Add system admins
   add_ace group.admin command allow # allow all commands
   add_ace group.admin command.quit deny # but don't allow quit
   add_principal identifier.fivem:1 group.admin # add the admin to the group

   # enable OneSync (required for server-side state awareness)
   set onesync on

   # Server player slot limit (see https://fivem.net/server-hosting for limits)
   sv_maxclients 48

   # Steam Web API key, if you want to use Steam authentication (https://steamcommunity.com/dev/apikey)
   # -> replace "" with the key
   set steam_webApiKey ""

   # License key for your server (https://keymaster.fivem.net)
   sv_licenseKey changeme
   ```

2. Populate the configuration file. A basic example can be found in the FiveM documentation.

3. Save and exit the editor:
    - Once you have finished editing the file in `nano`, you need to save your changes. To do this, press `Ctrl + O`. This command stands for 'write Out', which is nano's way of saying 'save'.
    - After pressing `Ctrl + O`, nano will ask you to confirm the file name. By default, it will use the name of the file you're editing. Simply press `Enter` to confirm.
    - Now that your changes are saved, you can exit nano. Press `Ctrl + X` to close the editor and return to the command prompt.

## Step 5: Configuring Firewall for FiveM

Before enabling the firewall, it's important to ensure you won't lose remote access to your server, especially if you're using SSH.

1. Check if UFW (Uncomplicated Firewall) is installed:
   ```bash
   sudo apt install ufw
   ```

2. Allow SSH connections to ensure you can still access your server after the firewall is enabled:
   ```bash
   sudo ufw allow 22/tcp
   ```

3. Enable UFW:
   ```bash
   sudo ufw enable
   ```

4. Allow the default FiveM ports. FiveM typically uses ports 30120 and 30110 for server and HTTP server:
   ```bash
   sudo ufw allow 30120/tcp
   sudo ufw allow 30110/tcp
   ```

5. Optionally, if you are using additional ports for specific resources or services, open them similarly:
   ```bash
   sudo ufw allow [YourAdditionalPort]/tcp
   ```

6. Check your UFW status to ensure the rules are applied:
   ```bash
   sudo ufw status
   ```

## Step 6: Running the Server

1. Start the server using `screen` for background execution:
   ```bash
   screen -S fivem-server ./run.sh +exec server.cfg
   ```


cd ~/FXServer/server-data && bash ~/FXServer/server/run.sh +exec server.cfg


## Step 6: Managing Your Server

- To detach from the `screen` session, press `Ctrl+A` then `Ctrl+D`.
- To reattach to the session, use `screen -r fivem-server`.

## Conclusion

You have now set up a FiveM server on Debian. Remember to manage your server responsibly and adhere to the FiveM terms of service.

---

For more advanced configurations and troubleshooting, refer to the [FiveM Documentation](https://docs.fivem.net/).
