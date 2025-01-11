---
title: Microsoft Connected Cache for Enterprise and Education prerequisites
description: Details of prerequisites and recommendations for using Microsoft Connected Cache for Enterprise and Education.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: conceptual
ms.author: lichris
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>
ms.date: 10/30/2024
---

# Microsoft Connected Cache for Enterprise and Education Requirements

This article details the requirements and recommended specifications for using Microsoft Connected Cache for Enterprise and Education.

## Licensing requirements

- **Valid Azure subscription**: To use the Microsoft Connected Cache for Enterprise and Education service, you'll need a valid Azure subscription that can be used to provision the necessary [Azure resources](/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management).

    If you don't have an Azure subscription already, you can create an Azure [pay-as-you-go](https://azure.microsoft.com/offers/ms-azr-0003p/) account, which requires a credit card for verification purposes. For more information, see the [Azure Free Account FAQ](https://azure.microsoft.com/free/free-account-faq/).

    The Azure resources used for Connected Cache will be free to you during this public preview.

- **E3/E5 or A3/A5 license**: Your organization must have one of the following license subscriptions for each device that downloads content from a Connected Cache node:

    - [Windows Enterprise E3 or E5](/windows/whats-new/windows-licensing#windows-11-enterprise), included in [Microsoft 365 F3, E3, or E5](https://www.microsoft.com/microsoft-365/enterprise/microsoft365-plans-and-pricing?msockid=32c407b43d5968050f2b13443c746916)
    - Windows Education A3 or A5, included in [Microsoft 365 A3 or A5](https://www.microsoft.com/education/products/microsoft-365?msockid=32c407b43d5968050f2b13443c746916#Education-plans)

## Cache node host machine requirements

### General requirements

- Any previous installations of Connected Cache must be [uninstalled](mcc-ent-uninstall-cache-node.md) from the host machine before installing the latest version of Connected Cache.
- [These listed endpoints](delivery-optimization-endpoints.md) must be reachable by the host machine.
- The host machine must have no other services / applications utilizing port 80 (for example, Configuration Manager or a distribution point).
- The host machine must have at least 4 GB of free memory.

### Additional requirements for Windows host machines

- The Windows host machine must be using Windows 11 or Windows Server 2022 with the latest cumulative update applied.
    - Windows 11 must have [OS Build 22631.3296](https://support.microsoft.com/topic/march-12-2024-kb5035853-os-builds-22621-3296-and-22631-3296-a69ac07f-e893-4d16-bbe1-554b7d9dd39b) or later
    - Windows Server 2022 must have [OS Build 20348.2227](https://support.microsoft.com/topic/january-9-2024-kb5034129-os-build-20348-2227-6958a36f-efaf-4ef5-a576-c5931072a89a) or later
- The Windows host machine must support nested virtualization. Ensure that any security settings that may restrict nested virtualization are not enabled, such as ["Trusted launch" in Azure VMs](/azure/virtual-machines/trusted-launch-portal).
- The Windows host machine must have [WSL 2 installed](/windows/wsl/install#install-wsl-command). You can install this on Windows 11 and Windows Server 2022 by logging on as a local administrator and running the PowerShell command `wsl.exe --install --no-distribution` in an elevated PowerShell window.

### Additional requirements for Linux host machines

- The Linux host machine must be using one of the following operating systems:
    - Ubuntu 22.04
    - Red Hat Enterprise Linux (RHEL) 8.* or 9.*
        - If using RHEL, the default container engine (Podman) must be replaced with [Moby](https://github.com/moby/moby#readme)

### Recommended host machine networking specifications

- Multiple network interface cards (NICs) on a single Connected Cache host machine isn't supported.
- 1 Gbps NIC is the minimum speed recommended but any NIC is supported.
- The NIC and BIOS should support SR-IOV for best performance.

### Recommended host machine hardware specifications

Based on your [enterprise configuration](mcc-ent-edu-overview.md), it's recommended to deploy your Connected Cache nodes to host machines that meet the following recommended hardware specifications:

| Component | Branch office | Small / medium enterprise | Large enterprise |
| --- | --- | --- | --- |
| CPU cores | 4 | 8 | 16 |
| Memory | 8 GB, 4 GB free | 16 GB, 4 GB free | 32 GB, 4 GB free |
| Disk storage | 100 GB free  | 500 GB free | 2x 200-500 GB free |
| NIC | 1 Gbps | 5 Gbps | 10 Gbps |
