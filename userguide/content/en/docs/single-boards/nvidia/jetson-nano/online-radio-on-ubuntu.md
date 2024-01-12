---
title: Advanced Online Radio Listening on Ubuntu
linktitle: Advanced Radio Setup
date: 2024-01-12T12:00:00Z
description: >
  Dive deeper into listening to online radio stations on your Ubuntu machine using advanced features of command-line tools such as mpv, radiotray, and radio-browser-cli.
tags: ["Ubuntu", "Radio", "mpv", "radiotray", "radio-browser", "Tutorial", "Advanced"]
categories: ["Ubuntu", "Radio"]
---

## Option 1: Using mpv

### Install mpv with Advanced Configuration

Ensure you have `mpv` installed with advanced audio options:

```bash
sudo apt-get install mpv
```

Configure advanced audio settings for optimal streaming:

```bash
echo "ao=alsa" >> ~/.config/mpv/mpv.conf
```

### Listen to a Dutch Radio Station with Quality Settings

Replace the URL with the streaming URL of the desired radio station. For example, to listen to NPO Radio 1 (Dutch) with high-quality settings:

```bash
mpv --no-cache --untimed http://icecast.omroep.nl/radio1-bb-mp3
```

## Option 2: Using radiotray

### Install radiotray with Custom Stations

```bash
sudo apt-get install radiotray
```

Create a custom station list for Radiotray:

```bash
echo "NPO Radio 1 | http://icecast.omroep.nl/radio1-bb-mp3" >> ~/.config/radiotray/bookmarks.xml
```

Open Radiotray and enjoy your custom station list.

## Option 3: Using radio-browser-cli

### Install radio-browser-cli with Advanced Search

```bash
sudo apt-get install radio-browser-cli
```

Search for stations by country, genre, and bitrate:

```bash
radiobrowser -c Netherlands -g Pop -b 128
```

Explore advanced search options to discover stations tailored to your preferences.

## Conclusion

Congratulations! You've delved into advanced settings for listening to online radio on your Ubuntu machine. Tailor your experience, whether it's adjusting audio configurations, creating custom station lists, or exploring radio stations with specific criteria. Enjoy the diverse world of online radio with these advanced tools.
