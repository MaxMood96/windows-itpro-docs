---
title: Uninstall Microsoft Connected Cache for Enterprise and Education cache nodes
description: Details on how to uninstall Microsoft Connected Cache for Enterprise and Education from a host machine.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.author: lichris
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a> 
ms.date: 10/30/2024
---

# Uninstall Connected Cache software from a host machine

This article describes how to uninstall Microsoft Connected Cache for Enterprise and Education caching software from a host machine. These steps should be taken after deleting the cache node in the Azure portal.

## Steps to uninstall Connected Cache from a Windows host machine

1. Launch a PowerShell window *as administrator* and navigate to the Connected Cache installation directory (C:\mcconwsl01 by default)
1. Run the `uninstallmcconwsl.ps1` script

## Steps to uninstall Connected Cache from a Linux host machine

The `uninstallmcc.sh` script within the provisioning package uninstalls the Connected Cache caching software and all related components, including:

- IoT Edge
- IoT Edge Agent
- IoT Edge Hub
- Connected Cache container
- Moby CLI
- Moby engine
