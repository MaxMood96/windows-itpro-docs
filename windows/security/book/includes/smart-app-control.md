---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
ms.service: windows-client
---

## Smart App Control

Smart App Control prevents users from running malicious applications by blocking untrusted or unsigned applications. Smart App Control goes beyond previous built-in browser protections by adding another layer of security that is woven directly into the core of the OS at the process level. Using AI, Smart App Control only allows processes to run if they're predicted to be safe based on existing and new intelligence updated daily.

Smart App Control builds on top of the same cloud-based AI used in *App Control for Business* to predict the safety of an application, so that users can be confident that their applications are safe and reliable. Additionally, Smart App Control blocks unknown script files and macros from the web, greatly improving security for everyday users.

We've been making significant improvements to Smart App Control to increase the security, usability, and cloud intelligence response for apps in the Windows ecosystem. Users can get the latest and best experience with Smart App Control by keeping their devices up to date via Windows Update every month.

To ensure that users have a seamless experience with Smart App Control enabled, we ask developers to sign their applications with a code signing certificate from the Microsoft Trusted Root Program. Developers should include all binaries, such as exe, dll, temp installer files, and uninstallers. Trusted Signing makes the process of obtaining, maintaining, and signing with a trusted certificate simple and secure.

Smart App Control is disabled on devices enrolled in enterprise management. We suggest enterprises running line-of-business applications continue to use *App Control for Business*.

[!INCLUDE [learn-more](learn-more.md)]

- [Smart App Control](/windows/apps/develop/smart-app-control/overview)