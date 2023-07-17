---
title: "Azure: Storage and Security"
date: 2023-06-24T21:50:47+01:00
description: "A brief introduction to Azure architecture and services as they pertain to the AZ900 certification. Part three"
draft: false
toc: false
author: Joseph Fleet
slug: intense.diverse.retrieval
tags:
- Azure
- Cloud
---

### Azure storage services

A storage account in Azure provides a _unique_ name which provides access over the web. This _unique_ name must be between 3 and 24 characters in length and may only contain alphanumeric characters. Data stored in a storage account is secure, highly available, durable, and scalable.

When creating a storage account. An **account type** must be selected. This account type determines the storage services and redundancy options.

The Storage account types are:

| Type of storage account         | Supported storage services                                                                | Redundancy options                        | Usage                                                                                                                                                         |
|---------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Standard general-purpose v2     | Blob Storage (including Data Lake Storage), Queue Storage, Table Storage, and Azure Files | LRS / GRS / RA-GRS / ZRS / GZRS / RA-GZRS | **Recommended for most scenarios using Azure Storage.** Network File System (NFS) is only supported at the premium tiers.                                         |
| Premium block blobs<sup>3</sup> | Blob Storage (including Data Lake Storage)                                                | LRS / ZRS                                 | Premium storage. **Recommended for scenarios with high transaction rates or require consistently low storage latency.**                                           |
| Premium file shares<sup>3</sup> | Azure Files                                                                               | LRS / ZRS                                 | Premium storage. **Recommended for enterprise or high-performance applications.** This account type supports both Server Message Block (SMB) and NFS file shares. |
| Premium page blobs<sup>3</sup>  | Page blobs only                                                                           | LRS                                       | Premium storage. **Used for page blobs only.**

The redundancy options include:
- **Locally redundant storage (LRS)**
- **Geo-redundant storage (GRS)**
- **Read-access geo-redundant storage (RA-GRS)**
- **Zone-redundant storage (ZRS)**
- **Geo-zone-redundant storage (GZRS)**
- **Read-access geo-zone-redundant storage (RA-GZRS)**

#### Azure storage redundancy

Data in Azure storage has **multiple** stored copies at any one time to protect from disaster. Such as hardware failures, network or power outages, and natural disasters. When deciding which redundancy option to use it is important to consider the tradeoffs between lower costs and higher availability.

#### Locally Redundant Storage (LRS)

**Locally Redundant Storage (LRS)** replicates your data _three_ (3) times within a single data center in the primary region. This redundancy option provides _eleven_ (11) _nines_ (9) of durability in an annual period (99.999999999% uptime). Protecting against server rack and drive failures this is the cheapest option which offers limited redundancy. 

#### Zone-redundant storage (ZRS)

**Zone-redundant storage (ZRS)** replicates your Azure Storage synchronously across _three_ (3) availability zones in the primary region. This redundancy option provides _twelve_ (12) _nines_ (9) of durability in an annual period (99.9999999999% uptime). **ZRS** allows for both read and write operations even if a zone become unavailable. When a zone becomes unavailable. Networking updates are taken care of by Azure automatically. ZRS is commonly used when restricting replication of data within a country or region to meet data governance requirements.

Data can additionally be copied to a **secondary** region (see Region Pairs for more information). The _two_ (2) options for copying data to a secondary region are: 

- **Geo-redundant storage (GRS)**
- **Geo-zone-redundant storage (GZRS)**

Think of GRS as running LRS in _two_ (2) **seperate** regions. 

Think of GZRS as similiar to running ZRS in the Primary region and LRS in the secondary region.

Default behaviour for data in the secondary region is to only be enabled for read and write access if the failover to the secondary region is activated.

#### Geo-redundant storage (GRS)

**Geo-redundant storage (GRS)** copies data in sync _three_ (3) times within a single physical location in the primary region using LRS. Data is then copied asynchronously to a single physical location in the secondary region using LRS. This redundancy option provides _sixteen_ (16) _nines_ (9) of durability in an annual period (99.99999999999999% uptime).

#### Geo-zone-redundant storage (GZRS)

**Geo-zone-redundant storage (GZRS)** copies data across _three_ (3) availability zones in the primary region. In addition to being replicated to a secondary geographical region using LRS. GZRS is reccommended for applications which require maximum consistency, durability, availability, excellent performance and resillience for disaster recovery. This redundancy option provides _sixteen_ (16) _nines_ (9) of durability in an annual period (99.99999999999999% uptime).

**GRS** and **GZRS** replicates your data to another physical location in the seconday region to provide protection against _regional_ outages. 

This data is only available **read-only** unless the customer **or** Microsoft initiates a _failover_. For scenarios where read access is required most of the time use **RA-GRS** or **RA-GZRS**.

#### Azure Storage services

Azure storage uses the following data sevices:
- **Blobs**: Scalable object stores for text and binary data. Data stored in a Blob is unstructured. Can managed thousands of simultaneous uploads, massive amounts of video data. and expanding log files.

Blobs are used:
- storing data for analysis
- storing backup data and archival purposes
- streaming video and audio
- distributed access to stored files

Can be accessed using HTTP or HTTPS or through software libraries. As well as Azure specific tools such as the Azure Storage REST API, Azure PowerShell or Azure CLI.

- **Files**: Managed file shares for cloud or on-premises deployments. Accessible using Server Message Block (SMB) or Network File System (NFS) protocols. Accessible from Windows, Linux, and macOS clients.

- **Queues**: Messaging store for reliable communication between application components. Has the ability to store large numbers of messages. Can be accessed using HTTP or HTTPS. A queue is only limited to the size of the storage account.
- Disks: Block-level storage volumes used by Azure Virtual Machines.

Available access tiers for blobs include:
- **Hot access tier**: optimised for storing data that is accessed frequently
- **Cool access tier**: optimised for infrequently accessed data and stored for at least 30 days
- **Archive access tier**: data which is rarely accessed and stored for a minimum 180 days

Hot and Cool access tiers can be set at the account level. Archive access **cannot** be assigned at the account level.

#### Azure Data Migration options

**Azure Migrate** is a service provided by Microsoft which helps to migrate from on-premises to the cloud. Migrate provides a central location to manage the assessment and migration.
Some of the tools provided by Migrate include:

- Discovery and assessment: assess physical and virtual servers.
- Server Migration: ability to migrate physical and virtualised servers.
- Data Migration Assistant: stand-alone tool to assess SQL Servers.
- Database Migration Service: migrates on-prem databases to Azure VMs running SQL servers.
- Web app Migration Assistant: standalone tool to assess .NET and PHP web apps readiness to transfer to Azure.
- Azure Data Box: physical data devices to transfer massive quantities of data.

For more information on Azure Data Boxes see this [article](https://wizardinthe.cloud/blue.info.crate/).

#### Benefits of Azure Storage

- Durable / Highly Available
- Secure: encrypted by default, provides fine-grained control over data access.
- Scalable: designed to be massively scalable.
- Managed: hardware maintenance, updates, and critical issues are all handled by Azure.
- Accessible: data is accessible from anywhere in the world using HTTP or HTTP. Libraries are provided by Microsoft for a wide range of programming languages including: .NET, Java, Node.js, Python, PHP, Ruby, and Go to name a few. There is also support for scripting using **Azure PowerShell** or **Azure CLI**.

#### Azure File Movement options

Azure provides the _AzCopy_ command-line utility for copying blobs and files to a storage account. _AzCopy_ can upload, download, and copy files. Can also be configured to work with other cloud providers.

```PowerShell
azcopy copy [source] [destination] [flags]
```

For a more graphical option there is the _Azure Storage Explorer_. This works on the Windows, macOS, and Linux. Effectively working as a frontend for the _AzCopy_ utility. Having all of the same functionality.

![Azure Storage Explorer ScreenShot](https://learn.microsoft.com/en-us/azure/media/vs-azure-tools-storage-manage-with-storage-explorer/vs-storage-explorer-overview.png)

For on-prem Windows servers _Azure File Sync_ is a tool to automatically sync (bi-directionally) local files and files in Azure.

### Azure Identity, Access, and Security

Azure uses **Azure Active Directory (AD)** as it's identity and access management service. **Azure AD** provides:

- Authentication: verifies identity for access to applications and resources.
- Single Sign-On: a single identity is tied to a user. This way a single username and password can be used to access multiple applications.
- Application Management: cloud-based and on-premises apps can be managed using **Azure AD**.
- Device Management: devices can be registered within **Azure AD** allowing those to managed through tools like [Intune](https://intune.microsoft.com/).

On-premises Active Directory can be connected to Azure AD by using **Azure AD Connect**. A connection made in this way synchronises data between the two.

![Azure AD Connect Diagram](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/media/whatis-hybrid-identity/arch.png)

**Azure Active Directory Domain Services (AD DS)** is a service which provides managed domain services. 

For an admin this means the benefits of using a directory service without the need to maintain the infrastructure. Deployment, management, and patching of domain controllers in the cloud is all handled in the background.

When an **Azure AD DS** is created, _two_ (2) Windows Server Domain Controllers are deployed in the specified [Azure Region](https://www.wizardinthe.cloud/springs.administered.supply/). These Domain Controllers are handled by the Azure platform.
Resources which are created in the **Azure AD DS** are only synced in one-direction.

#### Azure Authentication Methods

Azure Authentication includes:

- Single Sign-on: see above.
- **Multifactor Authentication** (MFA): prompting a user for an _extra_ form of identification during sign-in. MFA has authentication elements fall into _three_ (3) categories:

  - Something the user **knows** = Password or PIN
  - Something the user **has** = Smart Card or Hardware/Software Token ([Microsoft Authenticator](https://support.microsoft.com/en-gb/account-billing/download-and-install-the-microsoft-authenticator-app-351498fc-850a-45da-b7b6-27e523b8702a) falls into this category)
  - Something the user **is** = Biometric authentication

- **Passwordless Authentication**: replaces the need for a password with something you have, are, or know. Currently there are _three_ (3) passwordless authentication options which intergates with Azure Active Directory:

  - Windows Hello for Business: this form of authentication uses biometric and PIN credentials which are tied directly to a specific user's PC.
  - Microsoft Authenticator app: using this app allows for a users phone to become a passwordless authentication method. This differs from the MFA use case as in that scenario a password is also required _in addition_ to allowing the login via the app.
  - FIDO2 security keys: Created by the FIDO (Fast IDentity Online) Alliance to promote open authentication standards and reduce the reliance of passwords. FIDO2 security keys are typically USB devices but also support Bluetooth or NFC. One of the most popular is the [YubiKey](https://www.yubico.com/products/)

**Azure AD External Identities** refers to all the ways you can securely interact with users outside of the your organisation. In this way you can define how your internal users can access external organisations. 

With External Identities, exteral users can "bring their own identities". Whether this be a corporate/government-issued digitial identity or an unmanaged social identity like a Google or Facebook account.

- **Business to business** (B2B) collaboration: collaborate with external users by letting them use their preferred identity. Typically these users are represented as guest users in a company directory.
- **B2B direct connect**: establishes a mutual, two-way trust with another Azure AD organisation. This form of connection currently supports Teams shared channels.
- **Azure AD business to customer** (B2C): publishes modern SaaS apps or custom-developed apps to customers, whilst using Azure AD B2C for identity and access management.

**Conditional Access** is a tool for allowing or denying access to resources based on signals. These signals can include: physical location, application version, time and date. 

For an example of how this works; a user who is logging in from a known location (such as a main office) can be configured to not be challenged for a second authentication factor. Whereas someone logging in outside of business hours may have their account locked.

**Azure Role-Based Access Control** is the ability to control what _access_ users have to the resources in a cloud environment. Whilst using Azure RBAC the principle of [**least privilege**](https://www.cloudflare.com/learning/access-management/principle-of-least-privilege/) applies. 

**Azure RBAC** can be applied to _groups_ preventing manually applying permissions to each user. Enforcement of **Azure RBAC** is on any action which is initiated against an Azure resource.

A security model with increasing amounts of adoption is the **Zero Trust** model. Check out this [Data Breach Investigations Report](https://www.verizon.com/business/resources/reports/dbir/2023/summary-of-findings/) from Verizon for why this is happening. 

> TL;DR The three primary ways in which attackers access an organization are **stolen credentials**, **phishing** and **exploitation of vulnerabilities**.
> Each of these attacks have only risen in number year over year.

This model assumes a **security breach** and verifies each request. In this model instead of assuming that a device within the corporate network is safe, it instead requires everyone to authenticate. The guiding principles of **Zero Trust** are: 

- Verify explicitly
- Use least privilege access
- Assume a breach

The **defense-in-depth** strategy is put in place to slow the advance of an attack of acquiring unauthorised access to data. This strategy is split into _seven_ (7) layers. The layers are as follows:

1. Physical Security: locks, physical barriers, security personnel
2. Identity & Access: authentication
3. Perimeter: protection against network-based attacks
4. Network: least-privilege network connectivity to resources
5. Compute: secure access to systems
6. Application: bug checks/fixes, reduce vulnerabilities introduced into code
7. Data: the CIA (Confidentiality, Integrity, and Availability) trifecta applies here

**Defender for Cloud** is a natively integrated monitoring tool for security and threat protection. Provides the tools needed to harden your resources and protect against cyber attacks. 

**Defender for Cloud** can also be added to on-premises servers. Providing customised threat intelligence and prioritised alerts according to the specific environment.

Whilst **Defender for Cloud** is available natively on Azure it is not restricted to Azure only. Can be installed on other cloud providers such as Amazon Web Services (AWS) and Google Compute Platform.