---
title: "Azure: Regions and Networking"
date: 2023-06-20T18:08:15+01:00
description: "A brief introduction to Azure architecture and services as they pertain to the AZ900 certification."
draft: false
toc: false
author: Joseph Fleet
slug: springs.administered.supply
tags:
- Azure
- Cloud
---

As we continue covering the foundational knowledge of Azure. This post will cover some core components of Azure including Resources, regions, and networking. [See the previous post](https://wizardinthe.cloud/doing.tests.incurred/).

### Core architectural components of Azure

Azure is _the_ Microsoft Cloud services solution. Holding around 22% of the Global Cloud Market Share as of Q1 2022[^1]. Continually updated and expanded. Azure currently provides more than 100 services ranging from virtual machines to mixed reality. 

To use any of the Azure services requires an Azure subscription. A single account can have multiple subscriptions. A **free** Azure account can be created which allows free access to popular Azure products for 12 months, credit for the first 30 days, and access to more than 25 products which are always free. A link to create this free account can be found [here](https://azure.microsoft.com/en-gb/free/).

Azures physical infrastructure is the same as any other datacenter. They're facilities with resources arranged in racks, with dedicated power, cooling, and networking infrastructure. If this mega-global cloud service was to use a _single_ datacenter. That is a disaster waiting to happen. Instead Azure uses **regions**.

#### Regions

Azure **regions** contain at least one datacenter per region. In practice tend to have multiple. Datacenters in the same region are nearby to one another and networked together using low-latency networks.
Within a region **Availability Zones** are the physically seperate datacenters. Each of these have independant power, cooling, and networking from the each other. The thinking is if one zone goes down, all the others remain operational.

To use an avaliability zone for Azure resources or services there are three (3) possible categorisations:

- **Zonal services**: a resource is "pinned" to a specific zone
- **Zone-redundant services**: replicate resources automatically across zones
- **Non-regional services**: always available offerings which are resilient to zone-wide and region-wide outages.

Most of the Azure regions are paired with another region within the same geography. Within **300** miles between them. This helps to recover from and prevent outages due to natural disasters, civil unrest, power outages, or even physical network outages.

It is important to note not all Azure services will automatically replicate data or automatically fall back from a failed region.

One important advantage of **region pairs** is that data inside that pair is kept geographically the same. This is important for tax and law jurisdiction.

Similiar to other regions used by Azure are the **Sovereign regions** which are isolated from the main instances of Azure. These Sovereign regions can be used for compliance or legal purposes. The following are some of the regions which are physically and logically isolated from the rest of Azure in the United States: 

- US DoD Central
- US Gov Virginia
- US Gov Iowa

As you may be able to gather. These sovereign regions are used by Governments and high-ranking official bodies. Where data is highly sensitive.

There also exists regions which are physically and logically isolated from the rest of Azure elsewhere in the world. In partnership between **Microsoft** and [**21Vianet**](https://en.21vbluecloud.com/). This partnership allows the usage of Azure on the **Chinese** mainland. With the stipulation that Microsoft does not directly maintain those datacenters required for Azure functionality.

#### Resources and Subscriptions

A **resource** in Azure can be defined as anything which can be created, provisioned, or deployed. Virtual Machines, virtual networks, and cognitive services are all resources. 

A **resource group** is a collection of resources. A resource may only belong to _one_ (1) resource group at any time. Resource groups **cannot** be nested.
Actions performed to a resource group effects all resources in that group. So deleting a resource group will **delete** all the resources in that group.

**Azure subscriptions** are a way to logically organise resources. This allows for resource groups to be further grouped. For a more intuitive billing. 
For example a test environment might have a seperate resource group containing Virtual Machines which are replicas of production systems. This test environment would have a seperate Azure subscription which has its own billing.

An Azure subscription, Azure account, **and** an identity in Azure Active Directory are required in order to manage resources.

In a **multi-subscription** account, it is possible to use Azure subscriptions to define boundaries around Azure products, services, and resources. The _two_ (2) types of boundaries are:

- **Billing Boundary**: determines how an Azure account is billed for using Azure.
- **Access control Boundary**: access-management policies can be applied at the subscription level.

The final layer of Azure management are **Azure Management groups**. These sit above subscriptions. Providing enterprise-grade management.

Subscriptions can be placed into management groups which then allows for goverance conditions to be applied to that management group. Mangement groups **can** be nested.

### Azure compute and networking services

Azure has many compute options. Today we'll explore three (3) of them. 

- **Azure Virtual Machines**
- **Azure Containers**
- **Azure Functions**.

#### Azure Virtual Machines

**Azure Virtual Machines** allow you to create and use Virtual machines in the cloud. Virtual Machines are IaaS (Infrastructure as a Service) and have multiple use-cases. Virtual Machines allow for the total control of the Operating System. Everything from installation to configuration. 

Azure Virtual Machines give the option to run virtual clients without the need to buy and maintain physical hardware. As with other Virtual Machine offerings the instances can be created and provisioned using image templates.

Every Virtual Machine must have the following: 

- Size: Number of processor cores? Processor Speed? Amount of RAM?
- Storage disks: Size and quantity.
- Networking: Which Virtual network? Public IP address? Port configuration?

Azure Virtual Machines can be created in isolation or can be created and managed as groups. When delpoyed in a group this provides **high-availability**, **scalability** and **redundancy**. Azure has _two_ (2) tools in place to help manage groups of Virtual Machines: 

- **Scale sets**
- **Availability sets**

**Scale sets** allow for the creation and managing of groups of **identical**, load-balanced VMs. These scale sets allow for the central management and configurigation of large numbers of VMs in minutes. A number of VM instances within a scale set can adjust in response to demand or can even scale based on a defined schedule. This could mean for a business which has a busy period of the year. More Virtual Machine instances are automatically spun up to help deal with this heightened workload. Being then spun down once the busy period ends.

Scale sets automatically deploy a load balancer.

**Availability sets** are designed to be resilient to losing all VMs from a single network or power failure. This is done by staggering updates and using varied power and network connectivity. Internally to the availability set are _two_ (2) ways of grouping VMs: 

- **Update domains**
- **Fault domains**

**Update domains** are a logical grouping of hardware which undergo maintenance or reboots at the same time. Virtual Machines in Azure are automatically distributed across different update domains.

**Fault domains** group Virtual Machines by a common power source and network switch. By default an availability set will split VMs up to three fault domains.

#### Azure Containers

**Azure Containers** are the fastest and simplest way to run a [container 🐋](https://www.docker.com/resources/what-container/) in Azure. 

A container is a software package that contains all the necessary components for an application to run, including its code, dependencies, and configuration files. Containers are isolated from one another and from the underlying infrastructure. Which means they can run consistently across different environments without relying on specific hardware or operating system configurations. Multiple containers can run on a single host. 

Azure Container Instances are a form of PaaS (Platform as a Service).

#### Azure Functions

**Azure Functions** are a _serverless_ compute option. Meaning that they don't require either virtual machines or container instances to run. Azure Functions are event-driven by nature. Azure Function can scale automatically based on demand. Costing for Azure Functions is for the CPU time used whilst the function runs. 

Functions can be _stateless_ or _stateful_. 

_Stateless_ is the default and will have the function be unaware of previous data and actions. 

_Stateful_, also referred to as **Durable Functions**. Asks for a context to be passed to the function before running which tracks prior activity.

**Azure App Services** are what enables you to build and host web apps, background jobs, mobile back-ends, and RESTFul APIs. 

These services can be written in any programming language of choice without worrying about the underlying infrastructure. App Services supports Windows and Linux. Enables automated deployments from GitHub, **Azure DevOps**, or a Git Repository.

#### Azure Virtual Desktop

**Azure Virtual Desktop** is a desktop and application virtualisation service which runs on the cloud. **AVD** (Azure Virtual Desktop) is a cloud-hosted version of Windows. Which can be accessed from a multitude of applications and remote desktop services. **AVD** also has the benefit of multi-session support allowing for many concurrent users on a single Virtual Machine.

#### Azure Virtual Networks

**Azure Virtual Networks** and Virtual Subnets enable Azure resources such as Virtual Machines, Web Apps, and databases. To communicate with end users over the internet and with on-premises client computers. 

Think of Azure networks as an extension of your on-premises network. Public and Private endpoints enable communication between external and internal resources. Public as the name might suggest have a public IP. Private again have a private IP address within the address space of that virtual network.

A benefit of the Azure Virtual Networks is the that they are isolated by design as the private address space **isn't** routable on the Internet. 

If communication is required over the Internet then a public IP address can be assigned to the Azure resource. Servicce endpoints are also available to connect to other Azure resource types.

_Three_ (3) mechanisms are available to achieve connectivity from the Virtual networks to on-premises:

- **Point-to-Site**: connections from an outside node back into an on-premises network. Uses an encrypted VPN connection. 
- **Site-to-Site**: a link which is established from a VPN device or gateway to the Azure VPN gateway in a virtual network. Devices in Azure appear as being on the local network.
- **Azure ExpressRoute**: a dedicated private connection to Azure which doesn't route traffic over the internet. This method is used where there is a greater need for bandwidth and high levels of security for data in transit.

Virtual networks can also be connected together by using **Virtual Network Peering**. Which is used to connect two virtual networks directly together. Network traffic on these peered networks doesn't travel over the internet instead using the [Microsoft backbone network](https://azure.microsoft.com/en-gb/explore/global-infrastructure/global-network/).

**Azure Virtual Private Networks** are much like regular VPNs. Creating an encrypted tunnel within another network to connect _two_ (2) endpoints. To use a VPN requires a VPN gateway.

**Azure VPN gateways** are deployed in a dedicated subnet of the virtual network and enable the following:

- Using _site-to-site_ connections to connect **on-premises** datacenters to virtual networks.
- Using _point-to-site_ connections to connect **individual** devices to virtual networks.
- Using _network-to-network_ connections to connect **virtual networks** to other **virtual networks**.

Only _one_ (1) Azure VPN gateway is allowed per Azure Virtual Network. When a VPN gateway is deployed in can be done so in _two_ (2) ways:

- **Policy-based**: specifies the IP address of packets that should be encrypted through each tunnel. Evaluates every data packet against the list of those IP addresses to choose where that packet is going to be sent.
- **Route-based**: Uses [IPSec](https://www.cloudflare.com/learning/network-layer/what-is-ipsec/) tunnels which appear as network interfaces or virtual tunnel interfaces. This allows for "regular" IP routing rules and mechanisms to handle this traffic. This is the preferred connection method for on-premises devices.

Azure understand better than most the importance of **resiliency**. In terms of a VPN gateway there are _four_ (4) ways that **High Availability (HA)** is implemented:

- **Active/standby**: By default VPN gateways in Azure are deployed as _two_ (2) instances. Only _one_ (1) instance can be seen in Azure. The second instance will 'click in' if for any reason the first becomes unreachable or a connection is interrupted.
- **Active/active**: VPN gateways can be assigned a public IP Address each. This is beneficial for [BGP (Border Gateway Protocol)](https://www.cloudflare.com/learning/security/glossary/what-is-bgp/) routing as traffic can be routed at the router level intelligently.
- **ExpressRoute failover**: In this way a VPN gateway is configured as a secure failover for ExpressRoute connections (See below). Whilst ExpressRoute circuits are resilient by design. There is only so much that can be done if a physical wire is cut.
- **Zone-redundant gateways**: VPN and ExpressRoute gateways can be deployed in zone-redundant configuraion. Giving all the benefits that zone-redundancy provides. 

Azure **ExpressRoute** gives the ability for on-premises networks to extend into the Microsoft cloud over a private connection. The connection is defined as an **Azure ExpressRoute Circuit**. 

Connectivity can be:
- An _any-to-any_ (IP VPN) network
- A _point-to-point_ Ethenet network
- A _virtual cross-connection_ through a connectivity provider.

ExpressRoute connections **don't** go over the public Internet. ExpressRoute enables direct access to the following services in all regions:

- _Microsoft Office 365_
- _Microsoft Dynamics 365_
- _Azure compute services_, such as Azure Virtual Machines
- _Azure cloud services_, such as Azure Cosmos DB and Azure Storage

Multiple ExpressRoute circuits can be connected together using [**ExpressRoute Global Reach**](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-global-reach).

#### Azure DNS

**Azure DNS** is a hosting service for DNS (Domain Name System) domains using the Azure infrastructure. By hosting domains in Azure they can be managed using the same credentials, APIs, tools, and use the same billing as your other Azure services. Azure DNS **cannot** be used to buy a domain name.

---

Stayed tune for the next post where we cover Azure Storage Services, File Management, and Azure Identity Management.

[^1]: https://www.theregister.com/2022/05/02/cloud_market_share_q1_2022/