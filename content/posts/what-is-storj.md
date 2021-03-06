---
title: "Storj - what is Storj? (Part 2)"
date: 2022-03-15
description: "Today we look at Storj. What is it and who can benefit from it."
tags: ["crypto", "storj"]
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
    image: "posts/images/storj.png" # image path/url
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

>With Storj DCS (Decentralized Cloud Storage) files aren’t stored in centralized data centers—they're encrypted, split into pieces, and distributed on a global cloud network.

That's the message they convey on their website. They're a decentralized cloud storage network. Much like AWS, Azure and the many other cloud storage providers out there. The difference is where this data is being stored, and for Storj, that data gets hosted on consumer run systems, not Storj itself.

Storj offers the software while the user nodes offer unused storage to others looking to store files, together this creates a completely decentralized storage network.

To protect the network from downtime Storj audits the network with random file verification every hour to ensure its files are available. User nodes must be able to provide cryptographic proof the data is still available, upon receipt of said proof the user node receives payments for storing the data.

Storj uses blockchain technology to run its token (STORJ). The upside is they base all billing in USD to keep prices level. You do not need the token to pay for storage, this keeps the value of storage static with no worries of token price increases.

And like its competitors, you do not need to go to the source to get your own storage needs. Third party companies can use Storj to provide storage to its own users with through S3 APIs.

An example is https://filebase.com, Filebase provides 1TB storage for $5.99 a month with a pay as you go model after that. Their storage comes from Storj and Sia, both decentralized storage networks.

Now the real question is why go this route at all? Price is a factor but what else do you get from moving away from centralized storage to decentralized storage?

### Censorship
The wild west of the internet is long over. But an issue faced by some is with their politics, users may even face complete blocks by tyrannical governments if their views are not aligned. Even Wikipedia has faced blockades, but with decentralized platforms, being blocked becomes much more difficult when the data can be accessed from not one location but many.

### Data control
Are you willing to hand your data over to third-party providers knowing that their views impact what you can store? Google removes files from users personal accounts without resource. With decentralization comes default encryption, your data is never completely stored on a single node, it's split and encrypted amongst many nodes providing ultimate privacy.

### Uptime
AWS, the largest storage provider on the internet, providing 33% of all internet resources is a behemoth online. This behemoth though is not without problems. AWS has suffered outages that affected many of the top 100 websites online. In December of 2021 they had three separate outages, December 7 was a hectic day for them as many first-party Amazon services and third-party services were rendered useless.

As of now, decentralization has not been tested at scale. It's immune to censorship, it secures your data, and uptime is 100%. Will this hold up over time as more users and services start using decentralized storage? Only one way to find out.

As of 2022 the price comparison with the main centralized competitors:


|   |Storage /TB|Bandwidth /TB|Additional|
|---|---|---|---|
|Storj|$4|$7|#1|
|AWS|$23|$90|#2|
|Azure|$18|$87|#2.1|
|Backblaze B2|$5|$10|#4|


#1 Storj has a per-segment fee of $0.0000088 per 64MB of data.

#2
 1. AWS has a fee for every 1000 objects stored of $0.0025.
2. AWS also has a separate fee for requests to objects ranging from $0.0004 for GET/SELECT and $0.005 for PUT/COPY/POST requests, again charged in blocks of 1000.
3. AWS has exceptions to data transfer in the event you're using other services provided by Amazon.

#2.1 Like AWS it separates GET/PUT requests at a similar cost.

#4 Backblaze has a fee for every 10,000 objects stored of $0.004.

AWS/Azure provide multiple storage services—EBS, EFS, S3 and others. For this data I looked up standard S3 storage.