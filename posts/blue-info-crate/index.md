---
title: "Today I Learned: Azure Data Box(es)"
date: 2023-01-20T16:06:55+01:00
description: "TIL: Azure Data Box(es) Who? What? Where?"
draft: false
author: Joseph Fleet
slug: blue.info.crate
tags:
- TIL
- Hardware
- Networking
- Cloud
- Azure
---

**tl;dr** Physical devices used to transfer large quantities of data to the [Azure Cloud](https://azure.microsoft.com/en-gb).

---

## Intro

> 📖
>
> Move bulk data to Azure quickly and cost-effectively. Data Box data transfer products help you move data to Azure when busy networks aren’t an option.

What happens when a business generates 10's of Terabytes of data daily (or weekly). Yet has no reliable way of uploading this data to the Azure Cloud where it is: Secure[^1], and Available[^2].

*Azure Data Boxes.*

By taking the data stored locally. Transferring said data onto a physical device. Then shipping that device securely back to an Azure data center. Sensitive, mission-critical, data can be moved to the cloud where it can reach where it's needed most.

---

## Options

Depending on how much data is to be transferred to the cloud. There are 3 physical and 1 logical options available. Lets go over the physical options:

1. The **Data Box Disk**: 
    - An enterprise-grade HDD enclosure which holds 8TB per disk. 
    With five (5), for a maximum of 35TB, available per order. 
    - Uses AES[^3] 128-bit encryption and uses a USB3 or SATA interface.

2. The **Data Box**: 
    - Holds 100TB per device. One per order.
    - Uses AES 256-bit[^4] encryption. Comes equipped with 1x1/10 Gbps RJ45, 2x10 Gbps SFP+ interfaces. The RJ45 is used for management of the box including initial setup. But can also be used for data transfer. 
    - Think of this like a rugged NAS box.

3. The **Data Box Heavy**: 
    - Named correctly as each one holds a Petabyte **(!)** of data.
    - Weighing roughly 500lbs and coming with it's own trolley this is no joke. The same as the Data Box only one per order. 
    - Uses AES **256-bit** encryption, 2 X 1-GbE interfaces. Yet foregoes the 2x10 Gbps for 2x40 Gbps. A storage server on wheels. 
    - For when your data needs that bellhop treatment.

---

## What happens to the data after it's transferred into the cloud?
All data is securely wiped. According to the [National Institute of Standards and Technology (NIST) Special Publication 800-88 revision 1 standards](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-88r1.pdf).

Along with this the actual enclosures and disks are tamper-resistant.

---

## Use cases
### Oceaneering Intl

[Oceaneering Intl](https://www.oceaneering.com/) uses robotic workers which generate 1TB a day of sensor data, with entire ships generating 10TB a day.
Miles from the shoreline. Data uplink using satellites is prone to interference. 
Coupled with higher latency (compared to terrestrial offerings) and variable speeds.

This means a 6-7 month wait between the data being collected and it being in front of the people who need to see it. By offloading the data through Azure Data Boxes the collected data is uploaded and available in a fraction of the time.

For Oceaneering Intl this allows them to make decisions quicker. And their clients receive meaningful, relevant data. Video [here](https://youtube.com/v/y0nGRHw3Zqc).

---
## Further Reading
- [Microsoft Learn page for Data Boxes](https://learn.microsoft.com/en-us/azure/databox/)
- [Azure Overview page for Data Boxes](https://azure.microsoft.com/en-gb/products/databox/data/#overview)

[^1]: [World class security with a team of 3500 cybersecurity experts working to further strengthen and secure the cloud.](https://azure.microsoft.com/en-gb/explore/security/)
[^2]: At Azure's core is its [global distribution of data centers](https://i2.wp.com/www.lineal.co.uk/wp-content/uploads/2017/09/azure-datacentre-map.png) split into availability zones ensuring uptime for VM's stays at four nine availability.
[^3]: **A**dvanced **E**ncryption **S**tandard. The modern emerging standard for encryption.
[^4]: It takes [*1 billion billion years*](https://www.eetimes.com/how-secure-is-aes-against-brute-force-attacks/#:~:text=So%2C%20how%20long%20does%20it%20take%20to%20crack%20128%2Dbit%20encryption%3F%201%20billion%20billion%20years.) to crack 128-bit encryption. Bumping this up to 256-bit just ensures that data is not being brute-forced before the heat-death of the universe 😅.