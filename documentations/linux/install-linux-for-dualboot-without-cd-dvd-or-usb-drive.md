---
description: Laziness wins
---

# 🔧 Install Linux for Dualboot without CD/DVD or USB-Drive

When you don't want to burn a CD/DVD (or have an optical drive) or don't have a free USB-Stick / Drive on hand, this is the way.

## Prerequisites

There are as many Linux distributions as there are ice cream flavours, so get your favourite one.

If you don't know any or can't decide which one to take here's a small selection:

| Overview                                     | Download Page                                       |
| -------------------------------------------- | --------------------------------------------------- |
| [Linux Mint](https://linuxmint.com/)         | [Download Page](https://linuxmint.com/download.php) |
| [Pop!\_OS](https://pop.system76.com/)        | [Download Page](https://pop.system76.com/)          |
| [Plasma](https://kde.org/de/plasma-desktop/) | [Download Page](https://kde.org/de/distributions/)  |
| [Zorin OS](https://zorin.com/os/)            | [Download Page](https://zorin.com/os/download/)     |

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
