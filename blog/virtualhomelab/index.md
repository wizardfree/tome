---
title: "Create a Windows Domain Homelab in Virtualbox"
description: "The Step-by-Step process to installing and configuring a Windows Server domain in a private network using Virtualbox."
date: 2022-03-31T14:59:09.406Z
draft: false
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

{{< figure src="virtualbox2.webp" alt="VirtualBox screenshot" title="Screenshot of VirtualBox showing the name and operating system fields." link="virtualbox2.webp" >}}

Allocate an adequate amount of memory to the VM.

{{< box warning >}}
**Minimum RAM requirements**

[RAM · 512 MB (2 GB for Server with Desktop Experience installation option)](https://docs.microsoft.com/en-us/windows-server/get-started/hardware-requirements)

{{< /box>}}

{{< figure src="virtualbox3.webp" alt="VirtualBox screenshot" title="Screenshot of VirtualBox showing the memory size selector." link="virtualbox3.webp" >}}

Create a virtual HDD with default options, this will be more than adequate for testing purposes.

{{< figure src="virtualbox4.webp" alt="VirtualBox screenshot" title="Select Create a Virtual hard disk now." link="virtualbox4.webp" >}}

{{< figure src="virtualbox5.webp" alt="VirtualBox screenshot" title="Select VDI (Virtual Disk Image)." link="virtualbox5.webp" >}}

{{< figure src="virtualbox6.webp" alt="VirtualBox screenshot" title="Select Dynamically allocated." link="virtualbox6.webp" >}}

{{< figure src="virtualbox7.webp" alt="VirtualBox screenshot" title="Name the VDI and set the disk size." link="virtualbox7.webp" >}}

Assign CPU cores to the VM, in this case 4 although 2 cores is fine.

{{< figure src="virtualbox8.webp" alt="VirtualBox screenshot" title="Setting the number of processor cores." link="virtualbox8.webp" >}}

Tick the Enable 3D Acceleration checkbox and allocate more video memory to the VM. As we will install the Desktop Experience version of Windows Server more video memory is beneficial here.

{{< figure src="virtualbox9.webp" alt="VirtualBox screenshot" title="Setting the amount of Video Memory." link="virtualbox9.webp" >}}

Attach the Windows Server ISO.

{{< figure src="virtualbox10.webp" alt="VirtualBox screenshot" title="Attach the ISO file." link="virtualbox10.webp" >}}

Assign the first NIC to NAT to grab an IP dynamically and have access to the Internet.

Assign the second NIC to an Internal Network, this will seperate the Windows 10 Clients from your network.

{{< figure src="virtualbox11.webp" alt="VirtualBox screenshot" title="Set network adaptor 1 to NAT." link="virtualbox11.webp" >}}

{{< figure src="virtualbox12.webp" alt="VirtualBox screenshot" title="Set network adaptor 2 to Internal Network." link="virtualbox12.webp" >}}

If all the settings look good, lets move onto installation.

## Installing Server 2019
The Windows installation experience for both Desktop and Server is straight-forward even more so within a VM, click Next, agree to terms, click Next some more. Done.

{{< figure src="virtualbox14.webp" alt="VirtualBox screenshot" title="Windows Server 2019 OOBE." link="virtualbox14.webp" >}}

Ensure the (Desktop Experience) version is selected otherwise all further configuration will be done through the command-line
only.

Differences between Standard and Datacenter editions boil down to Hyper-V Virtual Machine limits/licensing and the Datacenter edition having support for Software-defined Networking.

Choose either as the server will ONLY be for testing, if unsure Standard will do fine for our purposes.

{{< figure src="virtualbox15.webp" alt="VirtualBox screenshot" title="Select Windows Server 2019 Standard (Desktop Experience)." link="virtualbox15.webp" >}}

{{< figure src="virtualbox16.webp" alt="VirtualBox screenshot" title="Select the attached VDI." link="virtualbox16.webp" >}}

{{< figure src="virtualbox17.webp" alt="VirtualBox screenshot" title="Windows Server 2019 Installing..." link="virtualbox17.webp" >}}

Once installation has finished the VM may restart a number of
times before reaching the following screen (see image below).

Choose a [strong, memorable password](https://xkcd.com/936/) and let the installation finish.

{{< figure src="virtualbox18.webp" alt="VirtualBox screenshot" title="P@ssw0rd! is not a good choice..." link="virtualbox18.webp" >}}

Once at the Desktop, Server Manager will start automatically.
To make out lives easier we will change the name for our Server.

Under Start ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change... || Start ⇾ Control Panel ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change...

{{< figure src="virtualbox24.webp" alt="VirtualBox screenshot" title="Change the hostname to something more memorable." link="virtualbox24.webp" >}}

{{< figure src="virtualbox39.webp" alt="VirtualBox screenshot" title="Restart to accept the changes to the hostname." link="virtualbox39.webp" >}}

## (Optional) VirtualBox Guest Additions
The following steps are optional and are done to enable better display options for the VM as well as Shared Clipboard/Folders
between host and VM.

Insert the Guest Additions ISO through the VirtualBox context menu.
If this is the first time Guest Additions have been used or a suitable image cannot be found locally you will be prompted to download the latest supported Guest Additions ISO.

{{< figure src="guest-additions.webp" alt="VirtualBox screenshot" title="Select Insert Guest Additions CD image..." link="guest-additions.webp" >}}

The ISO will act just like a CD Drive with an inserted disc.

{{< figure src="virtualbox20.webp" alt="VirtualBox screenshot" title="Guest Additions as it appears in Windows Explorer." link="virtualbox20.webp" >}}

Install the additions using the provided executable for your architecture.

{{< figure src="virtualbox21.webp" alt="VirtualBox screenshot" title="Install as Administrator for your architecture." link="virtualbox21.webp" >}}

Once the installation wizard finishes you will be prompted to reboot. Do so now.

{{< figure src="virtualbox22.webp" alt="VirtualBox screenshot" title="Restart to accept the changes to the Virtual Machine." link="virtualbox22.webp" >}}

Once the VM reboots and you login the desktop should automagically scale properly. If not allow the VM to fully boot and then check the VirtualBox context menu: View ⇾ Auto-resize Guest Display is active (not greyed-out).

{{< figure src="virtualbox23.webp" alt="VirtualBox screenshot" title="Look at all that room for activities..." link="virtualbox23.webp" >}}

## Network Setup
Now the fun stuff, as per our VM setup earlier under Network Connections || ipconfig, we see 2 virtual NICs (Network Interface Cards) show up.
Windows will default some settings such as the names for these interfaces (Ethernet, Ethernet 2) and attempt IP configuration dynamically.
We now need to override these default values to something more useful.
Pictured below is the 2 virtual NICs shown in Network
Connections.

{{< figure src="virtualbox25.webp" alt="VirtualBox screenshot" title="Both network adaptors as they appear in Network Connections." link="virtualbox25.webp" >}}

(Optional) Start by renaming the NICs as to make them more readable quickly. Ethernet and Ethernet 2 aren't particulary
distinct at a glance.

In my case INTERNET and INTERNAL also aren't particulary distinct but add some flair to yours, go wild.

{{< figure src="virtualbox26.webp" alt="VirtualBox screenshot" title="Alpha and Omega perhaps..." link="virtualbox26.webp" >}}

Firing up PowerShell we can run ipconfig to check out the current IP configuration for the Server at a glance.
Currently the NIC connected the Internet is acquiring it's IP configuration dynamically if you wish to set a static IP nows the time however in this case I'm happy to let it stay dynamic.

The Internal NIC however will require some configuration on our part.

Looking at the Internal NIC configuration currently we see the 169.254... tell-tell sign of an APIPA (Automatic Private Internet Protocol Addressing) address currently meaning that this isn't a lot of use to us.

{{< figure src="virtualbox27.webp" alt="VirtualBox screenshot" title="PowerShell output of the ipconfig command." link="virtualbox27.webp" >}}

Diving into the IPv4 properties for the INTERNAL NIC we'll start by deselecting the Obtain an IP address automatically radiobox instead opting for the Use the following IP address option.

Next we begin the definition of out private network. Choose your address range in this case 10.0.0.1/24 (in honesty a whack 24 is much too large for this scenario 2^8^ = 256 hosts but for simplicity /24 is easy to remember and write down). You don't have to use this address range any valid address range will work, remember this is a private network the hosts connected will have no direct access to the Internet.

NOTE: leave the Gateway address blank this allows for all routing to be done through the Server.

The Preferred DNS address should be the same as the address for the Internet facing NIC. This is another reason to go for a static IP for that NIC.

{{< figure src="virtualbox28.webp" alt="VirtualBox screenshot" title="Double-check that DNS server address." link="virtualbox28.webp" >}}

With the NICs setup we move onto the Domain...

## Domain Setup
Time to start utilising the domain controller capabilities of Windows Server.

Start by launching the Add Roles and Features Wizard (Server Manager has a quick link to it under option 2).

Select the first option for Role-based or feature-based installation and click next.

{{< figure src="virtualbox29.webp" alt="VirtualBox screenshot" title="Add Roles and Feature Wizard." link="virtualbox29.webp" >}}

(I've omitted the Server selection step as this is straight forward in our example, we only have 1 server to manage!)
Scroll down the list selecting the following: Active Directory Domain Services, DHCP Server, DNS Server AND Remote Access (I forgot this at the time of initial installation whoops)  (NOTE:

Selecting some of these options will present a pop-up window asking to also select additional required packages, skim the packages and accept.)

Once all selected click next.

{{< figure src="virtualbox30.webp" alt="VirtualBox screenshot" title="Select Active Directory Domain Services, DHCP Server, and DNS Server." link="virtualbox30.webp" >}}

{{< figure src="virtualbox51.webp" alt="VirtualBox screenshot" title="Don't forget Remote Access..." link="virtualbox51.webp" >}}

{{< figure src="virtualbox52.webp" alt="VirtualBox screenshot" title="Select Routing." link="virtualbox52.webp" >}}

Click next until the confirmation page is reached. Check the
Restart if neccessary checkbox and click Install.

{{< figure src="virtualbox31.webp" alt="VirtualBox screenshot" title="Confirm choices and Click Install." link="virtualbox31.webp" >}}

Grab a coffee and let the installation happen. The server may restart at this point again let the server finalise installation.

Once completed the Server Manager will be displaying the warning sign in the top right, click on this to continue onto
Post-installation configuration.

For now we'll address the Domain Services issue which has been highlighted by the Server Manager.

Click on the link: Promote this server to a domain controller, to continue.

{{< figure src="virtualbox32.webp" alt="VirtualBox screenshot" title="Select Promote this server to a domain controller." link="virtualbox32.webp" >}}

On the window which pops up we'll be creating a new forest. [^1]
Specify a root domain name this may be a domain you own or simply use one for testing. (foobar.local works nicely :wink:)
Happy? Click next and next again.

{{< figure src="virtualbox33.webp" alt="VirtualBox screenshot" title="Adding the Root domain name." link="virtualbox33.webp" >}}

On the review screen I've highlighted some important information which appears at the the bottom of the scrollable pane. Two important points are mentioned:

1. Firstly the DNS Server (service) will configured on this computer and this computer will be configured as its own preferred DNS server.

2. Secondly the password for the domain administrator account will be the same as the local administrator account of the server. (If the local admin password is weak now might be good time to change it)

Why is it important to have a DNS service running on our server well:

{{< box info >}}

...when a network user with an Active Directory user account logs in to an Active Directory domain, the DNS Client service queries the DNS server to locate a domain controller for the Active Directory domain... ([From the horses mouth](https://docs.microsoft.com/en-us/windows-server/networking/dns/dns-top##:~:text=when%20a%20network%20user%20with%20an%20Active%20Directory%20user%20account%20logs%20in%20to%20an%20Active%20Directory%20domain%2C%20the%20DNS%20Client%20service%20queries%20the%20DNS%20server%20to%20locate%20a%20domain%20controller%20for%20the%20Active%20Directory%20domain.))

{{< /box >}}

Click next.

{{< figure src="virtualbox34.webp" alt="VirtualBox screenshot" title="Review and Click Next." link="virtualbox34.webp" >}}

A couple warnings are thrown up during the prerequisite checks but nothing that bothers us for our example.

Clicking next at this point will begin the installation.

{{< figure src="virtualbox35.webp" alt="VirtualBox screenshot" title="Installing..." link="virtualbox35.webp" >}}

Once installation is finished the server will restart and once it gets back to the login screen you should now see DOMAIN\Administrator as the prompt (DOMAIN being whatever the root domain NETBIOS name was set to).

Remebering back to the review screen the password for this Domain Administrator account is the same as the local Administrator account, using that we can sign in as usual.

Before we begin connecting clients to this domain we need to continue setup on our private network for our clients namely their leases...

## DHCP Setup
To setup our DHCP (Dynamic Host Configuration Protocol) configuration, we begin by navigating to the DHCP tool either through the Start Menu or Server Manager/Tools/DHCP.

{{< figure src="virtualbox40.webp" alt="VirtualBox screenshot" title="DHCP settings can be found under Tools in Server Manager." link="virtualbox40.webp" >}}

We should see only 1 server present under the DHCP tree menu in the left-hand pane, expanding this server option, then further expanding IPv4 we can right-click on the IPv4 menu item to select New Scope...

{{< figure src="virtualbox41.webp" alt="VirtualBox screenshot" title="Create a New Scope." link="virtualbox41.webp" >}}

Provide a name, something like "Homelab clients" works.

{{< figure src="virtualbox42.webp" alt="VirtualBox screenshot" title="Add a name." link="virtualbox42.webp" >}}

Now we set out the IP ranges we wish to use for our clients, remembering back to the Network configuration we done earlier.

The INTERNAL nic uses an address of 10.0.0.1 and I want all of the clients connecting to this internal network to be given a 10.0.0.1/24 address so adding those settings to the wizards, lets continue.

{{< figure src="virtualbox43.webp" alt="VirtualBox screenshot" title="Add the DHCP scope." link="virtualbox43.webp" >}}

For exclusions lets not hand out our NIC address as this could cause some confusion in the future if that lease was to expire.

{{< figure src="virtualbox44.webp" alt="VirtualBox screenshot" title="Remember to exclude the NIC IP." link="virtualbox44.webp" >}}

The lease duration defaults to 8 days, in this case I've decreased this number by 1 to make it 7 days but adjust according to the network requirements of your homelab.

If you're spinning up lots of client VMs and not releasing the leases before destroying them it may be worth adjusting the lease duration to be shorter.

{{< figure src="virtualbox45.webp" alt="VirtualBox screenshot" title="Play around with the lease times to best fit your environment." link="virtualbox45.webp" >}}

Next up we'll continue onto Gateway setup.

{{< figure src="virtualbox46.webp" alt="VirtualBox screenshot" title="Select Yes, and Next." link="virtualbox46.webp" >}}

Provide the IP address of the INTERNAL NIC here, as we want all network traffic to be filtered/processed by our domain controller.

{{< figure src="virtualbox47.webp" alt="VirtualBox screenshot" title="Bet you have this memorised by now." link="virtualbox47.webp" >}}

Double-check DNS options, the defaults are good for our use-case. After this next through the wizard till setup is complete.

{{< figure src="virtualbox48.webp" alt="VirtualBox screenshot" title="Confirm and Next." link="virtualbox48.webp" >}}

Before moving on Right-click the Server Options menu under IPv4, select Configure options... and select the 003 Router checkbox providing the INTERNAL NIC IP once again.

{{< figure src="virtualbox50.webp" alt="VirtualBox screenshot" title="The traffic needs somewhere to go..." link="virtualbox50.webp" >}}

At this point we have a domain controller with no managed computers and a DHCP Scope without leases, just a little more to configure and then we can change that...

## Routing

Returning back to Server manager lets navigate to Tools/Routing and Remote Access.

{{< figure src="virtualbox53.webp" alt="VirtualBox screenshot" title="Server Manager > Tools > Routing and Remote Access." link="virtualbox53.webp" >}}

Right-click the server name and select the first option: Configure and Enable Routing and Remote Access.

{{< figure src="virtualbox54.webp" alt="VirtualBox screenshot" title="Configure and Enable Routing and Remote Access." link="virtualbox54.webp" >}}

On this screen we select the 2nd option, the explanation underneath clues us in, as to what this option will do.

Without this feature/option being present/configured the internal network would provision nodes with IP addresses as configured in the DHCP scope but those nodes would be unable to access the internet.

{{< figure src="virtualbox55.webp" alt="VirtualBox screenshot" title="Select Network address translation (NAT)." link="virtualbox55.webp" >}}

Select your Internet facing NIC here.

{{< figure src="virtualbox56.webp" alt="VirtualBox screenshot" title="Select the External / Internet facing network adaptor." link="virtualbox56.webp" >}}

Congratulations any clients connecting to the internal network are now handed out an IP lease you configured and can access Internet resources. :thumbsup:

## Connecting a client

Spin up a Windows 10 VM in a similiar fashion to the Windows 2019 Server we setup, the settings should be fairly similiar to the ones pictured below.

Remember the important part here is the VM should reside on the Internal Network only, we want the server to control it's DHCP/Routing.

{{< figure src="virtualbox49.webp" alt="VirtualBox screenshot" title="VM settings in VirtualBox Manager." link="virtualbox49.webp" >}}

Once installation finishes and you can get to the desktop (a local user of any name is just as great :wink: ), let's navigate over to Advanced System Properties (Under Start ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change... || Start ⇾ Control Panel ⇾ System ⇾ System Info ⇾ Advanced system settings ⇾ Change...) and connect the node to the domain.

Add in the domain name and click OK.

{{< figure src="w10cl1-2.webp" alt="VirtualBox screenshot" title="Joining the client VM to the Domain." link="w10cl1-2.webp" >}}

Enter in Admin credentials here to connect our node.

{{< figure src="w10cl1-3.webp" alt="VirtualBox screenshot" title="Enter the admin credentials." link="w10cl1-3.webp" >}}

Just like that it's connected.

{{< figure src="w10cl1-4.webp" alt="VirtualBox screenshot" title="Success." link="w10cl1-4.webp" >}}

The system will need a Restart at this point to reconfigure itself, once back at the login screen you should now see an option to not only login with a local account but also domain accounts.

{{< figure src="w10cl1-5.webp" alt="VirtualBox screenshot" title="Windows login screen confirming connection to the domain." link="w10cl1-5.webp" >}}

---

Checking in our DHCP leases and Active Directory Computers, we see our W10 VM has been joined successfully.

{{< figure src="virtualbox57.webp" alt="VirtualBox screenshot" title="ADUC confirming the Client VM has joined." link="virtualbox57.webp" >}}

## Closing thoughts
If you've managed to follow through with this guide, let me congratulate you and if you've skimmed through to check out all the steps before implementation what are you waiting for.

If you break something fix it, break it again, enjoy the process. A homelab needn't be this daunting task which requires you hundreds of hours of setup and big 4U servers all neatly aligned in a rack.

Some interconnected VMs will teach you a lot, Snapshots mean nothing is truly broken and if you completely, absolutely, catastrophically, f--k up, start again from scratch, cement your knowledge, perhaps try something different that time and maybe just maybe have some **fun**.

## Help from
- [This technet article (accessed through the waybackmachine due to broken image links)](http://web.archive.org/web/20170926171853/https://social.technet.microsoft.com/wiki/contents/articles/36438.windows-server-2016-build-a-windows-domain-lab-at-home-for-free.aspx)
- [Brilliant video from Josh Madakor](https://www.youtube.com/watch?v=MHsI8hJmggI)

[^1]: A forest in this scenario is the top-most "block" for how resources are managed by Windows Server (resources meaning users, domains, computers etc)
