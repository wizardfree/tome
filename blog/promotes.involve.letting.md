---
title: "Network Air Gaps: Why They're Crucial for Cybersecurity"
date: 2023-07-26T18:41:42+01:00
description: "In today's digital age, cybersecurity is more important than ever before. One of the most effective ways to protect against cyber threats is by implementing network air gaps. These are physical or virtual barriers that isolate critical systems from the rest of a network. In this blog article, we'll explore why network air gaps are crucial for cybersecurity."
draft: false
toc: false
author: Joseph Fleet
slug: promotes.involve.letting
tags:
- Snippet
- News
- Networking
---

## Introduction

If you've been keeping up to date with the ebb and flow of technology-related news. You may of heard that Google is to begin a small scale test of [removing internet access to internal workstations](https://www.theregister.com/2023/07/19/google_cuts_internet/).

This practice known as **"Air Gapping"**. Is nothing new in the world of cyber security. 

But what does it mean?

### Definition
The term "air gap". Refers to the physical distance between the computer or network and the Internet.

To define further what a network air gap is: 
> A security measure that involves physically disconnecting a computer or network from the Internet to prevent unauthorised access. It creates an isolated environment. Where data can is stored and processed without fear of cyber attacks.

Or think of it as the disconnecting or lack of routing. From a trusted network (internal) to a untrusted network (the Internet).

### Importance

Okay so we disconnect from the Internet and keep ourselves safe. But why? Without an Internet connection a computer, or group of computers, is/are not very useful.

This may be true for SOHO[^1] environments. Instead think of those environments which may handle sensitive data like Health and Financial Records. Would you want the detailed records of that mole you had removed only a Google search away? Or would you prefer a Nuclear Power Station be susceptible to someone clicking a dodgy link. I don't.

Network air gaps are an important measure for ensuring cyber security. Particularly for systems that handle sensitive information. With the physical or logical (more on this below) disconnecting of a computer or network from the internet. It becomes much more difficult for bad actors to access and steal data. 

Additionally, even if a bad actor manages to compromise the isolated system. They would be unable to move within the network. To other systems without first breaching more security measures. Pretty neat, huh.

## Implementation

Okay so unplug the router then. No more Internet connection equals no risk of bad actors preying on my collection of [cat pictures](https://icanhas.cheezburger.com/), right?

Correct. This is the simplest implementation of an air gapped system.

Bet you didn't think it would be that easy.

### Types of Network Air Gaps

There are actually a [few types](https://simplicable.com/IT/air-gap) of network air gaps that can be implemented. Depending on the specific needs and requirements of an organization. 

These include:

1. the Physical Air Gap - This involves physically disconnecting a computer or network from the internet using hardware such as firewalls, routers, and switches. This type of air gap is the most effective way to prevent data breaches.

2. the Logical Air Gap - This involves implementing software-based security measures such as Intrusion Detection Systems (IDS) and Access Control Lists (ACLs) to isolate a computer or network from the internet. While less effective than physical air gaps, logical air gaps can be more cost-effective and easier to implement in smaller organizations.

3. the Hybrid Air Gap - This involves combining both physical and logical air gap measures to create a comprehensive security solution. For example, an organization may use a combination of hardware-based firewalls and software-based IDS to protect against cyber threats.

To maintain the air gap once put in place. It requires regular security audits. Which are conducted to identify any vulnerabilities in the system.

Additionally, access control measures are implemented to ensure that only authorised personnel have access to the network. 

In the example of your laptop full of cat pictures. Maintainance would mean checking every few days that the router is still unplugged. And you haven't connected to the neighbours Wi-Fi "accidentally" 🤥. Access control could mean that only **you** use that laptop. Batting the hand away of anyone else who dares to come close. Those cat pictures are of great importance. 

Some of them are even wearing [hats](https://i.chzbgr.com/full/9735166720/h11F93FEF/hat-cats_and_cowboy_hats).

## Advantages and Disadvantages of Network Air Gaps

As discussed above there are several benefits to implementing a network air gap:
- increased security
- reduced risk of data breaches
- improved compliance with regulatory requirements (such as GDPR[^2] and PCI DSS[^3])

But, there are also some drawbacks to consider:
- cost of implementation 
- ongoing maintenance
- potential compatibility issues with other systems, 

It is also important to note that air gaps may not be effective against all types of cyber threats. An air gapped system is still susceptible to attacks involve physical access to the hardware. Such as USB malware. Or social engineering attacks. Such as phishing.

It's important to have solid cybersecurity training and support in place for the people who will be using those systems. Scratch that. **Any** computer related system needs solid cybersecurity training and support in place.

## Closing thoughts

Network air gaps are an important tool in cybersecurity. They help to prevent unauthorized access to sensitive information. In the event of a bad actor managing to gain access to another part of the network. They are unable to reach the data stored on the air-gapped system. And are particularly effective against cyber attacks. Such as phishing and other social engineering tactics.

All this from not being connected to the Internet. Crazy world out there.

-Joseph

[^1]: **S**mall **O**ffice **H**ome **O**ffice
[^2]: [General Data Protection Regulation (GDPR)](https://www.gov.uk/data-protection)
[^3]: [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/)