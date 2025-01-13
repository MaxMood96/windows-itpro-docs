---
title: Verify Microsoft Connected Cache for Enterprise and Education cache node functionality
description: Details on how to verify functionality of Microsoft Connected Cache for Enterprise and Education cache nodes.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 10/30/2024
appliesto: 
- ✅ Windows-hosted Connected Cache cache nodes
- ✅ Linux-hosted Connected Cache cache nodes
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Verify Connected Cache node functionality

This article describes how to verify that a Microsoft Connected Cache for Enterprise and Education cache node is functioning correctly.

These steps should be taken after deploying Connected Cache software to a [Windows](mcc-ent-deploy-to-windows.md) or [Linux](mcc-ent-deploy-to-linux.md) host machine.

## Steps to verify functionality of Connected Cache node

1. To verify that the Connected Cache container on the host machine is running and reachable, run the following command from the host machine:

    ```powershell
    wget http://localhost/filestreamingservice/files/7bc846e0-af9c-49be-a03d-bb04428c9bb5/Microsoft.png?cacheHostOrigin=dl.delivery.mp.microsoft.com
    ```

    If successful, there should be an HTTP response with StatusCode 200.

1. To verify that Windows clients in your network can reach the Connected Cache node, visit the following address from a web browser on a Windows client device:

    `http://[HostMachine-IP-address]/filestreamingservice/files/7bc846e0-af9c-49be-a03d-bb04428c9bb5/Microsoft.png?cacheHostOrigin=dl.delivery.mp.microsoft.com`

    If successful, the Windows client device should begin to download a small image file from the Connected Cache node.

1. To check how much content an individual Windows client has downloaded from a Connected Cache node, open the [Delivery Optimization activity monitor](/microsoft-365-apps/updates/delivery-optimization#viewing-data-about-the-use-of-delivery-optimization) on the Windows client device.

    You should see a donut chart titled **Download Statistics**. If the Windows client has downloaded content from the cache node, you'll see a segment of the donut labeled **From Microsoft cache server**.

## Related content

- [Monitor cache node usage](mcc-ent-monitoring.md)
- [Troubleshoot cache node](mcc-ent-troubleshooting.md)
