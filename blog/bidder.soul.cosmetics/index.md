---
title: "Moving VPS hosting provider"
date: 2024-06-30T12:43:17+01:00
description: "Annoucement that the webzone is moving from Hostworld.uk to Hostinger.co.uk to provide you with faster performance and enhanced security."
draft: false
toc: false
author: Joseph Fleet
slug: bidder.soul.cosmetics
tags:
- news
- webzone
---

**The webzone has moved to a new hosting provider !**

{{< figure src="friendship_ended.webp" alt="Edited friendship ended meme" link="friendship_ended.webp" >}}


### Why the Move?

The previous VPS was up for annual renewal, and initially, there was no consideration of moving.

However, over the past month, the Hostworld VPS has experienced issues with the attached storage media disappearing from the server, necessitating reinstalls or recovery from backups.

This was far from ideal since I prefer to occasionally tinker with my webzone and leave it running smoothly 24/7.

After researching well-reviewed VPS providers that didn't charge too many shekels for a small VPS, I decided to switch to Hostinger.

So far, the experience has been excellent. The setup was straightforward and took perhaps a total of 5 minutes for the VPS to spin up to a usable state.


#### Comparison Table

|         | Hostworld | Hostinger |
|---------|-----------|-----------|
| CPU     | 2 x vCPU  | 2 x vCPU  |
| RAM     | 1GB       | **8GB**       |
| Storage | 30GB      | **100GB**     |

### Benefits from the move ?

Well on the frontend you may have noticed new styling for the webzone. This isn't directly correlated to the move but I felt it was a good chance to further improve on the webzone styling.

On the backend the NGINX configuration has been changed to use more modern versions of TLS, improving security. [301 redirects](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/301) have been put in place if trying to hit the webzone on port 80 or on the server IP address.

Next up I'm going to be tackling the workflow for the updating of the site files on the VPS. Alongside some further tinkering with NGINX / Ubuntu Server.

Stay tuned for more updates on the webzone.

-*Joseph*