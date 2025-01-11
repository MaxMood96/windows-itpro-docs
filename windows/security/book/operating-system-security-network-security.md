---
title: Windows 11 security book - Network security
description: Operating System security chapter - Network security.
ms.topic: overview
ms.date: 11/18/2024
---

# Network security

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

Windows 11 raises the bar for network security, offering comprehensive protection to help people work with confidence from almost anywhere. To help reduce an organization's attack
surface, network protection in Windows prevents people from accessing dangerous IP addresses and domains that may host phishing scams, exploits, and other malicious content.
Using reputation-based services, network protection blocks access to potentially harmful, low-reputation domains and IP addresses.

New DNS and TLS protocol versions strengthen the end-to-end protections needed for applications, web services, and Zero Trust networking. File access adds an untrusted network scenario with Server Message Block over QUIC, and new encryption and signing capabilities. Wi-Fi and Bluetooth advancements also provide greater trust in connections to other devices. In addition, VPN and Windows Firewall platforms offer new ways to easily configure and debug software.

In enterprise environments, network protection works best with Microsoft Defender for Endpoint, which provides detailed reporting on protection events as part of larger investigation scenarios.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [How to protect your network][LINK-1]

## Transport Layer Security (TLS)

Transport Layer Security (TLS) is a popular security protocol, encrypting data in transit to help provide a more secure communication channel between two endpoints. Windows enables the latest protocol versions and strong cipher suites by default and offers a full suite of extensions such as client authentication for enhanced server security, or session resumption for improved application performance. TLS 1.3 is the latest version of the protocol and is enabled by default in Windows. This version helps to eliminate obsolete cryptographic algorithms, enhance security over older versions, and aim to encrypt as much of the TLS handshake as possible. The handshake is more performant with one less round trip per connection on average and supports only strong cipher suites which provide perfect forward secrecy and less operational risk. Using TLS 1.3 provides more privacy and lower latencies for encrypted online connections. If the client or server application on either side of the connection doesn't support TLS 1.3, the connection falls back to TLS 1.2. Windows uses the latest Datagram Transport Layer Security (DTLS) 1.2 for UDP communications.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [TLS/SSL overview (Schannel SSP)][LINK-2]
- [TLS 1.0 and TLS 1.1 soon to be disabled in Windows][LINK-3]

## Domain Name System (DNS) security

In Windows 11, the Windows DNS client supports DNS over HTTPS and DNS over TLS, two encrypted DNS protocols. These allow administrators to ensure their devices protect their
name queries from on-path attackers, whether they're passive observers logging browsing behavior or active attackers trying to redirect clients to malicious sites. In a Zero Trust
model where no trust is placed in a network boundary, having a secure connection to a trusted name resolver is required.

Windows 11 provides group policy and programmatic controls to configure DNS over HTTPS behavior. As a result, IT administrators can extend existing security to adopt new models such as Zero Trust. IT administrators can mandate DNS over HTTPS protocol, ensuring that devices that use insecure DNS will fail to connect to network resources. IT administrators also have the option not to use DNS over HTTPS or DNS over TLS for legacy deployments where network edge appliances are trusted to inspect plain-text DNS traffic. By default, Windows 11 will defer to the local administrator on which resolvers should use encrypted DNS.

Support for DNS encryption integrates with existing Windows DNS configurations such as the Name Resolution Policy Table (NRPT), the system Hosts file, and resolvers specified per network adapter or network profile. The integration helps Windows 11 ensure that the benefits of greater DNS security do not regress existing DNS control mechanisms.

## Bluetooth protection

The number of Bluetooth devices connected to Windows 11 continues to increase. Windows users connect their Bluetooth headsets, mice, keyboards, and other accessories and improve their day-to-day PC experience by enjoying streaming, productivity, and gaming. Windows supports all standard Bluetooth pairing protocols, including classic and LE Secure connections, secure simple pairing, and classic and LE legacy pairing. Windows also implements host-based LE privacy. Windows updates help users stay current with OS and driver security features in accordance with the Bluetooth Special Interest Group (SIG) and Standard Vulnerability Reports, as well as issues beyond those required by the Bluetooth core industry standards. Microsoft strongly recommends that Bluetooth accessories' firmware and software are kept up to date.

IT-managed environments have a number policy settings available via configuration service providers, group policy, and PowerShell. These settings can be managed through device management solutions like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>. You can configure Windows to use Bluetooth technology while supporting the security needs of your organization. For example, you can allow input and audio while blocking file transfer, force encryption standards, limit Windows discoverability, or even disable Bluetooth entirely for the most sensitive environments.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Policy CSP - Bluetooth][LINK-4]

## Wi-Fi connections

Windows Wi-Fi supports industry-standard authentication and encryption methods when connecting to Wi-Fi networks. WPA (Wi-Fi Protected Access) is a security standard defined by the Wi-Fi Alliance (WFA) to provide sophisticated data encryption and better user authentication.

The current security standard for Wi-Fi authentication is WPA3, which provides a more secure and reliable connection method as compared to WPA2 and older security protocols. Windows supports three WPA3 modes - WPA3 Personal, WPA3 Enterprise, and WPA3 Enterprise 192-bit Suite B.

Windows 11 includes WPA3 Personal with the new H2E protocol and WPA3 Enterprise 192-bit Suite B. Windows 11 also supports WPA3 Enterprise, which includes enhanced server certificate validation and TLS 1.3 for authentication using EAP-TLS authentication.

Opportunistic Wireless Encryption (OWE), a technology that allows wireless devices to establish encrypted connections to public Wi-Fi hotspots, is also included.

## 5G and eSIM

5G networks use stronger encryption and better network segmentation compared to previous generations of cellular protocols. Unlike Wi-Fi, 5G access is always mutually authenticated. Access credentials are stored in an EAL4-certified eSIM that is physically embedded in the device, making it much harder for attackers to tamper with. Together, 5G and eSIM provide a strong foundation for security.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [eSIM configuration of a download server][LINK-5]

## Windows Firewall

Windows Firewall is an important part of a layered security model. It provides host-based, two-way network traffic
filtering, blocking unauthorized traffic flowing into or out of the local device based on the types of networks the device is connected to.

Windows Firewall offers the following benefits:

- Reduces the risk of network security threats: Windows Firewall reduces the attack surface of a device with rules that restrict or allow traffic by many properties, such as IP addresses, ports, or program paths. This functionality increases manageability and decreases the likelihood of a successful attack
- Safeguards sensitive data and intellectual property: By integrating with Internet Protocol Security (IPSec), Windows Firewall provides a simple way to enforce authenticated, end-to-end network communications. It provides scalable, tiered access to trusted network resources, helping to enforce integrity of the data, and optionally helping to protect the confidentiality of the data
- Extends the value of existing investments: Because Windows Firewall is a host-based firewall that is included with the operating system, there's no extra hardware or software required. Windows Firewall is also designed to complement existing non-Microsoft network security solutions through a documented application programming interface (API)

Windows 11 makes the Windows Firewall easier to analyze and debug. IPSec behavior is integrated with Packet Monitor, an in-box, cross-component network diagnostic tool for Windows. Additionally, the Windows Firewall event logs are enhanced to ensure an audit can identify the specific filter that was responsible for any given event. This enables analysis of firewall behavior and rich packet capture without relying on third-party tools.

Admins can configure more settings through the Firewall and Firewall Rule policy templates in the Endpoint Security node in Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, using the platform support from the Firewall configuration service provider (CSP) and applying these settings to Windows endpoints.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

The Firewall Configuration Service Provider (CSP) in Windows now enforces an all-or-nothing approach to applying firewall rules within each atomic block. Previously, if the CSP encountered an issue with any rule in a block, it would not only stop processing that rule but also cease processing subsequent rules, potentially leaving a security gap with partially deployed rule blocks. Now, if any rule in the block cannot be successfully applied, the CSP stops processing subsequent rules and roll back all rules from that atomic block, eliminating the ambiguity of partially deployed rule blocks.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Firewall overview][LINK-6]
- [Firewall CSP][LINK-7]

## Virtual private networks (VPN)

Organizations have long relied on Windows to provide reliable, secured, and manageable virtual private network (VPN) solutions. The Windows VPN client platform includes built-in VPN
protocols, configuration support, a common VPN user interface, and programming support for custom VPN protocols. VPN apps are available in the Microsoft Store for both enterprise and
consumer VPNs, including apps for the most popular enterprise VPN gateways.

In Windows 11, we've integrated the most commonly used VPN controls right into the Windows 11 Quick Actions pane. From the Quick Actions pane, users can verify the status of their VPN, start and stop the connection, and easily open Settings for more controls.

The Windows VPN platform connects to Microsoft Entra ID<sup>[\[4\]](conclusion.md#footnote4)</sup> and Conditional Access for single sign-on, including multifactor authentication (MFA) through Microsoft Entra ID. The VPN platform also supports classic domain-joined authentication. It's supported by Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup> and other device management solutions. The flexible VPN profile supports both built-in protocols and custom protocols. It can configure multiple authentication methods and can be automatically started as needed or manually started by the end user. It also supports split-tunnel VPN and exclusive VPN with exceptions for trusted external sites.

With Universal Windows Platform (UWP) VPN apps, end users never get stuck on an old version of their VPN client. VPN apps from the store will be automatically updated as needed. Naturally, the updates are in the control of your IT admins.

The Windows VPN platform is tuned and hardened for cloud-based VPN providers like Azure VPN. Features like Microsoft Entra ID authentication, Windows user interface integration, plumbing IKE traffic selectors, and server support are all built into the Windows VPN platform. The integration into the Windows VPN platform leads to a simpler IT admin experience. User authentication is more consistent, and users can easily find and control their VPN.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows VPN technical guide][LINK-8]

## Server Message Block file services

Server Message Block (SMB) and file services are the most common Windows workloads in the commercial and public sector ecosystem. Users and applications rely on SMB to access the files that run organizations of all sizes.

Windows 11 introduced significant security updates to meet today's threats, including AES-256 SMB encryption, accelerated SMB signing, Remote Directory Memory Access (RDMA) network encryption, and SMB over QUIC for untrusted networks.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

New security options include mandatory SMB signing by default, NTLM blocking, authentication rate limiting, and several other enhancements.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Server Message Block (SMB) protocol changes in Windows 11, version 24H2][LINK-9]
- [File sharing using the SMB 3 protocol][LINK-10]

<!--links-->

[LINK-1]: /defender-endpoint/network-protection
[LINK-2]: /windows-server/security/tls/tls-ssl-schannel-ssp-overview
[LINK-3]: https://techcommunity.microsoft.com/blog/windows-itpro-blog/tls-1-0-and-tls-1-1-soon-to-be-disabled-in-windows/3887947
[LINK-4]: /windows/client-management/mdm/policy-csp-bluetooth
[LINK-5]: /mem/intune/configuration/esim-device-configuration-download-server
[LINK-6]: /windows/security/operating-system-security/network-security/windows-firewall
[LINK-7]: /windows/client-management/mdm/firewall-csp
[LINK-8]: /windows/security/operating-system-security/network-security/vpn/vpn-guide
[LINK-9]: /windows/whats-new/whats-new-windows-11-version-24h2#server-message-block-smb-protocol-changes
[LINK-10]: /windows-server/storage/file-server/file-server-smb-overview