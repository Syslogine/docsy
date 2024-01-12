---
title: Setting Up Your Own Radio Station on Ubuntu with Icecast and Jetson Nano
linktitle: Radio Station Setup
date: 2024-01-12T12:00:00Z
description: >
  Learn how to set up your own radio station using Icecast on an Ubuntu machine, specifically on a Jetson Nano. Broadcast audio content over the internet with ease.
tags: ["Ubuntu", "Icecast", "Jetson Nano", "Streaming", "Tutorial"]
categories: ["Jetson Nano", "Tutorials"]
---

## Introduction

In this tutorial, we'll guide you through the process of setting up your own radio station using Icecast on an Ubuntu machine, specifically on a Jetson Nano. Icecast is a popular streaming server that allows you to broadcast audio content over the internet.

### Prerequisites

- Ubuntu machine (Jetson Nano, in this case)
- Internet connection

## Step 1: Install Icecast Server

Open a terminal and run the following commands:

```bash
sudo apt-get update
sudo apt-get install icecast2
```

During the installation, you will be prompted to set a password for the admin user.

## Step 2: Configure Icecast

Edit the Icecast configuration file with your preferred text editor:

```bash
sudo nano /etc/icecast2/icecast.xml
```

Update the file with your server details, including the server name, port, and passwords.

## Step 3: Start Icecast

Start the Icecast server with the following command:

```bash
sudo service icecast2 start
```

## Step 4: Set Up a Source Client (Darkice)

Install the Darkice source client:

```bash
sudo apt-get install darkice
```

Configure Darkice by editing its configuration file:

```bash
sudo nano /etc/darkice.cfg
```

Provide the necessary settings, such as server, port, and source password.

## Step 5: Start Darkice

Start the Darkice source client:

```bash
darkice
```

## Step 6: Broadcast Your Audio

Use `ffmpeg` to convert your audio source and send it to the Icecast server. Adjust the parameters accordingly:

```bash
ffmpeg -f pulse -i default -acodec libmp3lame -ab 128k -ar 44100 -content_type audio/mpeg -ice_name "Your Radio Station" -ice_description "Description of your station" -ice_genre "Your preferred genre" -ice_url "http://yourstreamurl" -ice_public 1 -ice_server "localhost:8000" -ice_mount "/yourmountpoint" -ice_user "source" -ice_pass "yoursourcepassword" http://localhost:8000/yourmountpoint
```

## Step 7: Listen to Your Radio Station

Open a media player (e.g., VLC) and connect to your Icecast stream using the URL: `http://localhost:8000/yourmountpoint`.

Congratulations! You've successfully set up your own radio station using Icecast on your Ubuntu machine.

Feel free to customize the configuration based on your preferences and share your streaming URL with others.
