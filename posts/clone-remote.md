---
title: "🐑 Dolly the sheep approves this message"
date: 2022-07-12T18:12:13+01:00
description: "Using Clonezilla to image and clone OS installs using a remote file share for storage."
draft: false
toc: true
author: Joseph Fleet
slug: clone.node.remote
tags:
- Software
- Operating Systems
- Imaging
---
## Introduction
Today we explore the wild world of cloning[^1] and imaging[^2] using [Clonezilla](https://clonezilla.org/) an opensource disk imaging and cloning soltution, but first to clear up any confusion [Dolly the sheep](https://www.history.com/this-day-in-history/first-successful-cloning-of-a-mammal) is the first mammal to be succesfully cloned which is fitting for our subject matter.
### How cloning feels:
![Spiderman points at himself](https://i.kym-cdn.com/entries/icons/mobile/000/023/397/C-658VsXoAo3ovC.jpg)

## The problem
Pictured below is the a Virtual Machine running Windows 10 Professional, the OS has been customised and new applications have been installed.

![clonezilla1](/clone-remote/clonezilla1.png)

There is another Virtual Machine configured with the same hardware that has no OS. 

One option available is to do a High touch Windows install then replicate the customisations and application installs or perhaps even perform a Low/Zero touch installation which performs the OS install, adds the customisations AND installs required applications. 

This however requires a decent time-investment, introduces multiple points of failure and limits the duplication to Windows machines only. As alluded to earlier there is another way, enter [Clonezilla](https://clonezilla.org/) stage left.

## Stage left

Adding the [Clonezilla](https://clonezilla.org/) stable iso to the virtual machine will show the following at the system boot:

![clonezilla3](/clone-remote/clonezilla3.png)

Selecting the first option or waiting for 30 seconds will proceed to the language selection screen, then the keyboard locale selection.

![clonezilla4](/clone-remote/clonezilla4.png)

After starting Clonezilla (after Language/Locale selection) the following options are presented:
- device-image  : use this option for working with images
- device-device : for when duplicating from disk to disk
- remote-source : used to select node to disk duplicate remotely
- remote-dest   : remotely disk duplicate a node
- lite-server   : massive deployment from an image via multicast mechanism
- lite-client   : used in conjunction with above

In this example the first option will be used to work with images.

![clonezilla8](/clone-remote/clonezilla8.png)

Next is the selection of where the image should be saved, in this example a Samba share running on Windows Server 2019 will be used.

Other options here include:
- local disks, whether those be hard drives or removable media
- NFS servers
- AWS instances

![clonezilla9](/clone-remote/clonezilla9.png)

As access outside the local node is needed IP configuration is prompted.
Checking the Windows Server VMs IP address (10.0.0.163), it can be entered in the next screen.

![clonezilla10](/clone-remote/clonezilla10.png)
![clonezilla12](/clone-remote/clonezilla12.png)

An account with adequate permissions is needed to access the share. Adequate in this scenario means Full Control or RWX (7) permissions due the creation of directories, writing to and reading of files.

Next the location for the image is chosen, again adequate permissions are needed to write to this directory/share.

For this example a bad practice is used by specifying the Administrator account however due to the limited nature of the Virtual Machine environment it's acceptable here.

![clonezilla13](/clone-remote/clonezilla13.png)
![clonezilla14](/clone-remote/clonezilla14.png)

The password for the supplied account is required here, if the credentials are validated for the provided share a success output will be shown in the terminal output.

![clonezilla15](/clone-remote/clonezilla15.png)
![clonezilla16](/clone-remote/clonezilla16.png)

Many options are presented here but in this case the first option is one required as the image requires a complete duplication of data structure (partitions) on the disk.

![clonezilla18](/clone-remote/clonezilla18.png)

A name for the image is auto-populated but can be modified now. After which the local disks are displayed. The disk to be imaged is selected here.

![clonezilla19](/clone-remote/clonezilla19.png)
![clonezilla20](/clone-remote/clonezilla20.png)

### Options

In the following order various options are presented:

1. Which type of compression to use? Typically z1p is more than adequate.
2. Perform a file system check on the desired local disk BEFORE imaging. This check is only for Linux file systems such as ext3/4 or xfs NOT NTFS file systems.
3. Should the image be encrypted? This decision is subjective to how/where the images are stored, what data is being stored in the image etc.

Once all option screens are cleared a final confirmation is required before the imaging begins.

![clonezilla21](/clone-remote/clonezilla21.png)
![clonezilla22](/clone-remote/clonezilla22.png)
![clonezilla23](/clone-remote/clonezilla23.png)
![clonezilla24](/clone-remote/clonezilla24.png)

### Imaging in progress

![clonezilla25](/clone-remote/clonezilla25.png)

## 🐑 🐑

To clone using the image which was just created first a VM is spun up booting from the [Clonezilla](https://clonezilla.org/) stable iso.
Then following the same steps till the Select mode screen of the device-image option is presented. Instead of the first option, instead the third option is selected for a restoration of an image to a local disk.

![clonezilla26](/clone-remote/clonezilla26.png)
![clonezilla28](/clone-remote/clonezilla28.png)

If credentials are validated for the share then a list of image files will be presented. Selecting the newly created image and then the applicable local disk the cloning process starts.

![clonezilla29](/clone-remote/clonezilla29.png)
![clonezilla31](/clone-remote/clonezilla31.png)
![clonezilla30](/clone-remote/clonezilla30.png)
![clonezilla32](/clone-remote/clonezilla32.png)

## Conclusion
[Clonezilla](https://clonezilla.org/) is a powerful imaging tool with support for 40 devices simultaneously being imaged hopefully from what's been shown above you can appreciate some of this power. However [Clonezilla](https://clonezilla.org/) is not the only tool in this space, other offerings include:
- [NinjaOne](https://www.ninjaone.com/backup/): A Remote Monitoring and Management (RMM) system used by MSPs.
- [SmartDeploy](https://www.smartdeploy.com/): SmartDeploy provides the capability of storing and deploying your golden Windows image, software, scripts, and drivers using Box, Dropbox, Google Drive, or OneDrive.
- [Symantec Ghost](https://www.broadcom.com/products/cyber-security/endpoint/management/ghost-solutions-suite): Symantec Ghost Solution Suite is an award-winning software solution for imaging and deploying desktops, laptops, tablets and servers.

In the future I would love to get hands-on with other imaging tools to see how they compare against each other.

[^1]: [Cloning](https://www.techopedia.com/definition/31923/cloning-programming) is ... the act of making the exact copy of a directory file or disk inclusive of any subdirectories or files within the disk or directory.

[^2]: A [disk image](https://www.techopedia.com/definition/12705/disk-image) is a single file or storage device that holds a replica of all data on a storage medium or device.