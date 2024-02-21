---
linktitle: Downloads
title: Debian Downloads
categories: ["debian"]
tags: ["debian", "downloads"]
weight: 3
description: >
  Access the latest, upcoming, and archival Debian ISO images. Find direct download links, torrents, and essential verification instructions.
---

# Debian Downloads

Welcome to the comprehensive Debian downloads page, where you can find direct ISO links and torrents for the latest, upcoming, and archival versions of Debian. This section is designed to make it easy for you to access Debian ISO images for various architectures, ensuring you get the version that best fits your needs.

## Latest Debian Release: Debian 12 "Bookworm"

Debian 12, known as "Bookworm," is at the forefront of Debian stable releases, incorporating the latest software advancements and security enhancements.

### ISO Direct Downloads

- **Debian 12 Bookworm (64-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.0.0-amd64-netinst.iso)
- **Debian 12 Bookworm (32-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/debian-cd/current/i386/iso-cd/debian-12.0.0-i386-netinst.iso)

### Torrent Downloads

- **64-bit PC (DVD):** [Torrents 🌊](https://cdimage.debian.org/debian-cd/current/amd64/bt-dvd/)
- **32-bit PC (DVD):** [Torrents 🌊](https://cdimage.debian.org/debian-cd/current/i386/bt-dvd/)
- **64-bit PC (CD):** [Torrents 🌊](https://cdimage.debian.org/debian-cd/current/amd64/bt-cd/)
- **32-bit PC (CD):** [Torrents 🌊](https://cdimage.debian.org/debian-cd/current/i386/bt-cd/)

Discover [what's new in Debian 12 "Bookworm"](https://www.debian.org/releases/bookworm/amd64/release-notes/) to explore the latest features and improvements.

## Previous Debian Release: Debian 11 "Bullseye"

Debian 11, or "Bullseye," provides a stable foundation with robust features and security, serving as the previous major release.

### ISO Direct Downloads

- **Debian 11.6 Bullseye (64-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.6.0-amd64-netinst.iso)
- **Debian 11.6 Bullseye (32-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/debian-cd/current/i386/iso-cd/debian-11.6.0-i386-netinst.iso)

### Torrent Downloads

- **64-bit PC (DVD):** [Torrents](https://cdimage.debian.org/cdimage/archive/11.6.0/amd64/bt-dvd/)
- **32-bit PC (DVD):** [Torrents](https://cdimage.debian.org/cdimage/archive/11.6.0/i386/bt-dvd/)
- **64-bit PC (CD):** [Torrents](https://cdimage.debian.org/cdimage/archive/11.6.0/amd64/bt-cd/)
- **32-bit PC (CD):** [Torrents](https://cdimage.debian.org/cdimage/archive/11.6.0/i386/bt-cd/)

## Debian 10 "Buster"

As the oldstable release, Debian 10 "Buster" continues to receive security updates, ensuring its reliability for existing users.

### ISO Direct Downloads

- **Debian 10.12 Buster (64-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/cdimage/archive/10.12.0/amd64/iso-cd/debian-10.12.0-amd64-netinst.iso)
- **Debian 10.12 Buster (32-bit PC netinst iso):** [Download 📥](https://cdimage.debian.org/cdimage/archive/10.12.0/i386/iso-cd/debian-10.12.0-i386-netinst.iso)

### Torrent Downloads

- **64-bit PC (DVD):** [Torrents 🌊](https://cdimage.debian.org/cdimage/archive/10.12.0/amd64/bt-dvd/)
- **32-bit PC (DVD):** [Torrents 🌊](https://cdimage.debian.org/cdimage/archive/10.12.0/i386/bt-dvd/)
- **64-bit PC (CD):** [Torrents 🌊](https://cdimage.debian.org/cdimage/archive/10.12.0/amd64/bt-cd/)
- **32-bit PC (CD):** [Torrents 🌊](https://cdimage.debian.org/cdimage/archive/10.12.0/i386/bt-cd/)

## Note on Using Torrents

Using torrents is highly recommended for downloading large files. This method speeds up the download process by sharing the load among multiple peers, while also easing the demand on Debian's servers. Make sure you have a torrent client installed to utilize these links.

## Verifying Downloads

Ensuring the integrity and authenticity of your downloaded ISO images is essential. Follow these steps to verify your downloads:

1. **Download the Checksum File**: Locate and download the `SHA256SUMS` and `SHA256SUMS.sign` files from the same directory as your ISO.
2. **Verify the Checksum**:
   ```shell
   sha256sum -c SHA256SUMS 2>&1 | grep OK
   ```
3. **Verify the Signature**:
   ```shell
   gpg --verify SHA256SUMS.sign SHA256SUMS
   ```

For a comprehensive verification guide, visit the [Debian CD verification page](https://www.debian.org/CD/verify).

Seeking further assistance? The [Debian support page](https://www.debian.org/support) and [Debian forums](https://forums.debian.net/) are excellent resources for community support.

For more detailed information on the downloading and installation process, please consult the [official Debian installation guide](https://www.debian.org/releases/stable/installmanual).