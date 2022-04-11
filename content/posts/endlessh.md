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

What is Endlessh? Endlessh is a network based service that catches port scanners and nefarious users by sticking them in a permanent loop. Try as they might the terminal will never proceed to the authentication part of the shell.

Lets install!

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

Congratulations, SSH clients will now sit at blank screens trying to connect forever.

Endlessh also has a config available. You can change ports, timers, max clients etc. The biggest use of the config is having Endlessh run at boot.

My homelab SSH listens on port 2222, I forward that to port 22 on my router, the standard SSH port. I run many peering apps (like Storj and Sia) so as of writing this my IP sees 8,095 connections with 67 concurrent connections in 24 hours (7,500 come from China alone).

As a side note, if you wanted to prevent this you would need a Geo-IP filter / firewall to block IP ranges from getting near your system. It isn't uncommon to hear users blocking entire countries from their systems both inbound and outbound (China, Russia, NK etc.). An at home solution for this is pfSense/OPNsense. Once I have another ethernet port up on my homelab I can write more about this.

Another version of Endlessh I would like to share is endlessh-go.

[shizunge on Github](https://github.com/shizunge) remade Endlessh in golang with the added feature of exporting metrics to Prometheus. From there you can input them into Grafana for a nice visual display of what is happening. Endlessh-go will also convert IPs into Geohashes to show you where connecting IPs are coming from.

![endlessh-go dashboard](https://raw.githubusercontent.com/shizunge/endlessh-go/master/dashboard/screenshot.png)

To get set up simply run:

```bash
docker run -d --name endlessh -p 2222:2222 shizunge/endlessh-go -logtostderr -v=1
```

This image provides a working version of Endlessh that will slow down anyone trying to connect to your SSH port. Running ```docker logs endlessh``` will show you results if you have any internet-facing connectable devices. This is part and parcel of being connectable to the outside world.  Make sure to forward the port on your router, you will have it on 22 to the outside world as this is the standard SSH port.

If you do not have a Grafana setup yet you can use the [example full stack](https://github.com/shizunge/endlessh-go/blob/master/examples/README.md) provided by shizunge for endlessh-go. If you clone their repo and go to examples you will see an available script to have both Prometheus and Grafana running. You are required to import the dashboard but this is non-trivial (create -> import -> 15156). Grafana runs on port 3000, after login you can simply select the endlessh dashboard and see whats happening.

### References

* <https://github.com/skeeto/endlessh>
* <https://github.com/shizunge/endlessh-go>
