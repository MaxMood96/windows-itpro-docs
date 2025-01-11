---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
ms.service: windows-client
---

## App Control for Business

Your organization is only as secure as the applications that run on your devices. With *application control*, apps must earn trust to run, in contrast to an application trust model where all code is assumed trustworthy. By helping prevent unwanted or malicious code from running, application control is an important part of an effective security strategy. Many organizations cite application control as one of the most effective means of defending against executable file-based malware.

App Control for Business (previously called *Windows Defender Application Control*) and AppLocker are both included in Windows. App Control for Business is the next-generation app control solution for Windows and provides powerful control over what runs in your environment. Organizations that were using AppLocker on previous versions of Windows, can continue to use the feature as they consider whether to switch to App Control for Business for stronger protection.

Microsoft Intune<sup>[\[4\]](..\conclusion.md#footnote4)</sup> can configure App Control for Business in the admin console, including setting up Intune as a managed installer. Intune includes built-in options for App Control for Business and the possibility to upload policies as an XML file for Intune to package and deploy.

[!INCLUDE [learn-more](learn-more.md)]

- [Application Control for Windows](/windows/security/application-security/application-control/windows-defender-application-control/wdac)
- [Automatically allow apps deployed by a managed installer with App Control for Business](/windows/security/application-security/application-control/app-control-for-business/design/configure-authorized-apps-deployed-with-a-managed-installer)
