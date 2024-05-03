---
title: "Jetson Nano Setup Guide"
description: "A comprehensive guide to setting up your Jetson Nano."
weight: 1
---

## Introduction

Welcome to the Jetson Nano Setup Guide! This guide will walk you through the process of setting up your Jetson Nano developer kit, from downloading the system image to configuring advanced usage scenarios.

## Download Jetson Nano Image 

Before you begin, you'll need to download the system image for your Jetson Nano model:

- [Jetson Nano 2GB](https://developer.nvidia.com/embedded/l4t/r32_release_v7.1/jp_4.6.1_b110_sd_card/jetson_nano_2gb/jetson-nano-2gb-jp461-sd-card-image.zip)
- [Jetson Nano 4GB](https://developer.nvidia.com/embedded/l4t/r32_release_v7.1/jp_4.6.1_b110_sd_card/jetson_nano/jetson-nano-jp461-sd-card-image.zip)


## Setting up the MicroSD with Ubuntu using balenaEther

1.	Go to this [website](https://developer.nvidia.com/embedded/downloads#?tx=$product,jetson_nano)
2.	Find and download `Jetson Nano Developer Kit SD Card Image`
3.	Download and install [balenaEtcher](https://etcher.balena.io/)
4.	Open `balenaEthcer` 
	1.	Select: `Flash from file`
	2.	Select: `jetson-nano-jp461-sd-card-image.zip`
	3.	Select the MicroSD card 
	4.	Flash!
5.	Place the MicroSD back into the jetson nano and start.

## Fresh Install Setup Guide for Jetson Nano

Once your Jetson Nano board is up and running with Ubuntu Desktop, let's kickstart the setup process by opening the terminal and following these steps:

### Step 1: Update System

First, let's ensure your system is up to date:

```bash
sudo apt update
```

Next, upgrade your Jetson Nano:

```bash
sudo apt upgrade -y
```

During the upgrade process, you may encounter prompts for configuration files.

Select `Y` to install the package maintainer's version. 

```sh
Configuration file '/etc/ld.so.conf.d/nvidia-tegra.conf'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nvidia-tegra.conf (Y/I/N/O/D/Z) [default=N] ? Y
```

Again select `Y` to install the package maintainer's version. 

```sh
Configuration file '/etc/systemd/nv-oem-config-post.sh'
 ==> Deleted (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nv-oem-config-post.sh (Y/I/N/O/D/Z) [default=N] ? Y
```

Additionally, if prompted to restart Docker, select `YES`.

Now, let's perform a distribution upgrade:

```bash
sudo apt dist-upgrade -y
```

### Step 2: Clean Up

Once the upgrade process is complete, let's tidy up by removing old packages:

```bash
sudo apt autoremove -y
```

And finally, let's clean up the cache:

```bash
sudo apt clean
```

### Step 3: Reboot

After these maintenance tasks, it's recommended to reboot your Jetson Nano for changes to take effect:

```bash
sudo reboot now
```


## Install Useful Tools

Here are some essential tools that are handy for almost every project:

```bash
sudo apt install git nano curl wget -y
```


## Uninstall LibreOffice

If you no longer need LibreOffice and want to reclaim some disk space, follow these steps to remove it:

```bash
sudo apt autoremove libreoffice* -y
```

This command will uninstall all LibreOffice packages from your system.

After removing LibreOffice, let's clean up the residual files:

```bash
sudo apt clean
```

This command will clean the package cache, freeing up additional disk space.

Your system is now free of LibreOffice and optimized for your needs.


## Installing pip and pip3

To install both pip and pip3, which are package managers for Python 2 and Python 3 respectively, run the following command:

```bash
sudo apt install python-pip python3-pip -y
```

This command will install pip for Python 2 and pip3 for Python 3 on your system.

You're all set with pip and pip3 installed and ready to manage Python packages!


## Installing Jetson Stats

To install Jetson Stats, a utility for monitoring and controlling NVIDIA Jetson devices, follow these steps:

{{< alert color="warning" title="Warning" >}}Before proceeding, ensure that you have pip3 installed on your system. If not, you can install it using `sudo apt install python3-pip`.{{< /alert >}}

```bash
sudo pip3 install -U jetson-stats
```

This command will install Jetson Stats and ensure that you have the latest version.

After installation, reboot your Jetson Nano to enable the `jtop` command:

```bash
sudo reboot now
```

Once your device has rebooted, reopen the terminal and type the following command to launch Jetson Stats:

```bash
jtop
```

This will open the Jetson Stats interface, allowing you to monitor various aspects of your Jetson Nano's performance.

You're now ready to utilize Jetson Stats for optimizing your Jetson Nano's performance!


## Configuring Jetson Fan to Start at Boot

To ensure your Jetson Nano's fans start automatically at boot, follow these steps:

1. Open and edit the `rc.local` file using the Nano text editor:

```bash
sudo nano /etc/rc.local
```

Paste the following lines into the file:

```sh
#!/bin/bash
sleep 10
sudo /usr/bin/jetson_clocks
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
exit 0
```

2. Next, create and edit the `rc-local.service` file:

```bash
sudo nano /etc/systemd/system/rc-local.service
```

Insert the following content:

```txt
[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

3. Ensure the `rc.local` file has execute permissions:

```bash
sudo chmod +x /etc/rc.local
```

4. Now, enable the `rc-local` service to run on system boot:

```bash
sudo systemctl enable rc-local
```

5. Start the `rc-local` service:

```bash
sudo systemctl start rc-local.service
```

Your Jetson Nano's fans will now start automatically at boot, ensuring optimal cooling performance.


## Increase Swap Space

To increase the swap space on your Jetson Nano, follow these steps:

1. Clone the `resizeSwapMemory` repository:

```bash
git clone https://github.com/JetsonHacksNano/resizeSwapMemory
```

2. Navigate to the cloned repository:

```bash
cd resizeSwapMemory
```

3. Set the entire swap memory size to 8GB:

```bash
./setSwapMemorySize.sh -g 8
```

This will ensure sufficient memory for the OpenCV installation.


## OpenCV Installation Guide

Before installing OpenCV on your Jetson Nano, ensure that your system has sufficient memory by following the steps above to increase swap space if needed.

Next, download the OpenCV installation script:

```bash
wget https://github.com/Qengineering/Install-OpenCV-Jetson-Nano/raw/main/OpenCV-4-8-0.sh
```

Set the appropriate permissions for the script:

```bash
sudo chmod 755 ./OpenCV-4-8-0.sh
```

Run the installation script:

```bash
./OpenCV-4-8-0.sh
```

Once the installation is complete, you can remove the installation script:

```bash
rm OpenCV-4-8-0.sh
```

Finally, you can remove the `dphys-swapfile`:

```bash
sudo /etc/init.d/dphys-swapfile stop
sudo apt-get remove --purge dphys-swapfile
```

As a tip to save additional space, you can remove the OpenCV and OpenCV_contrib directories:

```bash
sudo rm -rf ~/opencv
sudo rm -rf ~/opencv_contrib
```

Congratulations! You've successfully installed OpenCV on your Jetson Nano.


## Install Python 3.12 on Jetson Nano From Source

Python 3.12 brings new features, improvements, and optimizations to the language, making it desirable for developers who want to leverage the latest capabilities. 

To install Python 3.12 on your Jetson Nano from source, follow these steps:


1. Update your system's package list:

```bash
sudo apt update
```

2. Install the necessary dependencies for building Python:

```bash
sudo apt install wget build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev -y
```

3. Create a directory for the Python source code and navigate to it:

```bash
mkdir ./python && cd ./python
```

4. Download the Python source code. Replace `3.12.0` with the desired Python version:

```bash
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
```

5. Extract the downloaded archive:

```bash
tar -xvf Python-3.12.0.tgz
```

6. Navigate to the extracted directory:

```bash
cd Python-3.12.0
```

7. Configure the build with optimizations enabled:

```bash
./configure --enable-optimizations
```

8. Compile and install Python:

```bash
sudo make install
```

9. After completing the installation, reboot your Jetson Nano:

```bash
sudo reboot now
```

After rebooting, Python 3 will be installed on your Jetson Nano from the source code. You can verify the installation by running `python3 --version`.




## Install CrewAI on Jetson Nano

CrewAI is a powerful AI platform designed to assist with a variety of tasks. To install CrewAI on your Jetson Nano, follow these steps:

To install the main CrewAI package, which includes core functionalities, run the following command:

```bash
pip3 install crewai
```

If you also want to install the tools package, which includes a series of helpful tools for your agents, you can use the following command:

```bash
pip3 install 'crewai[tools]'
```

This command will install the main CrewAI package along with additional tools to enhance your CrewAI experience.

Once installed, you can start using CrewAI to develop and deploy AI solutions on your Jetson Nano.


## Make test script for crewAI (Testing)

```bash
mkdir test_ai && cd test_ai
```

```bash
nano .env
```

and then add this
```txt
ANTHROPIC_API_KEY=your_anthropic_api_key
```
Now save and close nano

now let's create our `main.py`
```bash
nano main.py
```

And then add this code below

```python
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew
from langchain.llms import Anthropic
from textwrap import dedent

# Load the API key from the .env file
load_dotenv()
ANTHROPIC_API_KEY = os.getenv("ANTHROPIC_API_KEY")

# Define a simple agent
class SimpleAgent:
    def __init__(self):
        self.Claude = Anthropic(anthropic_api_key=ANTHROPIC_API_KEY, temperature=0.7)

    def create_agent(self):
        return Agent(
            role="Simple Test Agent",
            backstory=dedent("""You are a helpful assistant."""),
            goal=dedent("""Your goal is to assist the user with their query."""),
            allow_delegation=False,
            verbose=True,
            llm=self.Claude,
        )

# Define a simple task
class SimpleTask:
    def __init__(self, user_query):
        self.user_query = user_query

    def create_task(self, agent):
        return Task(
            description=dedent(
                f"""
            Please assist with the following query:
            
            {self.user_query}
        """
            ),
            agent=agent,
        )

# Main function
if __name__ == "__main__":
    print("## Welcome to the Crew AI Test")
    print("-------------------------------")

    user_query = input(dedent("""Enter your query: """))

    simple_agent = SimpleAgent().create_agent()
    simple_task = SimpleTask(user_query).create_task(simple_agent)

    crew = Crew(agents=[simple_agent], tasks=[simple_task], verbose=True)
    result = crew.kickoff()

    print("\n\n########################")
    print("## Here is the result:")
    print("########################\n")
    print(result)
```


