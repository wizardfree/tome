---
title: "Create a Windows Domain Homelab in Virtualbox"
description: "The Step-by-Step process to installing and configuring a Windows Server domain in a private network using Virtualbox."
date: 2022-03-31T14:59:09.406Z
draft: false
toc: true
author: Joseph Fleet
slug: windows.home.lab
tags:
- Windows
- Tips
- Windows Server
- Tutorial
---

## Introduction
Whilst studying for the [Modern Desktop Administrator Associate](https://docs.microsoft.com/en-us/learn/certifications/modern-desktop/) certification its been a tremendous help to setup a virtualised homelab consisting of a Windows Server virtual machine and multiple Windows 10 virtual machines.
This step-by-step instruction set will show the same steps which I used to get setup and configured.

## Prerequisites
- Multi-core CPU with support for virtualisation (Intel® VT/AMD-V)
- Enough RAM for host and minimum 2 clients (>6GB)
- [Windows Server ISO](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019)
- [Windows 10 ISO](https://uupdump.net/)
- [Virtualbox](https://www.virtualbox.org/)

## Virtual Machine Setup
Choose an appropriate name for the VM (Virtual Machine), in this case W19SRV.

![virtualbox2.png](/virtualhomelab/virtualbox2.png)

Allocate an adequate amount of memory to the VM.
> [RAM · 512 MB (2 GB for Server with Desktop Experience installation option)](https://docs.microsoft.com/en-us/windows-server/get-started/hardware-requirements)

![virtualbox3.png](/virtualhomelab/virtualbox3.png)

Create a virtual HDD with default options, this will be more than adequate for testing purposes.

![virtualbox4.png](/virtualhomelab/virtualbox4.png)
![virtualbox5.png](/virtualhomelab/virtualbox5.png)
![virtualbox6.png](/virtualhomelab/virtualbox6.png)
![virtualbox7.png](/virtualhomelab/virtualbox7.png)

Assign CPU cores to the VM, in this case 4 although 2 cores is fine.

![virtualbox8.png](/virtualhomelab/virtualbox8.png)

Tick the Enable 3D Acceleration checkbox and allocate more video memory to the VM. As we will install the Desktop Experience version of Windows Server more video memory is beneficial here.

![virtualbox9.png](/virtualhomelab/virtualbox9.png)

Attach the Windows Server ISO.

![virtualbox10.png](/virtualhomelab/virtualbox10.png)

Assign the first NIC to NAT to grab an IP dynamically and have access to the Internet.

Assign the second NIC to an Internal Network, this will seperate the Windows 10 Clients from your network.

![virtualbox11.png](/virtualhomelab/virtualbox11.png)
![virtualbox12.png](/virtualhomelab/virtualbox12.png)

If all the settings look good, lets move onto installation.

## Installing Server 2019
The Windows installation experience for both Desktop and Server is straight-forward even more so within a VM, click Next, agree to terms, click Next some more. Done.

![virtualbox14.png](/virtualhomelab/virtualbox14.png)

Ensure the (Desktop Experience) version is selected otherwise all further configuration will be done through the command-line 
only.

Differences between Standard and Datacenter editions boil down to Hyper-V Virtual Machine limits/licensing and the Datacenter edition having support for Software-defined Networking.

Choose either as the server will ONLY be for testing, if unsure Standard will do fine for our purposes.

![virtualbox15.png](/virtualhomelab/virtualbox15.png)
![virtualbox16.png](/virtualhomelab/virtualbox16.png)
![virtualbox17.png](/virtualhomelab/virtualbox17.png)

Once installation has finished the VM may restart a number of 
times before reaching the following screen (see image below).

Choose a [strong, memorable password](https://xkcd.com/936/) and let the installation finish.

![virtualbox18.png](/virtualhomelab/virtualbox18.png)

Once at the Desktop, Server Manager will start automatically.
To make out lives easier we will change the name for our Server. 

Under Start ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change... || Start ⇾ Control Panel ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change...

![virtualbox24.png](/virtualhomelab/virtualbox24.png)
![virtualbox39.png](/virtualhomelab/virtualbox39.png)

## (Optional) VirtualBox Guest Additions
The following steps are optional and are done to enable better display options for the VM as well as Shared Clipboard/Folders 
between host and VM.

Insert the Guest Additions ISO through the VirtualBox context menu. 
If this is the first time Guest Additions have been used or a suitable image cannot be found locally you will be prompted to download the latest supported Guest Additions ISO.

![guest-additions.png](/virtualhomelab/guest-additions.png)

The ISO will act just like a CD Drive with an inserted disc.

![virtualbox20.png](/virtualhomelab/virtualbox20.png)

Install the additions using the provided executable for your architecture.

![virtualbox21.png](/virtualhomelab/virtualbox21.png)

Once the installation wizard finishes you will be prompted to reboot. Do so now.

![virtualbox22.png](/virtualhomelab/virtualbox22.png)
Once the VM reboots and you login the desktop should automagically scale properly. If not allow the VM to fully boot and then check the VirtualBox context menu: View ⇾ Auto-resize Guest Display is active (not greyed-out).

![virtualbox23.png](/virtualhomelab/virtualbox23.png)

## Network Setup
Now the fun stuff, as per our VM setup earlier under Network Connections || ipconfig, we see 2 virtual NICs (Network Interface Cards) show up. 
Windows will default some settings such as the names for these interfaces (Ethernet, Ethernet 2) and attempt IP configuration dynamically. 
We now need to override these default values to something more useful.
Pictured below is the 2 virtual NICs shown in Network 
Connections.

![virtualbox25.png](/virtualhomelab/virtualbox25.png)

(Optional) Start by renaming the NICs as to make them more readable quickly. Ethernet and Ethernet 2 aren't particulary 
distinct at a glance.

In my case INTERNET and INTERNAL also aren't particulary distinct but add some flair to yours, go wild. 

![virtualbox26.png](/virtualhomelab/virtualbox26.png)

Firing up PowerShell we can run ipconfig to check out the current IP configuration for the Server at a glance. 
Currently the NIC connected the Internet is acquiring it's IP configuration dynamically if you wish to set a static IP nows the time however in this case I'm happy to let it stay dynamic. 

The Internal NIC however will require some configuration on our part.

Looking at the Internal NIC configuration currently we see the 169.254... tell-tell sign of an APIPA (Automatic Private Internet Protocol Addressing) address currently meaning that this isn't a lot of use to us.

![virtualbox27.png](/virtualhomelab/virtualbox27.png)

Diving into the IPv4 properties for the INTERNAL NIC we'll start by deselecting the Obtain an IP address automatically radiobox instead opting for the Use the following IP address option.

Next we begin the definition of out private network. Choose your address range in this case 10.0.0.1/24 (in honesty a whack 24 is much too large for this scenario 2^8^ = 256 hosts but for simplicity /24 is easy to remember and write down). You don't have to use this address range any valid address range will work, remember this is a private network the hosts connected will have no direct access to the Internet.

NOTE: leave the Gateway address blank this allows for all routing to be done through the Server.

The Preferred DNS address should be the same as the address for the Internet facing NIC. This is another reason to go for a static IP for that NIC.

![virtualbox28.png](/virtualhomelab/virtualbox28.png)

With the NICs setup we move onto the Domain...

## Domain Setup
Time to start utilising the domain controller capabilities of Windows Server.

Start by launching the Add Roles and Features Wizard (Server Manager has a quick link to it under option 2).

Select the first option for Role-based or feature-based installation and click next.

![virtualbox29.png](/virtualhomelab/virtualbox29.png)

(I've omitted the Server selection step as this is straight forward in our example, we only have 1 server to manage!)
Scroll down the list selecting the following: Active Directory Domain Services, DHCP Server, DNS Server AND Remote Access (I forgot this at the time of initial installation whoops)  (NOTE: 

Selecting some of these options will present a pop-up window asking to also select additional required packages, skim the packages and accept.)

Once all selected click next.

![virtualbox30.png](/virtualhomelab/virtualbox30.png)
![virtualbox51.png](/virtualhomelab/virtualbox51.png)
![virtualbox52.png](/virtualhomelab/virtualbox52.png)

Click next until the confirmation page is reached. Check the 
Restart if neccessary checkbox and click Install.

![virtualbox31.png](/virtualhomelab/virtualbox31.png)

Grab a coffee and let the installation happen. The server may restart at this point again let the server finalise installation.

Once completed the Server Manager will be displaying the warning sign in the top right, click on this to continue onto 
Post-installation configuration.

For now we'll address the Domain Services issue which has been highlighted by the Server Manager.

Click on the link: Promote this server to a domain controller, to continue.

![virtualbox32.png](/virtualhomelab/virtualbox32.png)

On the window which pops up we'll be creating a new forest. [^1]
Specify a root domain name this may be a domain you own or simply use one for testing. (foobar.local works nicely :wink:)
Happy? Click next and next again.

![virtualbox33.png](/virtualhomelab/virtualbox33.png)

On the review screen I've highlighted some important information which appears at the the bottom of the scrollable pane. Two important points are mentioned: 

1. Firstly the DNS Server (service) will configured on this computer and this computer will be configured as its own preferred DNS server.

2. Secondly the password for the domain administrator account will be the same as the local administrator account of the server. (If the local admin password is weak now might be good time to change it)

Why is it important to have a DNS service running on our server well:
> ...when a network user with an Active Directory user account logs in to an Active Directory domain, the DNS Client service queries the DNS server to locate a domain controller for the Active Directory domain... ([From the horses mouth](https://docs.microsoft.com/en-us/windows-server/networking/dns/dns-top##:~:text=when%20a%20network%20user%20with%20an%20Active%20Directory%20user%20account%20logs%20in%20to%20an%20Active%20Directory%20domain%2C%20the%20DNS%20Client%20service%20queries%20the%20DNS%20server%20to%20locate%20a%20domain%20controller%20for%20the%20Active%20Directory%20domain.))

Click next.

![virtualbox34.png](/virtualhomelab/virtualbox34.png)

A couple warnings are thrown up during the prerequisite checks but nothing that bothers us for our example.

Clicking next at this point will begin the installation.

![virtualbox35.png](/virtualhomelab/virtualbox35.png)

Once installation is finished the server will restart and once it gets back to the login screen you should now see DOMAIN\Administrator as the prompt (DOMAIN being whatever the root domain NETBIOS name was set to).

Remebering back to the review screen the password for this Domain Administrator account is the same as the local Administrator account, using that we can sign in as usual.

Before we begin connecting clients to this domain we need to continue setup on our private network for our clients namely their leases...

## DHCP Setup
To setup our DHCP (Dynamic Host Configuration Protocol) configuration, we begin by navigating to the DHCP tool either through the Start Menu or Server Manager/Tools/DHCP.

![virtualbox40.png](/virtualhomelab/virtualbox40.png)

We should see only 1 server present under the DHCP tree menu in the left-hand pane, expanding this server option, then further expanding IPv4 we can right-click on the IPv4 menu item to select New Scope...

![virtualbox41.png](/virtualhomelab/virtualbox41.png)

Provide a name, something like "Homelab clients" works.

![virtualbox42.png](/virtualhomelab/virtualbox42.png)

Now we set out the IP ranges we wish to use for our clients, remembering back to the Network configuration we done earlier. 

The INTERNAL nic uses an address of 10.0.0.1 and I want all of the clients connecting to this internal network to be given a 10.0.0.1/24 address so adding those settings to the wizards, lets continue.

![virtualbox43.png](/virtualhomelab/virtualbox43.png)

For exclusions lets not hand out our NIC address as this could cause some confusion in the future if that lease was to expire.

![virtualbox44.png](/virtualhomelab/virtualbox44.png)

The lease duration defaults to 8 days, in this case I've decreased this number by 1 to make it 7 days but adjust according to the network requirements of your homelab.

If you're spinning up lots of client VMs and not releasing the leases before destroying them it may be worth adjusting the lease duration to be shorter.

![virtualbox45.png](/virtualhomelab/virtualbox45.png)

Next up we'll continue onto Gateway setup.

![virtualbox46.png](/virtualhomelab/virtualbox46.png)

Provide the IP address of the INTERNAL NIC here, as we want all network traffic to be filtered/processed by our domain controller.

![virtualbox47.png](/virtualhomelab/virtualbox47.png)

Double-check DNS options, the defaults are good for our use-case. After this next through the wizard till setup is complete.

![virtualbox48.png](/virtualhomelab/virtualbox48.png)

Before moving on Right-click the Server Options menu under IPv4, select Configure options... and select the 003 Router checkbox providing the INTERNAL NIC IP once again.

![virtualbox50.png](/virtualhomelab/virtualbox50.png)

At this point we have a domain controller with no managed computers and a DHCP Scope without leases, just a little more to configure and then we can change that...

## Routing

Returning back to Server manager lets navigate to Tools/Routing and Remote Access.

![virtualbox53.png](/virtualhomelab/virtualbox53.png)

Right-click the server name and select the first option: Configure and Enable Routing and Remote Access.

![virtualbox54.png](/virtualhomelab/virtualbox54.png)
On this screen we select the 2nd option, the explanation underneath clues us in, as to what this option will do.

Without this feature/option being present/configured the internal network would provision nodes with IP addresses as configured in the DHCP scope but those nodes would be unable to access the internet.

![virtualbox55.png](/virtualhomelab/virtualbox55.png)

Select your Internet facing NIC here.

![virtualbox56.png](/virtualhomelab/virtualbox56.png)

Congratulations any clients connecting to the internal network are now handed out an IP lease you configured and can access Internet resources. :thumbsup:

## Connecting a client

Spin up a Windows 10 VM in a similiar fashion to the Windows 2019 Server we setup, the settings should be fairly similiar to the ones pictured below.

Remember the important part here is the VM should reside on the Internal Network only, we want the server to control it's DHCP/Routing.

![virtualbox49.png](/virtualhomelab/virtualbox49.png)

Once installation finishes and you can get to the desktop (a local user of any name is just as great :wink: ), let's navigate over to Advanced System Properties (Under Start ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change... || Start ⇾ Control Panel ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change...) and connect the node to the domain.

Add in the domain name and click OK.

![w10cl1-2.png](/virtualhomelab/w10cl1-2.png)

Enter in Admin credentials here to connect our node.

![w10cl1-3.png](/virtualhomelab/w10cl1-3.png)

Just like that it's connected.

![w10cl1-4.png](/virtualhomelab/w10cl1-4.png)

The system will need a Restart at this point to reconfigure itself, once back at the login screen you should now see an option to not only login with a local account but also domain accounts.

![w10cl1-5.png](/virtualhomelab/w10cl1-5.png)

---

Checking in our DHCP leases and Active Directory Computers, we see our W10 VM has been joined successfully.

![virtualbox57.png](/virtualhomelab/virtualbox57.png)

## Closing thoughts
If you've managed to follow through with this guide, let me congratulate you and if you've skimmed through to check out all the steps before implementation what are you waiting for.

If you break something fix it, break it again, enjoy the process. A homelab needn't be this daunting task which requires you hundreds of hours of setup and big 4U servers all neatly aligned in a rack. 

Some interconnected VMs will teach you a lot, Snapshots mean nothing is truly broken and if you completely, absolutely, catastrophically, f--k up, start again from scratch, cement your knowledge, perhaps try something different that time and maybe just maybe have some **fun**.

## Help from
- [This technet article (accessed through the waybackmachine due to broken image links)](http://web.archive.org/web/20170926171853/https://social.technet.microsoft.com/wiki/contents/articles/36438.windows-server-2016-build-a-windows-domain-lab-at-home-for-free.aspx)
- [Brilliant video from Josh Madakor](https://www.youtube.com/watch?v=MHsI8hJmggI)

[^1]: A forest in this scenario is the top-most "block" for how resources are managed by Windows Server (resources meaning users, domains, computers etc)