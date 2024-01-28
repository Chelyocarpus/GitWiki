---
description: Laziness wins
---

# Install Linux for Dualboot without CD/DVD or USB-Drive

When you don't want to burn a CD/DVD (or have an optical drive) or don't have a free USB-Stick / Drive on hand, this is the way.

## Prerequisites

There are as many Linux distributions as there are ice cream flavours, so get your favourite one.

If you don't know any or can't decide which one to take here's a small selection:

<table><thead><tr><th width="326">Overview</th><th>Download Page</th></tr></thead><tbody><tr><td><a href="https://linuxmint.com/">Linux Mint</a></td><td><a href="https://linuxmint.com/download.php">Download Page</a></td></tr><tr><td><a href="https://pop.system76.com/">Pop!_OS</a></td><td><a href="https://pop.system76.com/">Download Page</a></td></tr><tr><td><a href="https://kde.org/de/plasma-desktop/">Plasma</a></td><td><a href="https://kde.org/de/distributions/">Download Page</a></td></tr><tr><td><a href="https://zorin.com/os/">Zorin OS</a></td><td><a href="https://zorin.com/os/download/">Download Page</a></td></tr></tbody></table>

At this point you should be downloading a 1-3 GB big .iso file.

<figure><img src="../../.gitbook/assets/iso dl.png" alt="The picture shows the progress of a Linux Mint iso file download"><figcaption><p>The picture shows the progress of a Linux Mint iso file download</p></figcaption></figure>

## &#x20;Disk partitioning

While the file is downloading we can use the time to create two disk partitions (=split the hard drive) so we don't overwrite Windows nor important files. One of these partitions will also be used to install Linux.

### 1. Open Windows Disk Management

There are a few ways to open Windows Disk Management

### 2. Create a \~5 GB disk partition with the **fat32** file format

This partition will be used as a replacement for the missing CD/DVD or USB-Drive/Stick. It's basically a built-in USB-Drive, hence the **fat32** file format. Since we are just going to Copy\&Paste the content of the 1-3 GB big .iso file a 5 GB disk partition should be more than enough.

### 3. Create a disk partition for the Linux OS&#x20;

This partition will be used for the Linux operating system (like C: for Windows) and should have a size of at least 20 GB. If you want to install many programs/apps or games on Linux, you should increase the size accordingly. But don't think too hard, we can still change the size after installation.

## Create installation medium



## Reboot into UEFI OS

## Linux Installation

## Sources

[https://askubuntu.com/a/1357348](https://askubuntu.com/a/1357348)
