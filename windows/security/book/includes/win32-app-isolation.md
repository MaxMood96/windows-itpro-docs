---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
ms.service: windows-client
---

## :::image type="icon" source="../images/new-button-title.svg" border="false"::: Win32 app isolation

Win32 app isolation is a security feature designed to be the default isolation standard on Windows clients. It's built on [AppContainer][LINK-1], and offers several added security features to help the Windows platform defend against attacks that use vulnerabilities in applications or third-party libraries. To isolate their applications, developers can update them using Visual Studio.

Win32 app isolation follows a two-step process:

- In the first step, the Win32 application is launched as a low-integrity process using AppContainer, which is recognized as a security boundary by Windows. The process is limited to a specific set of Windows APIs by default and is unable to inject code into any process operating at a higher integrity level
- In the second step, least privilege is enforced by granting authorized access to Windows securable objects. This access is determined by capabilities that are added to the application manifest through MSIX packaging. *Securable objects* in this context refers to Windows resources whose access is safeguarded by capabilities. These capabilities enable the implantation of a [Discretionary Access Control List][LINK-2] on Windows

To help ensuring that isolated applications run smoothly, developers must define the access requirements for the application via access capability declarations in the application package manifest. The *Application Capability Profiler (ACP)* simplifies the entire process by allowing the application to run in *learn mode* with low privileges. Instead of denying access if the capability isn't present, ACP allows access and logs additional capabilities required for access if the application were to run isolated.

To create a smooth user experience that aligns with nonisolated, native Win32 applications, two key factors should be taken into consideration:

- Approaches for accessing data and privacy information
- Integrating Win32 apps for compatibility with other Windows interfaces

The first factor relates to implementing methods to manage access to files and privacy information within and outside the isolation boundary AppContainer. The second factor involves integrating Win32 apps with other Windows interfaces in a way that helps enable seamless functionality without causing perplexing user consent prompts.

[!INCLUDE [learn-more](learn-more.md)]

- [Win32 app isolation overview][LINK-4]
- [Application Capability Profiler (ACP)][LINK-5]
- [Packaging a Win32 app isolation application with Visual Studio][LINK-6]
- [Sandboxing Python with Win32 app isolation][LINK-7]

<!--links-->

[LINK-1]: /windows/win32/secauthz/implementing-an-appcontainer
[LINK-2]: /windows/win32/secauthz/access-control-lists
[LINK-4]: /windows/win32/secauthz/app-isolation-overview
[LINK-5]: /windows/win32/secauthz/app-isolation-capability-profiler
[LINK-6]: /windows/win32/secauthz/app-isolation-packaging-with-vs
[LINK-7]: https://blogs.windows.com/windowsdeveloper/2024/03/06/sandboxing-python-with-win32-app-isolation/
