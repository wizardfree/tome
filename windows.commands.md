---
title: "Windows Commands"
date: 2022-03-31T14:43:37.949Z
description: "Common Windows Commands."
draft: false
toc: true
author: Joseph Fleet
slug: sporadic.strunting.blunderbuss
tags:
- Windows
---

## *ipconfig*
> Displays all current TCP/IP network configuration values and refreshes Dynamic Host Configuration Protocol (DHCP) and Domain Name System (DNS) settings.


```cmd
C: ipconfig /? : Displays help output

C:\ipconfig /all : Displays TCP/IP network information about ALL current adapters.

C:\ipconfig /flushdns : Clears the DNS resolver cache.

C:\ipconfig /release : Forces ALL attached adapters to release their DHCP leases.

C:\ipconfig /release [adapter] : Releases the specified adapter (e.g. ethernet) DHCP lease.

C:\ipconfig /renew : Renews DHCP configuration for adapters which are configured with automatic IP configuration.

C:\ipconfig /renew [adapter] : Renews DHCP configuration for specified adapter.
```

## *ping*
> Verifies IP-level connectivity to another TCP/IP computer by sending Internet Control Message Protocol (ICMP) echo Request messages.
{.is-info}

```cmd
C:\ping /? : Displays help output

C:\ping foobar.uk : Sends 3 ICMP packets to specified FQDN (Fully Qualified Domain Name) or IP address.

C:\ping foobar.uk /t : Continously sends ICMP packets to specified FQDN or IP address. (To interrupt and display statistics, press <kbd>CTRL</kbd>+<kbd>ENTER</kbd>. To interrupt and quit this command, press <kbd>CTRL</kbd>+<kbd>C</kbd>.)

C:\ping foobar.uk /n # : Sends specified number of ICMP packets.
```

## *netstat*
> Displays active TCP connections, ports on which the computer is listening, Ethernet statistics, the IP routing table, IPv4 statistics, and IPv6 statistics.

```cmd
C:\netstat /a : Displays all active connections w/ TCP/UDP port numbers.

C:\netstat /b : Displays the executable which is making the connection. Requires elevated prompt.

C:\netstat /n : Displays address and port numbers in numeric representation only.

C:\netstat /o : Shows the PID (Process IDentifier) which is making the connection.
```

## *tracert*
> This diagnostic tool determines the path taken to a destination by sending Internet Control Message Protocol (ICMP) echo Request or ICMPv6 messages to the destination with incrementally increasing time to live (TTL) field values.

```cmd
C:\tracert foobar.uk : Traces the path to the specified domain.
C:\tracert -d foobar.uk : Traces the path to the specified domain w/o resolving IP addresses to hostnames (may speed up the pathing process).
```

## *systeminfo*
> Displays detailed configuration information about a computer and its operating system, including operating system configuration, security information, product ID, and hardware properties (such as RAM, disk space, and network cards).

```cmd
C:\systeminfo : Displays system info.

C:\systeminfo -s <host> : Displays information for host on the local network.

C:\systeminfo -u <domain>\<user> -p <password> : Runs the command using the credentials of the specified user, default behaviour uses the currently logged-in account.
```

## *sfc*
> Scans and verifies the integrity of all protected system files and replaces incorrect versions with correct versions.

```cmd
C:\sfc /scannow : Scans the integrity of all protected system files and attempts to repair files.

C:\sfc /verifyonly : Scans but does not attempt repairs.
```

## *taskkill*
> Ends one or more tasks or processes.
> Replaces the *kill* command.

```cmd
C:\taskkill /im <program_name> : Ends tasks which match the specified program name.

C:\taskkill /pid <PID> : Ends task with specified PID.

C:\taskkill ... /f : Forcefully kill task.
```

## *cls*
> Clears the Command Prompt window.

```cmd
C:\cls : Similair to BASH `clear` command.
```

## *gpresult*
> Displays the Resultant Set of Policy [^1] (RSoP) information for a remote user and computer.

```cmd
C:\gpresult /r : Displays RSoP information for local computer.

C:\gpresult ... /h <filepath> : Saves report to HTML file at specified path.
```

[^1]: Resultant Set of Policy (RSoP) is an addition to Group Policy to assist in policy implementation and troubleshooting.

