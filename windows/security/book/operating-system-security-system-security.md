---
title: Windows 11 security book - System security
description: Operating System security chapter - System security.
ms.topic: overview
ms.date: 11/18/2024
---

# System security

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

## Trusted Boot (Secure Boot + Measured Boot)

Windows 11 requires all PCs to use Unified Extensible Firmware Interface (UEFI)'s Secure Boot feature. When a Windows 11 device starts, Secure Boot and Trusted Boot work together to prevent malware and corrupted components from loading. Secure Boot provides initial protection, then Trusted Boot picks up the process.

Secure Boot makes a safe and trusted path from the Unified Extensible Firmware Interface (UEFI) through the Windows kernel's Trusted Boot sequence. Malware attacks on the Windows boot sequence are blocked by the signature-enforcement handshakes throughout the boot sequence between the UEFI, bootloader, kernel, and application environments.

To mitigate the risk of firmware rootkits, the PC verifies the digital signature of the firmware at the start of the boot process. Secure Boot then checks the digital signature of the OS bootloader and all code that runs before the operating system starts, ensuring that the signature and code are uncompromised and trusted according to the Secure Boot policy.

Trusted Boot picks up the process that begins with Secure Boot. The Windows bootloader verifies the digital signature of the Windows kernel before loading it. The Windows kernel, in turn, verifies every other component of the Windows startup process, including boot drivers, startup files, and any anti-malware product's early-launch anti-malware (ELAM) driver. If any of these files have been tampered with, the bootloader detects the problem and refuses to load the corrupted component. Often, Windows can automatically repair the corrupted component, restoring the integrity of Windows and allowing the PC to start normally.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Secure the Windows boot process][LINK-1]
- [Secure Boot and Trusted Boot][LINK-2]

## Cryptography

Cryptography is designed to protect user and system data. The cryptography stack in Windows 11 extends from the chip to the cloud, enabling Windows, applications, and services to protect system and user secrets. For example, data can be encrypted so that only a specific reader with a unique key can read it. As a basis for data security, cryptography helps prevent anyone except the intended recipient from reading data, performs integrity checks to ensure data is free of tampering, and authenticates identity to ensure that communication is secure. Windows 11 cryptography is certified to meet the Federal Information Processing Standard (FIPS) 140. FIPS 140 certification ensures that US government-approved algorithms are correctly implemented.

[!INCLUDE [learn-more](includes/learn-more.md)]

- FIPS 140 validation

Windows cryptographic modules provide low-level primitives such as:

- Random number generators (RNG)
- Support for AES 128/256 with XTS, ECB, CBC, CFB, CCM, and GCM modes of operation; RSA and DSA 2048, 3072, and 4,096 key sizes; ECDSA over curves P-256, P-384, P-521
- Hashing (support for SHA1, SHA-256, SHA-384, and SHA-512)
- Signing and verification (padding support for OAEP, PSS, and PKCS1)
- Key agreement and key derivation (support for ECDH over NIST-standard prime curves P-256, P-384, P-521 and HKDF)

Application developers can use these cryptographic modules to perform low-level cryptographic operations (Bcrypt), key storage operations (NCrypt), protect static data (DPAPI), and securely share secrets (DPAPI-NG).

[!INCLUDE [learn-more](includes/learn-more.md)]

- Cryptography and certificate management

Developers can access the modules on Windows through the Cryptography Next Generation API (CNG), which is powered by Microsoft's open-source cryptographic library, SymCrypt. SymCrypt supports complete transparency through its open-source code. In addition, SymCrypt offers performance optimization for cryptographic operations by taking advantage of assembly and hardware acceleration when available.

SymCrypt is part of Microsoft's commitment to transparency, which includes the global Microsoft Government Security Program that aims to provide the confidential security information and resources people need to trust Microsoft's products and services. The program offers controlled access to source code, threat and vulnerability information
exchange, opportunities to engage with technical content about Microsoft's products and services, and access to five globally distributed Transparency Centers.

## Certificates

To help safeguard and authenticate information, Windows provides comprehensive support for certificates and certificate management. The built-in certificate management command-line utility (certmgr.exe) or Microsoft Management Console (MMC) snap-in (certmgr.msc) can be used to view and manage certificates, certificate trust lists (CTLs), and certificate revocation lists (CRLs). Whenever a certificate is used in Windows, we validate that the leaf certificate and all the certificates in its chain of trust haven't been revoked or compromised. The trusted root and intermediate certificates and publicly revoked certificates on the machine are used as a reference for Public Key Infrastructure (PKI) trust and are updated monthly by the Microsoft Trusted Root program. If a trusted certificate or root is revoked, all global devices are updated, meaning users can trust that Windows will automatically protect against vulnerabilities in public key infrastructure. For cloud and enterprise deployments, Windows also offers users the ability to autoenroll and renew certificates in Active Directory with group policy to reduce the risk of potential outages due to certificate expiration or misconfiguration.

## Code signing and integrity

To ensure that Windows files haven't been tampered with, the Windows Code Integrity process verifies the signature of each file in Windows. Code signing is core to establishing the integrity of firmware, drivers, and software across the Windows platform. Code signing creates a digital signature by encrypting the hash of the file with the private key portion of a code-signing certificate and embedding the signature into the file. The Windows code integrity process verifies the signed file by decrypting the signature to check the integrity of the file and confirm that it is from a reputable publisher, ensuring that the file hasn't been tampered with.

The digital signature is evaluated across the Windows environment on Windows boot code, Windows kernel code, and Windows user mode applications. Secure Boot and Code Integrity verify the signature on bootloaders, Option ROMs, and other boot components to ensure that it's trusted and from a reputable publisher. For drivers not published by Microsoft, Kernel Code Integrity verifies the signature on kernel drivers and requires that drivers be signed by Windows or certified by the [Windows Hardware Compatibility Program (WHCP)][LINK-3]. This program ensures that third-party drivers are compatible with various hardware and Windows and that the drivers are from vetted driver developers.

## Device Health Attestation

The Windows Device Health Attestation process supports a Zero Trust paradigm that shifts the focus from static, network-based perimeters to users, assets, and resources. The attestation process confirms the device, firmware, and boot process are in a good state and haven't been tampered with before they can access corporate resources. These determinations are made with data stored in the TPM, which provides a secure root-of-trust. The information is sent to an attestation service such as Azure Attestation to verify that the device is in a trusted state. Then a cloud-native device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup> reviews device health and connects this information with Microsoft Entra ID<sup>[\[4\]](conclusion.md#footnote4)</sup> for conditional access.

Windows includes many security features to help protect users from malware and attacks. However, security components are trustworthy only if the platform boots as expected and isn't tampered with. As noted above, Windows relies on Unified Extensible Firmware Interface (UEFI) Secure Boot, ELAM, DRTM, Trusted Boot, and other low-level hardware and firmware security features to protect your PC from attacks. From the moment you power on your PC until your anti-malware starts, Windows is backed with the appropriate hardware configurations that help keep you safe. Measured Boot, implemented by bootloaders and BIOS, verifies and cryptographically records each step of the boot in a chained manner. These events are bound to the TPM, that functions as a hardware root-of-trust. Remote attestation is the mechanism by which these events are read and verified by a service to provide a verifiable, unbiased, and tamper-resilient report. Remote attestation is the trusted auditor of your system's boot, allowing reliant parties to bind trust to the device and its security.

A summary of the steps involved in attestation and Zero-Trust on a Windows device are as follows:

- During each step of the boot process - such as a file load, update of special variables, and more - information such as file hashes and signature(s) are measured in the TPM Platform Configuration Register (PCRs). The measurements are bound by a Trusted Computing Group specification that dictates which events can be recorded and the format of each event. The data provides important information about device security from the moment it powers on
- Once Windows has booted, the attestor (or verifier) requests the TPM get the measurements stored in its PCRs alongside the Measured Boot log. Together, these form the attestation evidence that's sent to the Azure Attestation service
- The TPM is verified by using the keys or cryptographic material available on the chipset with an Azure Certificate Service
- The above information is sent to the Azure Attestation Service to verify that the device is in a trusted state.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Control the health of Windows devices][LINK-4]

## Windows security policy settings and auditing

Security policy settings are a critical part of your overall security strategy. Windows provides a robust set of security setting policies that IT administrators can use to help protect Windows devices and other resources in your organization. Security policies settings are rules you can configure on a device, or multiple devices, to control:

- User authentication to a network or device
- Resources that users are permitted to access
- Whether to record a user or group's actions in the event log
- Membership in a group

Security auditing is one of the most powerful tools that you can use to maintain the integrity of your network and assets. Auditing can help identify attacks, network vulnerabilities, and attacks against high-value targets. You can specify categories of security-related events to create an audit policy tailored to the needs of your organization using configuration service providers (CSP) or group policies.

All auditing categories are disabled when Windows is first installed. Before enabling them, follow these steps to create an effective security auditing policy:

1. Identify your most critical resources and activities.
1. Identify the audit settings you need to track them.
1. Assess the advantages and potential costs associated with each resource or setting.
1. Test these settings to validate your choices.
1. Develop plans for deploying and managing your audit policy.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Security policy settings][LINK-5]
- [Security auditing][LINK-6]

## Windows Security

:::row:::
    :::column span="2":::
        Visibility and awareness of device security and health are key to any action taken. The Windows Security app provides an at-a-glance view of the security status and health of your device. These insights help you identify issues and act to make sure you're protected. You can quickly see the status of your virus and threat protection, firewall and network security, device security controls, and more.
    :::column-end:::
    :::column span="2":::
:::image type="content" source="images/windows-security.png" alt-text="Screenshot of the Windows Security app." border="false" lightbox="images/windows-security.png" :::
    :::column-end:::
:::row-end:::

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Stay protected with Windows Security][LINK-7]
- [Windows Security][LINK-8]

## :::image type="icon" source="images/new-button-title.svg" border="false"::: Config Refresh

With traditional group policy, policy settings are refreshed on a PC when a user signs in and every 90 minutes by default. Administrators can adjust that timing to be shorter to ensure that the policy settings are compliant with the management settings set by IT.

By contrast, with a device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, policies are refreshed when a user signs in and then at eight-hours interval by default. But policy settings are migrated from GPO to a device management solution, one remaining gap is the longer period between the reapplication of a changed policy.

Config Refresh allows settings in the Policy configuration service provider (CSP) that drift due to misconfiguration, registry edits, or malicious software on a PC to be reset to the value the administrator intended every 90 minutes by default. It's configurable to refresh every 30 minutes if desired. The Policy CSP covers hundreds of settings that were traditionally set with group policy and are now set through Mobile Device Management (MDM) protocols.

Config Refresh can also be paused for a configurable period of time, after which it will be reenabled. This is to support scenarios where a helpdesk technician might need to reconfigure a device for troubleshooting purposes. It can also be resumed at any time by an administrator.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Config Refresh][LINK-9]

## Kiosk mode

:::row:::
    :::column span="2":::
        Windows allows you to restrict functionality to specific applications using built-in features, making it ideal for public-facing or shared devices like kiosks. You can set up Windows as a kiosk either locally on the device, or through a cloud-based device management solution like Microsoft Intune<sup>[\[7\]](conclusion.md#footnote7)</sup>. Kiosk mode can be configured to run a single app, multiple apps, or a full-screen web browser. You can also configure the device to automatically sign in and launch the designated kiosk app at startup.
    :::column-end:::
    :::column span="2":::
:::image type="content" source="images/kiosk.png" alt-text="Screenshot of a Windows kiosk." border="false" lightbox="images/kiosk.png" :::
    :::column-end:::
:::row-end:::

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows kiosks and restricted user experiences](/windows/configuration/assigned-access)

## :::image type="icon" source="images/new-button-title.svg" border="false"::: Windows protected print

Windows protected print is built to provide a more modern and secure print system that maximizes compatibility and puts users first. It simplifies the printing experience by allowing devices to exclusively print using the Windows modern print stack.

The benefits of Windows protected print include:

- Increased PC security
- Simplified and consistent printing experience, regardless of PC architecture
- Removes the need to manage print drivers

Windows protected print is designed to work with Mopria certified printers only. Many existing printers are already compatible.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows protected print][LINK-10]
- [New, modern, and secure print experience from Windows][LINK-11]

## :::image type="icon" source="images/new-button-title.svg" border="false"::: Rust for Windows

Rust is a modern programming language known for its focus on safety, performance, and concurrency. It was designed to prevent common programming errors such as null pointer dereferencing and buffer overflows, which can lead to security vulnerabilities and crashes. Rust achieves this through its unique ownership system, which ensures memory safety without needing a garbage collector.
We're expanding the integration of Rust into the Windows kernel to enhance the safety and reliability of Windows' codebase. This strategic move underscores our commitment to adopting modern technologies to improve the quality and security of Windows.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Rust for Windows, and the windows crate][LINK-12]

<!--links-->

[LINK-1]: /windows/security/operating-system-security/system-security/secure-the-windows-10-boot-process
[LINK-2]: /windows/security/operating-system-security/system-security/trusted-boot
[LINK-3]: /windows-hardware/design/compatibility/
[LINK-4]: /windows/security/operating-system-security/system-security/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices
[LINK-5]: /windows/security/threat-protection/security-policy-settings/security-policy-settings
[LINK-6]: /windows/security/threat-protection/auditing/security-auditing-overview
[LINK-7]: https://support.microsoft.com/topic/2ae0363d-0ada-c064-8b56-6a39afb6a963
[LINK-8]:  /windows/security/operating-system-security/system-security/windows-defender-security-center/windows-defender-security-center
[LINK-9]: https://techcommunity.microsoft.com/blog/windows-itpro-blog/intro-to-config-refresh-%e2%80%93-a-refreshingly-new-mdm-feature/4176921
[LINK-10]: /windows-hardware/drivers/print/modern-print-platform
[LINK-11]: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/a-new-modern-and-secure-print-experience-from-windows/ba-p/4002645
[LINK-12]: /windows/dev-environment/rust/rust-for-windows
