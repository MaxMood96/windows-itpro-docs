---
title: Required service data for Windows 
description: Learn about required service data for Windows, including how to manage it and how it's used.
ms.service: windows-client
ms.subservice: itpro-privacy
ms.localizationpriority: high
author: DHB-MSFT
ms.author: danbrown
manager: dansimp
ms.date: 07/29/2025
ms.topic: concept-article
hideEdit: true
ms.collection: 
- privacy-windows
- must-keep
- trust-pod
---

# Required service data for Windows

**Applies to**

- Windows 11, version 21H2 and later
- Windows 10, version 1903 and later

Windows collects and processes personal data to deliver cloud-service-backed features of Windows known as [connected experiences](essential-services-and-connected-experiences.md). The data collected includes Windows required service data—data that is necessary to operate the service and deliver the expected connected experience. Windows must send required service data to the associated cloud service so that the feature can function. A connected experience may also collect Windows diagnostic data to keep the feature secure, up to date, and performing as expected, and the collection of such data is subject to the [Windows diagnostic data consent](configure-windows-diagnostic-data-in-your-organization.md).  

## Types of Windows connected experiences  

Windows required service data is collected and sent to Microsoft for essential services. [Essential services](essential-services-and-connected-experiences.md#windows-essential-services) are either integral to how Windows works or are used to keep Windows secure, up to date, performing as expected. For example, the licensing service uses Windows required service data to confirm that you’re properly licensed to use Windows.  

Windows required service data is also collected and sent to Microsoft for optional connected experiences.

The connected experiences you choose to use in Windows will determine what additional Windows required service data is sent to Microsoft. For example, if you choose to use a connected experience or provide consent to sync your data with your Microsoft account such as Find My Device and Windows backup, Windows required service data is sent and processed to provide you with the ability to locate or restore your device when needed. Windows required service data can also include information needed by a connected experience to perform its task, such as configuration information about Windows. Most Windows required service data is considered ephemeral and is discarded immediately after use, typically within 48 hours. For more information, refer to the [How Windows required service data is used](#how-windows-required-service-data-is-used) section later in this article. In some cases, you may consent for Windows required service data collected through optional connected experiences to be promoted to [Account Data](https://support.microsoft.com/topic/7efd7da0-9683-45f3-9e32-9e9dc90b8ebb). This allows you to sync the data across devices or Microsoft apps, enhancing continuity and usability.

## Manage Windows required service data  

For optional connected experiences, such as Find My Device, you can choose to turn off the experience. When turned off, it means no Windows required service data is sent back to Microsoft for that feature.  

For essential services, administrators have controls to turn some of them off. For more information, see [Manage connections from Windows 10 and Windows 11 operating system components to Microsoft services](manage-connections-from-windows-operating-system-components-to-microsoft-services.md).  

The connected experiences that you enable and use will influence the volume of data sent from your device.  

Microsoft is committed to maintaining your rights to access your customer data. For more information on accessing and porting your Windows required service data promoted to Account Data, refer to the [Microsoft Privacy Statement](https://www.microsoft.com/privacy/privacystatement#mainhowtoaccesscontrolyourdatamodule). To help maintain the security, integrity, and resiliency of Windows and protect customer data, certain types of information may not be eligible for export. This includes data related to the design or operation of the Windows cloud infrastructure, particularly where such information relates to cybersecurity practices or detection capabilities. These limitations are intended to support a secure and trusted environment for all Windows customers.  

Windows required service data is separate from required or optional Windows diagnostic data, which relates to information about your Windows device. Therefore, the privacy settings you choose for Windows required or optional diagnostic data don't affect whether Windows required service data is sent to Microsoft.

## How Windows required service data is used  

Windows uses required service data for operating the service and for delivering the expected connected experience. Once the service is provided, it's discarded. Because of this, Windows required service data is considered ephemeral and is typically discarded within 48 hours of use.  

Windows does not:  

- Combine personal data from Windows required service data with other types of data without consent, including Windows diagnostic data and personal data from other services.  

- Combine Windows data with [Account Data](https://support.microsoft.com/topic/7efd7da0-9683-45f3-9e32-9e9dc90b8ebb) from other products and services unless the service seeks consent to do so before promoting the Windows required service data to Account Data.  

Microsoft may also de-identify or aggregate the Windows required service data and process the resulting data to improve the quality of a connected experience. This resulting data is no longer personal data because it's neither linked nor linkable to an individual user.