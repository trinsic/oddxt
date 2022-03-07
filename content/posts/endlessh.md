---
title: "Endlessh - blackholing port scanners"
description: "Endlessh is an SSH tarpit that very slowly sends an endless, random SSH banner."
date: "2022-02-15"
author: "Mark Antony"
tags: ["linux", "ssh"]
cover:
    image: "posts/images/endlessh.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
ShowToc: false
TocOpen: false
draft: false
ShowToc: false
TocOpen: true
---

### Intro

Endlessh is a network service that opens a network socket to purposefully catch port scanners and other nefarious users into getting stuck in a permanent loop. They can try again and again to connect but the terminal will never proceed to the authentication part of the shell.

So lets install it.

```bash
git clone https://github.com/skeeto/endlessh
cd endlessh
make && make install
```

 > A precompiled binary is also available: [endlessh-1.0.tar.xz](https://github.com/skeeto/endlessh/releases/download/1.0/endlessh-1.0.tar.xz)

After cloning the repo, here’s how you can try it out for yourself (default port 2222):

```bash
./endlessh &
ssh -p2222 localhost
```

Congratulations, your SSH client will now sit at a blank screen trying to connect forever.

Endlessh also has a config file available, you can change ports, timers, max clients etc. Most of this is not important as the defaults are good enough, if you enable at boot the settings could be of some help.

My homelab listens on port 2222, which I forward to port 22 on my router. As of writing this my IP is hit with 8095 connections with 67 concurrent connections in the last 24 hours, 7500 come from China alone. To actually stop this from happening you would need a Geo-IP filter / firewall so you can straight up block entire IP blocks from getting near your system. It isn't uncommon to hear users blocking entire countries from their systems both inbound and outbound (China, Russia, NK etc.). An at home solution for this is pfSense. Once I have another ethernet port up on my homelab I can write about this.

Another version of endlessh I would like to share is endlessh-go.

[shizunge on Github](https://github.com/shizunge) has remade endlessh in golang, which can export its metrics to Prometheus, and further on to Grafana for a nice visual display of what is happening.

![endlessh-go dashboard](https://raw.githubusercontent.com/shizunge/endlessh-go/master/dashboard/screenshot.png)

This version of endlessh will also translate IPs to Geohashes and show you where the connecting IPs are coming from. Best of all, it has a docker image, making install super easy! When it comes to testing out software I love when a docker image is available. Especially with software that requires dependencies I don't often use (sorry golang!)

To get set up simply run:

```bash
docker run -d --name endlessh -p 2222:2222 shizunge/endlessh-go -logtostderr -v=1
```

This image provides a working version of endlessh that will instantly start slowing down anyone trying to connect to you. Running ```docker logs endlessh``` will show you results instantly if you have any internet-facing connectable devices, this is part and parcel for being connectable to the outside world.  Make sure to forward the port on your router, ideally you will have it on 22 to the outside world as this is the standard SSH port.

If you do not have a Grafana setup yet you can use the [example full stack](https://github.com/shizunge/endlessh-go/blob/master/examples/README.md) provided by shizunge for endlessh-go. If you clone their repo and go to examples you will see an available script to have both Prometheus and Grafana running. You are required to import the dashboard but this is non-trivial (create -> import -> 15156). Grafana runs on port 3000, after login you can simply select the endlessh dashboard and see whats happening.

### References

* <https://github.com/skeeto/endlessh>
* <https://github.com/shizunge/endlessh-go>
