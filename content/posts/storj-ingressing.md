---
title: "Storj - zero ingressing data"
date: 2022-01-06
description: ""
tags: ["storj", "crypto"]
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
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "posts/images/storj.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

Storj is a decentralized, open-source distributed cloud storage platform. It offers unlimited and secure data storage. The company has created a blockchain-based marketplace where users can rent out their unused hard drive space to earn Storj tokens (STORJ).

Here we will discuss the benefits of using Storj over other cloud storage providers such as Dropbox or Google Drive. These are some of the benefits:

- Unlimited data storage

- Secure data

- No ingressing data

- No central point of failure

It was designed to provide a better solution for storing data in comparison to conventional cloud storage platforms. The Storj protocol achieves this by encrypting and distributing data among nodes in the network. This makes it impossible for any single node to access the entirety of the data stored on the network. The nodes are incentivized with cryptocurrency, which they receive when they offer storage space and bandwidth to the network.

Storj works by splitting content 80x times and placing bits on different nodes for redundency (up to x2.7). To retrieve the bits again you only require 29 bits to remake the file. This is because of [Reed–Solomon error correction](https://en.wikipedia.org/wiki/Reed%E2%80%93Solomon_error_correction), a form of erasure coding that allows a minimum amount of bits needed to remake the data.

I run my own node on a Raspberry Pi 3B (64bit), this node provides 4TB of free storage I have on an external drive. After three months without issue I ran into a problem one day where ingress dropped to zero. With a whole day of no ingress I began investigating and found something interesting. The minimum allowed version displayed in the webUI is not really what you should follow as a guide. While running v1.38, the allowed version is v1.24. However when Storj updated the software to v1.40, anyone running below this would stop receiving ingress.

Problems arise when running such a node when you use Docker, because Docker images do not update, ever. You must pull new images yourself. So while running Storj on Docker comes with an easy setup and forget system, this does come with some caviets. You **must stay up to date** on major version updates. Another choice is running [watchtower](https://containrrr.dev/watchtower/) in order to keep the container up to date. Not updating will have your node unable to ingress any more data and your stored data will stop growing.

On the Storj webUI it will tell you that Storj will continue to run on older major versions, what this should also tell you is major versions require updating too (e.g v1.3X will not receive ingress if the latest is v1.4X).

Heading over to their forums you will find users pointing out that this is known and written somewhere and that we all should know about. But perhaps it could just be written better in the webUI. Running through Docker it is best if you run a watchtower container as well. This container will monitor your other containers for image updates (by default every 24 hours) and proceed to update them for you.

I use this to keep my node up to date:

```bash
docker run -d \
  --name watchtower \
  -e WATCHTOWER_CLEANUP=true \
  -e WATCHTOWER_TIMEOUT=20s \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /etc/localtime:/etc/localtime:ro \
  containrrr/watchtower \
  storagenode
```

I added a few environment variables to my liking:

* WATCHTOWER_CLEANUP as true will remove old images to save space.
* WATCHTOWER_TIMEOUT as 20s will give the containers 20s to shutdown before updating them. Default is 10s and seems a little short for a Storj node.

The two volumes linked to the container (-v) are docker runtime so that watchtower can see the containers on the host system and localtime so watchtower is linked to my timezone.

Hint: As the last line of my command I have the containers I want to monitor. Rather than monitor all images I'm running I have just my Storj container called storagenode. This is handy as I run many containers that I don’t necessarily want to be updating the second they are released (number one cause of breaking things).

Storj is exciting technology that is bound to shake up traditional centralized cloud storage providers. I love how easy it is to contribute your own storage and can't wait to see real-world usage in time.
