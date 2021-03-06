---
title: "Common Windows Group Policies"
date: 2022-04-01T15:31:31.204Z
description: "[Updated: 08/07/22] A selection of common/useful Group Policies for Windows."
draft: false
toc: true
author: Joseph Fleet
slug: windows.group.policies
tags:
- Windows
- Tips
- Windows Server
---

Group Policies can be managed (at the domain level) with the Group Policy Management MMC (Microsoft Management Console) snap-in.

Server Manager ⇾ Tools ⇾ Group Policy Management
The following are a number of common/useful GPOs (Group Policy Objects) which can help to manage Users and Windows Clients.
If looking for GPO best practices go [here](/404) instead.

---
For each policy we'll start from with the Group Policy Management snap-in under the domain, Group Policy Objects ⇾ Right-Click ⇾ New: [GPO Name]
![createpolicy.gif](/group-policy/createpolicy.gif)

Then under Group Policy Objects ⇾ Right-Click ⇾ Edit:
![editpolicy.gif](/group-policy/editpolicy.gif)
## **Password Policy**
Computer Configuration ⇾ Policies ⇾ Windows Settings ⇾ Security Settings ⇾ Account Policies ⇾ Password Policy
![password-policy-example.png](/group-policy/password-policy-example.png)

## **Account Lockout Policy**
Computer Configuration ⇾ Policies ⇾ Windows Settings ⇾ Security Settings ⇾ Account Policies ⇾ Account Lockout Policy 
![account-lockout-example.png](/group-policy/account-lockout-example.png)

## **Disabled Windows Update Restarts**
Computer Configuration ⇾ Policies ⇾ Administrative Templates ⇾ Windows Component ⇾ Windows Update ⇾ Select: No auto-restart with logged on users for scheduled automatic updates installations
![auto-restart.png](/group-policy/auto-restart.png)

## **Prohibit User Software Install**
Computer Configuration ⇾ Policies ⇾ Administrative Templates ⇾ Windows Component ⇾ Windows Installer ⇾ Select: Prohibit User Install
![prohibit-user-install.png](/group-policy/prohibit-user-install.png)

## **Block All Removable Media**
User Configuration ⇾ Policies ⇾ Administrative Templates ⇾ System ⇾ Removable Storage Access ⇾ Select: All Removable Storage classes: Deny all access
![block-removable.png](/group-policy/block-removable.png)

## **Disable Guest Account**
Computer Configuration ⇾ Windows Settings ⇾ Security Settings ⇾ Local Policies ⇾ Security Options ⇾ Select: Accounts:Guest acount status
![guest-gpo.png](/group-policy/guest-gpo.png)

## **Disable Control Panel Access**
User Configuration ⇾ Policies ⇾ Administrative Templates ⇾ Control Panel ⇾ Select: Prohibit access to Control Panel and PC settings
![prohibit-control.png](/group-policy/prohibit-control.png)

## **Disable Command Prompt Access**
User Configuration ⇾ Policies ⇾ Administrative Templates ⇾ System ⇾ Select: Prevent access to the command prompt
![prohibit-cmd.png](/group-policy/prohibit-cmd.png)

## ![newmove.gif](/newmove.gif) **Map Shared Network Drive**
User Configuration ⇾ Preferences ⇾ Windows Settings ⇾ Drive Maps ⇾ Right Click: New > Mapped Drive

![mapdrive1.png](/group-policy/mapdrive1.png)
![mapdrive2.png](/group-policy/mapdrive2.png)