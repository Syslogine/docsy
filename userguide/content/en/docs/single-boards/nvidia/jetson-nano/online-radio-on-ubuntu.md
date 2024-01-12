---
title: Listening to Online Radio Stations on Ubuntu
linktitle: Online Radio on Ubuntu
date: 2024-01-12T12:00:00Z
description: >
  Explore how to listen to online radio stations on your Ubuntu machine using various command-line tools such as mpv, radiotray, and radio-browser-cli.
tags: ["Ubuntu", "Radio", "mpv", "radiotray", "radio-browser", "Tutorial"]
categories: ["Ubuntu", "Radio"]
menu: main
---

## Option 1: Using mpv

### Install mpv

Ensure you have `mpv` installed:

```bash
sudo apt-get install mpv
```

### Listen to a Dutch Radio Station

Replace the URL with the streaming URL of the desired radio station. For example, to listen to NPO Radio 1 (Dutch):

```bash
mpv http://icecast.omroep.nl/radio1-bb-mp3
```

## Option 2: Using radiotray

### Install radiotray

```bash
sudo apt-get install radiotray
```

### Open Radiotray

Open Radiotray from your applications menu and browse through different radio stations based on categories and genres.

## Option 3: Using radio-browser-cli

### Install radio-browser-cli

```bash
sudo apt-get install radio-browser-cli
```

### List and Play Radio Stations

```bash
radiobrowser
```

Navigate through different countries and genres to find the radio station you want to listen to.

## Conclusion

Enjoy exploring and listening to a variety of online radio stations on your Ubuntu machine using these command-line tools. Customize your listening experience by discovering stations from different countries and genres.