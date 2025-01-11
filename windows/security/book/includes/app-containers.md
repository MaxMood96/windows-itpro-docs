---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
ms.service: windows-client
---

## App containers

In addition to Windows Sandbox for Win32 apps, Universal Windows Platform (UWP) applications run in Windows containers known as *app containers*. App containers act as process and resource isolation boundaries, but unlike Docker containers, these are special containers designed to run Windows applications.

Processes that run in app containers operate at a low integrity level, meaning they have limited access to resources they don't own. Because the default integrity level of most resources is medium integrity level, the UWP app can access only a subset of the file system, registry, and other resources. The app container also enforces restrictions on network connectivity. For example, access to a local host isn't allowed. As a result, malware or infected apps have limited footprint for escape.

[!INCLUDE [learn-more](learn-more.md)]

- [Windows and app container](/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/feature-mapping-table?source=recommendations)
