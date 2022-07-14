---
title: "Flame - a homelab dashboard"
date: 2022-07-01
description: "Flame is self-hosted startpage for your server. Easily manage your apps and bookmarks with built-in editors."
tags: ["linux"]
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
    image: "posts/images/flamedashboard.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
Need a place to keep track of your growing services in a simple, easy to use homepage-like display? Then the Flame dashboard has you covered. Flame offers a simple UI for adding your services and/or bookmarks to make access easier.

Flame offers a single page dashboard with search functionality (search includes local and web search) along with multiple themes to get it to your liking.

![SUI](../images/flamedashboard.sui.png)

Originally developed by [jeroenpardon](https://github.com/jeroenpardon) under the name SUI, contained a minimalist design and required you to edit config files to get it working. If this is your thing perhaps try out SUI. SUI was forked by [pawelmalak](https://github.com/pawelmalak) and heavily modified to introduce a working UI to add/edit applications and bookmarks while keeping the aesthetic of SUI intact. For as long as it has existed I have used Flame as my starter page, adding new services was easy and I liked it that way.

![Flame](../images/flamedashboard.png)

Not content with the features of Flame, [fdarveau](https://github.com/fdarveau) had the idea of having split categories in Flame to split your services up, something I wanted from the original Flame but couldn't get. It's not stated in this fork but the biggest feature they included was categories and it works great.

![Flame](../images/flamedashboard.screencap.png)

With Docker, testing out each is super simple, below I include fdarveau's version since I believe it offers the most features.

```bash
docker run -d \
  --name flame-dashboard \
  -p 5005:5005 \
  -v /mnt/docker-configs/flame-dashboard:/app/data \
  -e PASSWORD=demo \
  ghcr.io/fdarveau/flame:latest
  ```

* <https://github.com/jeroenpardon/sui>
* <https://github.com/pawelmalak/flame>
* <https://github.com/fdarveau/flame>