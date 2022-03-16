---
title: "Collection of Docker scripts"
description: "A list of available docker images I use on my homelab servers."
author: "Mark Antony"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: true
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
weight: 10
cover:
    image: "posts/images/dockerscripts.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
This post is a collection of Docker images I use on my homelab servers. Docker uses OS-level virtualization to deliver software in packages called containers. They're completely self-contained and allow a user to quickly spin-up any software almost instantly to use or test out without installing extra.

### Crypto
#### Storj

Storj is an S3-compatible platform and suite of decentralized applications that allows you to store data in a secure and decentralized manner. This image allows you (the user) to supply Storj with your available storage. Like most crypto adventures this requires 24/7 access to any data you host.

```bash
docker run -d --restart always --stop-timeout 300 \
-p 28967:28967/tcp \
-p 28967:28967/udp \
-p 192.168.1.83:14002:14002 \
-e WALLET="YOUR.WALLET.HERE" \
-e EMAIL="YOUR.EMAIL.HERE" \
-e ADDRESS="YOUR.DDNS.HERE:28967" \
-e STORAGE="10TB" \
--dns="8.8.8.8" \
--mount type=bind,source=/mnt/storj/identity/storagenode,destination=/app/identity \
--mount type=bind,source=/mnt/storj/storagenode,destination=/app/config \
--mount type=bind,source=/mnt/storj/dbs,destination=/app/dbs \
--name storagenode storjlabs/storagenode:latest
```
As of 2022, you can run a Storj node on a Raspberry Pi 3B or higher; or an x86 machine.