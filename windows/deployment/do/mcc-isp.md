---
title: Microsoft Connected Cache for ISPs
description: This article contains details about the early preview for Microsoft Connected Cache for Internet Service Providers (ISPs).
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.author: carmenf
author: cmknox
ms.reviewer: mstewart
manager: aaroncz
ms.localizationpriority: medium
ms.collection: tier3
ms.date: 10/30/2024
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
- ✅ Microsoft Connected Cache for ISPs (early preview)
---

# Microsoft Connected Cache for Internet Service Providers (early preview)

> [!IMPORTANT]
> Microsoft Connected Cache for ISPs is now in Public Preview - for our early preview customers, the early preview version is no longer supported. We highly encourage you to onboard onto our Public Preview program. For instructions on signing up and onboarding, visit [Operator sign up and service onboarding for Microsoft Connected Cache](mcc-isp-signup.md).

## Overview

Microsoft Connected Cache preview is a software-only caching solution that delivers Microsoft content within operator networks. Connected Cache can be deployed to as many physical servers or VMs as needed and is managed from a cloud portal. Microsoft cloud services handle routing of consumer devices to the cache server for content downloads. For more information, visit [Microsoft Connected Cache for ISP](mcc-isp-overview.md).


Microsoft Connected Cache for Internet Service Providers is now in Public Preview! To get started, visit  [Azure portal](https://www.portal.azure.com) to sign up for Microsoft Connected Cache for Internet Service Providers. Please see [Operator sign up and service onboarding for Microsoft Connected Cache](mcc-isp-signup.md) for more information on the requirements for sign up and onboarding.





<!-- 

### Setting up a VM on Windows Server

You can use hardware that will natively run Ubuntu 20.04 LTS, or you can run an Ubuntu VM. The following steps describe how to set up a VM on Hyper-V.

1. Download the ISO. You can use either Ubuntu Desktop or Ubuntu Server.

    - [Download Ubuntu Desktop](https://ubuntu.com/download/desktop)
    - [Download Ubuntu Server](https://ubuntu.com/download/server)

1. Start the **New Virtual Machine Wizard** in Hyper-V.

    :::image type="content" source="./images/mcc-isp-hyper-v-begin.png" alt-text="Screenshot of the Before You Begin page of the Hyper-V New Virtual Machine Wizard.":::

1. Specify a name and choose a location.

    :::image type="content" source="./images/mcc-isp-hyper-v-name.png" alt-text="Screenshot of the Specify Name and Location page in the Hyper-V New Virtual Machine Wizard.":::

1. Select **Generation 2**. You can't change this setting later.

    :::image type="content" source="./images/mcc-isp-hyper-v-generation.png" alt-text="Screenshot of the Specify Generation page in the Hyper-V New Virtual Machine Wizard.":::

1. Specify the startup memory.

    :::image type="content" source="./images/mcc-isp-hyper-v-memory.png" alt-text="Screenshot of the Assign Memory page of the Hyper-V New Virtual Machine Wizard.":::

1. Choose the network adapter connection.

    :::image type="content" source="./images/mcc-isp-hyper-v-networking.png" alt-text="Screenshot of the Configure Networking page of the Hyper-V New Virtual Machine Wizard.":::

1. Set the virtual hard disk parameters. You should specify enough space for the OS and the content that will be cached. For example, `1024` GB is 1 terabyte.

    :::image type="content" source="./images/mcc-isp-hyper-v-disk.png" alt-text="Screenshot of the Connect Virtual Hard Disk page of the Hyper-V New Virtual Machine Wizard.":::

1. Select **Install an OS from a bootable image file** and browse to the ISO for Ubuntu 20.04 LTS that you previously downloaded.

    :::image type="content" source="./images/mcc-isp-hyper-v-installation-options.png" alt-text="Screenshot of the Installation Options page of the Hyper-V New Virtual Machine Wizard.":::

1. Review the settings and select **Finish** to create the Ubuntu VM.

    :::image type="content" source="./images/mcc-isp-hyper-v-summary.png" alt-text="Screenshot of completing the New Virtual Machine Wizard on Hyper-V.":::

1. Before you start the Ubuntu VM, disable **Secure Boot** and allocate multiple cores to the VM.

    1. In Hyper-V Manager, open the **Settings** for the VM.

        :::image type="content" source="./images/mcc-isp-hyper-v-vm-settings.png" alt-text="Screenshot of the settings for a VM in Hyper-V Manager.":::

    1. Select **Security**. Disable the option to **Enable Secure Boot**.

        :::image type="content" source="./images/mcc-isp-hyper-v-vm-security.png" alt-text="Screenshot of the security page from VM settings in Hyper-V Manager.":::

    1. Select **Processor**. Increase the number of virtual processors. This example shows `12`, but your configuration may vary.

        :::image type="content" source="./images/mcc-isp-hyper-v-vm-processor.png" alt-text="Screenshot of the processor page from VM settings in Hyper-V Manager.":::

1. Start the VM and select **Install Ubuntu**.

    :::image type="content" source="./images/mcc-isp-gnu-grub.png" alt-text="Screenshot of the GNU GRUB screen, with Install Ubuntu selected.":::

1. Choose your default language.

    :::image type="content" source="./images/mcc-isp-ubuntu-language.png" alt-text="Screenshot of the Ubuntu install's language selection page.":::

1. Choose the options for installing updates and third party hardware. For example, download updates and install third party software drivers.

1. Select **Erase disk and install Ubuntu**. If you had a previous version of Ubuntu installed, we recommend erasing and installing Ubuntu 16.04.

    :::image type="content" source="./images/mcc-isp-ubuntu-erase-disk.png" alt-text="Screenshot of the Ubuntu install Installation type page with the Erase disk and install Ubuntu option selected.":::

    Review the warning about writing changes to disk, and select **Continue**.

    :::image type="content" source="./images/mcc-isp-ubuntu-write-changes.png" alt-text="Screenshot of the Ubuntu install's 'Write the changes to disks' warning.":::

1. Choose the time zone.

    :::image type="content" source="./images/mcc-isp-ubuntu-time-zone.png" alt-text="Screenshot of the Ubuntu install's 'Where are you page' to specify time zone.":::

1. Choose the keyboard layout.

    :::image type="content" source="./images/mcc-isp-ubuntu-keyboard.png" alt-text="Screenshot of the Ubuntu install's Keyboard layout page.":::

1. Specify your name, a name for the computer, a username, and a strong password. Select the option to **Require my password to log in**.

    > [!TIP]
    > Everything is case sensitive in Linux.

    :::image type="content" source="./images/mcc-isp-ubuntu-who.png" alt-text="Screenshot of the Ubuntu install's, 'Who are you' screen.":::

1. To complete the installation, select **Restart now**.

    :::image type="content" source="./images/mcc-isp-ubuntu-restart.png" alt-text="Screenshot of the Ubuntu install's installation complete, restart now screen.":::

1. After the computer restarts, sign in with the username and password.

    > [!IMPORTANT]
    > If it shows that an upgrade is available, select **Don't upgrade**.
    >
    > :::image type="content" source="./images/mcc-isp-ubuntu-upgrade.png" alt-text="Screenshot of the Ubuntu install's Upgrade Available prompt with Don't Upgrade selected.":::

Your Ubuntu VM is now ready to install Connected Cache.

### IoT Edge runtime

The Azure IoT Edge runtime enables custom and cloud logic on IoT Edge devices. The runtime sits on the IoT Edge device, and does management and communication operations. The runtime does the following functions:

- Installs and updates workloads (Docker containers) on the device.
- Maintains Azure IoT Edge security standards on the device.
- Makes sure that IoT Edge modules (Docker containers) are always running.
- Reports module (Docker containers) health to the cloud for remote monitoring.
- Manages communication between an IoT Edge device and the cloud.

For more information on Azure IoT Edge, see the [Azure IoT Edge documentation](/azure/iot-edge/about-iot-edge).

## Related articles

[Microsoft Connected Cache overview](waas-microsoft-connected-cache.md)

[Introducing Microsoft Connected Cache](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/introducing-microsoft-connected-cache-microsoft-s-cloud-managed/ba-p/963898)

-->
