---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
ms.service: windows-client
---

## Windows Subsystem for Linux (WSL)

With Windows Subsystem for Linux (WSL) you can run a Linux environment on a Windows device, without the need for a separate virtual machine or dual booting. WSL is designed to provide a seamless and productive experience for developers who want to use both Windows and Linux at the same time.

[!INCLUDE [new-24h2](new-24h2.md)]

- **Hyper-V Firewall** is a network firewall solution that enables filtering of inbound and outbound traffic to/from WSL containers hosted by Windows
- **DNS Tunneling** is a networking setting that improves compatibility in different networking environments, making use of virtualization features to obtain DNS information rather than a networking packet
- **Auto proxy** is a networking setting that enforces WSL to use Windows' HTTP proxy information. Turn on when using a proxy on Windows, as it makes that proxy automatically apply to WSL distributions

These features can be set up using a device management solution such as Microsoft Intune<sup>[\[7\]](../conclusion.md#footnote7)</sup>. Microsoft Defender for Endpoint (MDE) integrates with WSL, allowing it to monitor activities within a WSL distro and report them to the MDE dashboards.

[!INCLUDE [learn-more](learn-more.md)]

- [Hyper-V Firewall][LINK-1]
- [DNS Tunneling][LINK-2]
- [Auto proxy][LINK-3]
- [Intune setting for WSL][LINK-4]
- [Microsoft Defender for Endpoint plug-in for WSL][LINK-5]

<!--links-->

[LINK-1]: /windows/security/operating-system-security/network-security/windows-firewall/hyper-v-firewall
[LINK-2]: /windows/wsl/networking#dns-tunneling
[LINK-3]: /windows/wsl/networking#auto-proxy
[LINK-4]: /windows/wsl/intune
[LINK-5]: /defender-endpoint/mde-plugin-wsl
