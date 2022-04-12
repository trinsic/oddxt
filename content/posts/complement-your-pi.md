---
title: "Dietpi - complement your pi"
date: 2022-04-04
description: "Dietpi - the extremely lightweight Debian OS, highly optimized for minimal CPU and RAM resource usage, ensuring your SBC always runs at its maximum potential."
tags: ["linux", "RPi"]
author: "Mark Antony"
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "posts/images/dietpi.cover.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

Today I will show you Dietpi, my favorite Raspberry Pi operating system (OS). Dietpi is a lightweight OS built for single board computers (SBC). It is a stripped back version of Debian, on the same grounds as Raspbian.

<p align="center">
<img src="../images/dietpi.logo.png" />
</p>

Dietpi bundles a range of tools to help you manage the system with easy setup of software for your device. This OS is designed to maximize performance for a range of SBC devices but will also work in virtual environments and x86 systems.

![Dietpi Terminal](../images/dietpi.terminal.png)

As you can see, Dietpi comes with some working scripts to help you get your system running.

```dietpi-launcher``` is a collection of all the scripts they have available.

```dietpi-config``` is device settings you can change. They cater to a wide range of devices, so some settings will be specific to your device.

```dietpi-software``` is there auto-installer. To date they have 114 pieces of software that can be installed with little user input.

Popular software includes media centers, downloaders, self-hosting, backups, VPNs, Docker etc. You're not limited to this software (you can install anything yourself) but it makes throwing up a system easy.

From my years of using a Raspberry Pi 3B I want to share some of my use cases:

#### Pi-Hole + Unbound recursive DNS server
One of my all-time favorites is running an adblocker/recursive dns server. Pi-Hole can be used in a number of ways but I always ran it as the DHCP server for my network. Pi-Hole's interface also contains a good set of information to show you an overview of your devices and their use.

+ Adblocking is done network wide and with a good list you can block a majority of all advertising online. I recommend OISD, maintained by Stephan van Ruth over on his website https://oisd.nl. His block lists are designed for everyone, rather than blocking everything and annoying your family members, these block lists will block most of the bad stuff without breaking shopping or social networking.

+ Unbound is a recursive DNS server. Instead of using your ISP's DNS, Unbound will contact the DNS root servers directly, then Unbound and Pi-Hole can cache your often used DNS hits. Unbound also prefetch's DNS so it can keep the cache pool full, giving you fast and secure results.


#### Media downloader
The Pi 3B was my workhorse for many years, running Kodi, Sonarr, Radarr, Transmission, and Jackett. With this setup I was able to automate all media consumption from a single SBC under my TV. Performance was not important here, media was stored externally and the CPU would often be pegged while things were happening, but it never crashed doing its thing. 

---
The above setups can be achieved with Dietpi in just a matter of minutes. All the software is installed directly to the system and configs are preconfigured for an optimal setup on low powered SBC devices.

Since SBC devices mostly use SD cards you generally need to be careful writing too much data to them. Once again Dietpi's solution is to minimize logging and everything else is placed into RAM and written less to the SD card. They even have scripts for Sonarr and Radarr to minimize read/writes to the SD card and disks, allowing your storage disks to sleep.

In the end, Dietpi will complement your SBC device. It will maximize performance, lower power usage and generally stabilize your devices for long-term use. I'm a huge fan.

### References

* <https://dietpi.com>
* <https://github.com/MichaIng/DietPi>