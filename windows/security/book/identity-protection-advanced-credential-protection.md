---
title: Windows 11 security book - Advanced credential protection
description: Identity protection chapter - Advanced credential protection.
ms.topic: overview
ms.date: 11/18/2024
---

# Advanced credential protection

:::image type="content" source="images/identity-protection.png" alt-text="Diagram containing a list of security features." lightbox="images/identity-protection.png" border="false":::

In addition to adopting passwordless sign-in, organizations can strengthen security for user and domain credentials in Windows 11 with Credential Guard and Remote Credential Guard.

## Local Security Authority (LSA) protection

Windows has several critical processes to verify a user's identity. Verification processes include Local Security Authority (LSA), which is responsible for authenticating users, and verifying Windows sign-ins. LSA handles tokens and credentials that are used for single sign-on to a Microsoft account and Entra ID account.

By loading only trusted, signed code, LSA provides significant protection against credential theft. LSA protection supports configuration using group policy and other device management solutions.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

To help keep these credentials safe, LSA protection is enabled by default on all devices (MSA, Microsoft Entra joined, hybrid, and local). For new installs, it is enabled immediately. For upgrades, it is enabled after rebooting after an evaluation period of 10 days.

Users have the ability to manage the LSA protection state in the Windows Security application under **Device Security** > **Core Isolation** > **Local Security Authority protection**.

To ensure a seamless transition and enhanced security for all users, the enterprise policy for LSA protection takes precedence over enablement on upgrade.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Configuring additional LSA protection][LINK-2]

## Credential Guard

:::row:::
    :::column:::
        Credential Guard uses hardware-backed, Virtualization-based security (VBS) to protect against credential theft. With Credential Guard, the Local Security Authority (LSA) stores and protects Active Directory (AD) secrets in an isolated environment that isn't accessible to the rest of the operating system. LSA uses remote procedure calls to communicate with the isolated LSA process.

By protecting the LSA process with Virtualization-based security, Credential Guard shields systems from user credential theft attack techniques like Pass-the-Hash or Pass-the-Ticket. It also helps prevent malware from accessing system secrets even if the process is running with admin privileges.
    :::column-end:::
    :::column:::
:::image type="content" source="images/credential-guard-architecture.png" alt-text="Diagram of the Credential Guard's architecture."  lightbox="images/credential-guard-architecture.png" border="false":::
    :::column-end:::
:::row-end:::

[!INCLUDE [new-24h2](includes/new-24h2.md)]

Credential Guard protections are expanded to optionally include machine account passwords for Active Directory-joined devices. Administrators can enable audit mode or enforcement of this capability using Credential Guard policy settings.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Protect derived domain credentials with Credential Guard][LINK-3]

## Remote Credential Guard

Remote Credential Guard helps organizations protect credentials over a Remote Desktop connection by redirecting the Kerberos requests back to the device that is requesting the connection. It also provides single sign-on experiences for Remote Desktop sessions.

Administrator credentials are highly privileged and must be protected. When Remote Credential Guard is configured to connect during Remote Desktop sessions, the credential and credential derivatives are never passed over the network to the target device. If the target device is compromised, the credentials aren't exposed.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Remote Credential Guard][LINK-4]

## :::image type="icon" source="images/new-button-title.svg" border="false"::: VBS key protection

VBS key protection enables developers to secure cryptographic keys using Virtualization-based security (VBS). VBS uses the virtualization extension capability of the CPU to create an isolated runtime outside of the normal OS. When in use, VBS keys are isolated in a secure process, allowing key operations to occur without ever exposing the private key material outside of this space. At rest, private key material is encrypted by a TPM key, which binds VBS keys to the device. Keys protected in this way can't be dumped from process memory or exported in plain text from a user's machine, preventing exfiltration attacks by any admin-level attacker.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Advancing key protection in Windows using VBS][LINK-8]

## Token protection (preview)

Token protection attempts to reduce attacks using Microsoft Entra ID token theft. Token protection makes tokens usable only from their intended device by cryptographically binding a token with a device secret. When using the token, both the token and proof of the device secret must be provided. Conditional Access policies<sup>[\[4\]](conclusion.md#footnote4)</sup> can be configured to require token protection when using sign-in tokens for specific services.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Token protection in Entra ID Conditional Access][LINK-5]

### Sign-in session token protection policy

This feature allows applications and services to cryptographically bind security tokens to the device, restricting attackers' ability to impersonate users on a different device if tokens are stolen.

## Account lockout policies

New devices with Windows 11 installed will have account lockout policies that are secure by default. These policies mitigate brute-force attacks such as hackers attempting to access Windows devices via the Remote Desktop Protocol (RDP).

The account lockout threshold policy is now set to 10 failed sign-in attempts by default, with the account lockout duration set to 10 minutes. The *Allow Administrator account lockout* is now enabled by default. The Reset account lockout counter after is now set to 10 minutes by default as well.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Account lockout policy][LINK-6]

## Access management and control

Access control in Windows ensures that shared resources are available to users and groups other than the resource's owner and are protected from unauthorized use. IT administrators can manage the access of users, groups, and computers to objects and assets on a network or computer. After a user is authenticated, Windows implements the second phase of protecting resources with built-in authorization and access control technologies. These technologies determine if an authenticated user has the correct permissions.

Access Control Lists (ACLs) describe the permissions for a specific object and can also contain System Access Control Lists (SACLs). SACLs provide a way to audit specific system level events, such as when a user attempts to access file system objects. These events are essential for tracking activity for objects that are sensitive or valuable and require extra monitoring. Being able to audit when a resource attempts to read or write part of the operating system is critical to understanding a potential attack.

IT administrators can refine the application and management of access to:

- Protect a greater number and variety of network resources from misuse
- Provision users to access resources in a manner that is consistent with organizational policies and the requirements of their jobs. Organizations can implement the principle of least-privilege access, which asserts that users should be granted access only to the data and operations they require to perform their jobs
- Update users' ability to access resources regularly, as an organization's policies change or as users' jobs change
- Support evolving workplace needs, including access from hybrid or remote locations, or from a rapidly expanding array of devices, including tablets and phones
- Identify and resolve access issues when legitimate users are unable to access resources that they need to perform their jobs

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Access control][LINK-7]

<!--links-->

[LINK-2]: /windows-server/security/credentials-protection-and-management/configuring-additional-lsa-protection
[LINK-3]: /windows/security/identity-protection/credential-guard
[LINK-4]: /windows/security/identity-protection/remote-credential-guard
[LINK-5]: /azure/active-directory/conditional-access/concept-token-protection
[LINK-6]: /windows/security/threat-protection/security-policy-settings/account-lockout-policy
[LINK-7]: /windows/security/identity-protection/access-control/access-control
[LINK-8]: https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-key-protection-in-windows-using-vbs/4050988