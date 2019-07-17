---
title: Manage Windows 10 delta updates
titleSuffix: Configuration Manager
description: Configuration Manager supports delta installation files for Windows 10, which provide smaller downloads and faster installation times on clients.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.collection: M365-identity-device-management
---

# Manage delta installation files for Windows 10 updates

Configuration Manager supports delta installation files for Windows 10 updates. Configure the client to download only the changes between the current month's Windows 10 cumulative quality update and the previous month's update. Without delta installation files, Configuration Manager clients download the full Windows 10 cumulative update each month, including all updates from previous months. Using delta installation files provides for smaller downloads and faster installation times on clients.

To learn how to use Configuration Manager to manage update content to stay current with Windows 10, see [Optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).  


> [!IMPORTANT]  
> The OS client support is available in Windows 10, version 1607, with an update to the Windows Update Agent. This update is included with the updates released on April 11, 2017. For more information about these updates, see [support article 4015217](http://support.microsoft.com/kb/4015217). Future updates leverage delta for smaller downloads. Prior versions of Windows 10, and Windows 10 version 1607 without this update don't support delta installation files.  


### Enable the site to download delta installation files for Windows 10 updates
To start synchronizing the metadata for Windows 10 delta installation files, enable it in the properties of the software update point.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. Select the central administration site or the stand-alone primary site.  

3. In the ribbon, click **Configure Site Components**, and then click **Software Update Point**. Switch to the **Update Files** tab, and select **Download both full files for all approved updates and express installation files for Windows 10**.

> [!NOTE]    
> You can't configure the software update point component to *only* download delta updates.  The site downloads the delta installation files in addition to the full files. This increases the amount of content stored in the content library, and distributed to and stored on your distribution points.

> [!Tip]  
> To determine the actual space being used on disk by the file, check the **Size on disk** property of the file. The Size on disk property should be considerably smaller than the Size value. For more information, see [FAQs to optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq).  


### Enable clients to download and install delta installation files
To enable delta installation files support on clients, enable delta installation files in the **Software Updates** group of client settings. This setting creates a new HTTP listener that listens for requests to download delta installation files on the port that you specify.

> [!NOTE]    
> This is a local port that clients use to listen for requests from Delivery Optimization or Background Intelligent Transfer Service (BITS) to download delta content from the distribution point. You don't need to open this port on firewalls because all traffic is on the local computer.  

Once you deploy client settings to enable this functionality on the client, it attempts to download the delta between the current month's Windows 10 cumulative update and the previous month's update. Clients must run a version of Windows 10 that supports delta installation files.  

1. Enable support for delta installation files in the properties of the software update point component (previous procedure).  

2. In the Configuration Manager console, go to the **Administration** workspace, and select **Client Settings**.  

3. Select the appropriate client settings, and click **Properties** on the ribbon.  

4. Select the **Software Updates** group. Configure to **Yes** the setting to **Allow clients to update with Delta content when available**. Configure the **Port used to download content for delta content** with the port used by the HTTP listener on the client.
