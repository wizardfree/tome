---
title: "Introduction to Azure Cloud Concepts"
date: 2023-06-18T12:06:58+01:00
description: "An article covering Cloud Concepts as they relate to Microsoft Azure."
draft: false
toc: false
author: Joseph Fleet
slug: doing.tests.incurred
tags:
- Azure
- Cloud
---

> "There is no spoon" 🥄
>
> – Spoon Boy (The Matrix) [^1]


## What is Cloud computing?

_Cloud computing_ is computing services offered and delivered over the Internet. These services include IT Infrastructure. Think virtual machines, storage, databases. And hosted software services such as Office 365.

Also falling under the cloud services umbrella. Internet of Things (IoT), Machine Learning (ML) and Artificial Intelligence (AI).

When discussing anything to do with IT there is a question that arises. **Who takes care of it all?**. If it's a business or small company there may be an IT team dedicated to support and maintenance. Or otherwise in a home network _someone_ has to take up the mantle of keeping the computers running.

So when discussing cloud computing models. Which are in essence _"someone else's computer"_ **who** takes care of it all?

To answer the above we must first understand the **Shared Responsibility** model. Meaning that the physical, security, power, cooling, and network connectivity aspects. Are all handled by the cloud provider. With the consumer being responsible for the data and information stored in the cloud.

This can be broken down further by the cloud computing model which is being used:
![Microsoft Shared Responsibility Diagram](https://learn.microsoft.com/en-us/azure/security/fundamentals/media/shared-responsibility/shared-responsibility.svg)

The diagram above shows that _Software as a Service (SaaS)_ has the least amount of responsibility. With _Platform as a Service (PaaS)_ and _Infrastructure as a Service (IaaS)_ each having  more and more responsibility. The scenario with the most responsibility is _On-premises_.

### Cloud Computing Models

A collection of cloud resources are defined under a cloud model. There are **three (3)** cloud models.

1. **Private** Cloud

This is used by a **single** entity. Using a Private Cloud comes with a greater cost. But much greater control as compared to other cloud models.

2. **Public** Cloud

Built, controlled, and maintained by a **third-party** cloud provider. Think [Azure](https://portal.azure.com/), [Amazon Web Services (AWS)](https://aws.amazon.com/), and the [Google Cloud Platform (GCP)](https://console.cloud.google.com/). With a public cloud. Anyone can buy and use cloud services. Only requires an account and a credit card!

3. **Hybrid** Cloud

A computing environment which uses both **public** and **private** clouds. This is an inter-connected environment. Using this model allows a private cloud when experiencing an increased, temporary demand. To deploy public cloud resources to help with this increased demand.

Other possible cloud models include:

- **Multi-cloud**

As the name suggests this is where you can use multiple public cloud providers.

- **Azure Arc** (Microsoft Azure only)

A set of technologies which help to manage your cloud environment. Whether that is a Public cloud purely on Azure, or a private cloud in a datacenter.

- **Azure VMware Solution** (Microsoft Azure only)

If a solution has already been established with VMware in a private cloud environment. This allows for running of VMware workloads in Azure with seamless integrations and scalability.

### Captial Expenditure (CapEx) vs Operational Expenditure (OpEx)

**CapEx** is typically a one-time, up-front expenditure. 

**OpEx** is spending money on services or products over time.

Cloud computing falls under **OpEx** as you pay for the IT resources you use. You only pay for what you use. Didn't run that VM this month? No charge. Ran several VMs over the course of two weeks? Get the credit card ready.

### Azure?[^2]

[Microsoft _Azure_](https://portal.azure.com/) is a cloud computing platform. Which offers all three (3) of the above models. The number of services available on the Azure platform is ever increasing.

## The benefits of using cloud services

Two (2) major benefits of using cloud services include:

1. **High Availability**

It is important that resources are available when needed. The concept of **High Availability**. Focuses on the greatest availability, regardless of disruptions or unforeseen events.

2. **Scalability**

The ability to adjust resources to meet demands. Such as in the case of a sudden peak in traffic where you may need more computational power or more storage.
There is also the benefit of only paying for what you use. If demand for a service lessens, so does your resource usage so in turn your bill gets cheaper.

Scaling is also broken down into two (2) varieties:

- **Vertical Scaling**

The ability to add/remove more resources to a single service. Such as more CPUs or RAM to a Virtual Machine.

- **Horizontal Scaling**

The ability to add or remove nodes into an existing system infrastructure. Used in conjunction with a load balancer. 

Along with the benefits of **High Availability** and **Scalability**. Cloud computing also offers. **Reliability** and **Predictability** as cornerstones of the Azure Well-Architected Framework.

In this context **Reliability** means that due to the decentralised design of the Azure Cloud (datacenters existing multiple locations across the globe) that even if one or more nodes was to go down the other regions datacenters would remain functioning. An application or resource group can be configured in such a way as to benefit from this global reliability.

**Predictability** in the cloud focuses on _Performance_ or _Cost_. 

Performance focuses on predicting the resources needed to continue delivering an experience users love. _Auto-scaling_, _Load Balancing_, and _High Availability_. Are some of the tools used to create this predictability.

Cost, is the ability to forecast future costings of using cloud services. Uses data analytics to find patterns and trends. Which can aid in planning resource deployments.

### Misc Benefits

In a more than ever before connected world. It's of major importance. To be compliant with regulatory requirements. Whether these be at the business or government levels. Cloud features such as _set templates_ ensure these requirements are being met. Cloud based auditing. Will flag any resources which are not in compliance and provides mitigation strategies.

With the 'cloud' accessed through the Internet. Cloud providers are some of the best equipped to handle **DDoS (Distributed Denial of Service)** and other Internet based attacks.

Resources in the 'Cloud' are managed through several means. Various web portals. Command line interfaces. APIs (Application Programming Interfaces), and PowerShell code. Can all be used to manage the 'Cloud'.

## Cloud service types

There are many types of cloud service types. Some of the most prevelant are:
- **IaaS (Infrastructure as a Service)**
- **PaaS (Platform as a Service)**
- **SaaS (Software as a Service)**

### IaaS (Infrastructure as a Service)

The most flexible of the cloud services. This categorisation provides greatest control for the tenant. With the higher responsibility that entails (see **Shared Responsibility**). With **IaaS** the cloud provider maintains the hardware, network connectivity, and physical security. Everything else is the users responsibility. You can think of this as paying to use someone elses hardware.

Common use-cases for this are testing and development. Lift-and-shift migrations also use this model. 

A Lift-and-shift is the creation of cloud resources similiar to on-premises. Such that it is possible to move the on-prem scenarion to the cloud. [An IRL example of a Lift-and-shift](https://www.youtube.com/watch?v=Tc6IT5L3ZSk).

### PaaS (Platform as a Service)

The middle ground between renting space in a datacenter and paying for a complete deployed solution. 

`IaaS -> PaaS* -> SaaS`  * = On the scale of responsibility. We are here.

Much like an **IaaS** offering. The cloud provider maintains the physical infrastructure, physical security, and a connection to the internet. Also they maintain the operating systems, middleware, development tools, and can even provide business intelligence services. **PaaS** scenarios abstract out the licensing and continous patching for Operating Systems and Databases. 

Think of **PaaS** like using a domain joined machine. An in-house IT team maintains the device with regular updates, patches, and refreshes. Letting the end-user focus on their work.

Common use-cases for **PaaS** are using these as a framework for Developers to build upon. Think developers writing an application which is to support both Windows and macOS platforms. Using **PaaS** they don't have to physically own these devices or maintain those devices. Simply spinning up a Virtual Machine and performing tests or development as need be.

Analytics and business intelligence are also available on the **PaaS** model. Allowing for businesses to analyse their data for insights and pattern analysis.

### SaaS (Software as a Service)

Think of this model as renting the usage of an application. Email, messaging applications, and financial software are all common examples of **SaaS** implementation. The **SaaS** model is the least flexible but easiest to get up and running.

In this model the user is only responsible for their data. Everything else is managed by the cloud provider. [Office 365](https://www.office.com/), the latest office suite offered by Microsoft. Is a prime example of **SaaS**. All the products contained within [Office 365](https://www.office.com/) have web versions. Which are accessed using a browser.

In closing. This was part one (1) of a three (3) part mini-series of articles. Each one covering the material needed for the [AZ-900: Microsoft Azure Fundamental](https://learn.microsoft.com/en-us/certifications/exams/az-900/) certification. The purpose of these articles is to share knowledge and develop a further understanding of the material herein.

_-Joseph_

[^1]: Referring how there is no 'Cloud'. Simply someone else's computer. Also can we appreciate what a belter "Spoon Boy" is as a nickname.
[^2]: This header/paragraph really doesn't flow very well but I struggled to find a suitable place for it. 🤷🏻