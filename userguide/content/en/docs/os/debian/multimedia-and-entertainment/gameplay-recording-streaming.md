---
title: "Recording and Streaming Gameplay"
description: "Guide on recording and streaming gameplay on Debian systems using software like OBS Studio or SimpleScreenRecorder."
icon: "code"
draft: false
toc: true
weight: 1
---

## Overview

Recording and streaming gameplay on Debian systems can be achieved using software applications like OBS Studio or SimpleScreenRecorder. This tutorial provides step-by-step instructions for setting up, configuring, and using these tools to capture and broadcast gameplay footage on Debian.

## Software Installation

### 1. **Install OBS Studio**

   OBS Studio is a popular open-source software for recording and streaming. Install it using the following commands:

   ```bash
   sudo apt update
   sudo apt install -y obs-studio
   ```

### 2. **Install SimpleScreenRecorder**

   SimpleScreenRecorder is another lightweight tool for recording gameplay. Install it with:

   ```bash
   sudo apt update
   sudo apt install -y simplescreenrecorder
   ```

## Recording Gameplay with OBS Studio

### 1. **Launch OBS Studio**

   Open OBS Studio from the application menu or by running `obs-studio` in the terminal.

### 2. **Set Up Scene**

   - Click on the "+" icon under the "Scenes" box to create a new scene.
   - Add sources like game capture, window capture, or display capture to capture your gameplay.

### 3. **Configure Settings**

   - Navigate to "Settings" and configure video and audio settings according to your preferences.
   - Adjust output settings for recording format, bitrate, and quality.

### 4. **Start Recording**

   - Click on the "Start Recording" button to begin capturing gameplay footage.

## Recording Gameplay with SimpleScreenRecorder

### 1. **Launch SimpleScreenRecorder**

   Open SimpleScreenRecorder from the application menu or by running `simplescreenrecorder` in the terminal.

### 2. **Configure Recording**

   - Choose the screen area to record (full screen, specific window, or custom region).
   - Adjust audio settings for capturing system sound and microphone input.

### 3. **Start Recording**

   - Click on the "Record" button to start recording gameplay.

## Streaming Gameplay with OBS Studio

### 1. **Configure Streaming Settings**

   - Go to "Settings" > "Stream" and enter your streaming platform's stream key (e.g., Twitch, YouTube).
   - Adjust other streaming settings like bitrate, encoder, and server.

### 2. **Start Streaming**

   - Click on the "Start Streaming" button to begin broadcasting gameplay to your streaming platform.

## Conclusion

By following this tutorial, you can easily record and stream gameplay on your Debian system using software like OBS Studio or SimpleScreenRecorder. Whether you're a content creator sharing your gaming adventures or a streamer engaging with your audience, these tools offer versatile features and customization options to enhance your gaming content.
