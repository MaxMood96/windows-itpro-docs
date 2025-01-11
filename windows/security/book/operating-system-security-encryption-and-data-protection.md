---
title: Windows 11 security book - Encryption and data protection
description: Operating System security chapter - Encryption and data protection.
ms.topic: overview
ms.date: 11/18/2024
---

# Encryption and data protection

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

When people travel with their PCs, their confidential information travels with them. Wherever confidential data is stored, it must be protected against unauthorized access, whether through physical device theft or from malicious applications.

## BitLocker

BitLocker is a data protection feature that integrates with the operating system to address the threats of data theft or exposure from lost, stolen, or improperly decommissioned devices. It uses the AES algorithm in XTS or CBC mode with 128-bit or 256-bit key lengths to encrypt data on the volume. During the initial setup, when BitLocker is enabled during OOBE and the user signs into their Microsoft account for the first time, BitLocker automatically saves its recovery password to the Microsoft account for retrieval if needed. Users also have the option to export the recovery password if they manually enable BitLocker. Recovery key content can be saved to cloud storage on OneDrive or Azure<sup>[\[4\]](conclusion.md#footnote4)</sup>.

For organizations, BitLocker can be managed via group policy or with a device management solution like Microsoft Intune<sup>[\[3\]](conclusion.md#footnote3)</sup>. It provides encryption for the OS, fixed data, and removable data drives (BitLocker To Go), using technologies such as Hardware Security Test Interface (HSTI), Modern Standby, UEFI Secure Boot, and TPM.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

The BitLocker preboot recovery screen includes the Microsoft account (MSA) hint, if the recovery password is saved to an MSA. This hint helps the user to understand which MSA account was used to store recovery key information.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [BitLocker overview](../operating-system-security/data-protection/bitlocker/index.md)

### BitLocker To Go

BitLocker To Go refers to BitLocker on removable data drives. BitLocker To Go includes the encryption of USB flash drives, SD cards, and external hard disk drives. Drives can be unlocked using a password, certificate on a smart card, or recovery password.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [BitLocker FAQ](../operating-system-security/data-protection/bitlocker/faq.yml)

## Device encryption

Device encryption is a Windows feature that simplifies the process of enabling BitLocker encryption on certain devices. It ensures that only the OS drive and fixed drives are encrypted, while external/USB drives remain unencrypted. Additionally, devices with externally accessible ports that allow DMA access are not eligible for device encryption. Unlike standard BitLocker implementation, device encryption is enabled automatically to ensure continuous protection. Once a clean installation of Windows is completed and the out-of-box experience is finished, the device is prepared for first use with encryption already in place.

Organizations have the option to disable device encryption in favor of a full BitLocker implementation. This allows for more granular control over encryption policies and settings, ensuring that the organization's specific security requirements are met.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

The Device encryption prerequisites of DMA and HSTI/Modern Standby are removed. This change makes more devices eligible for both automatic and manual device encryption.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Device encryption](../operating-system-security/data-protection/bitlocker/index.md#device-encryption)

## Encrypted hard drive

Encrypted hard drives are a class of hard drives that are self-encrypted at the hardware level. They allow for full-disk hardware encryption and are transparent to the user. These drives combine the security and management benefits provided by BitLocker, with the power of self-encrypting drives.

By offloading the cryptographic operations to hardware, encrypted hard drives increase BitLocker performance and reduce CPU usage and power consumption. Because encrypted hard drives encrypt data quickly, BitLocker deployment can be expanded across enterprise devices with little to no impact on productivity.

Encrypted hard drives enable:

- Smooth performance: encryption hardware integrated into the drive controller allows the drive to operate at full data rate without performance degradation
- Strong security based in hardware: encryption is always-on, and the keys for encryption never leave the hard drive. The drive authenticates the user independently from the operating system before it unlocks
- Ease of use: encryption is transparent to the user, and the user doesn't need to enable it. Encrypted hard drives are easily erased using an onboard encryption key. There's no need to re-encrypt data on the drive
- Lower cost of ownership: there's no need for new infrastructure to manage encryption keys since BitLocker uses your existing infrastructure to store recovery information. Your device operates more efficiently because processor cycles don't need to be used for the encryption process

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Encrypted hard drive](../operating-system-security/data-protection/encrypted-hard-drive.md)

## Personal Data Encryption

Personal Data Encryption is a user-authenticated encryption mechanism designed to protect user's content. Personal Data Encryption uses Windows Hello for Business as its modern authentication scheme, with PIN or biometric authentication methods. The encryption keys used by Personal Data Encryption are securely stored within the Windows Hello container. When a user signs in with Windows Hello, the container is unlocked, making the keys available to decrypt the user's content.

The initial release of Personal Data Encryption in Windows 11, version 22H2, introduced a set of public APIs that applications can adopt to safeguard content.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

Personal Data Encryption is further enhanced with *Personal Data Encryption for known folders*, which extends protection to the Windows folders: Documents, Pictures, and Desktop.

:::image type="content" source="images/pde.png" alt-text="Screenshot of files encrypted with Personal Data Encryption showing a padlock." border="false":::

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Personal Data Encryption](../operating-system-security/data-protection/personal-data-encryption/index.md)

## Email encryption

Email encryption allows users to secure email messages and attachments so that only the intended recipients with a digital identification (ID), or certificate, can read them<sup>[\[8\]](conclusion.md#footnote8)</sup>. Users can also *digitally sign* a message, which verifies the sender's identity and ensures the message hasn't been tampered with.

The new Outlook app included in Windows 11 supports various types of email encryption, including Microsoft Purview Message Encryption, S/MIME, and Information Rights Management (IRM).

When using Secure/Multipurpose Internet Mail Extensions (S/MIME), users can send encrypted messages to people within their organization and to external contacts who have the proper encryption certificates. Recipients can only read encrypted messages if they have the corresponding decryption keys. If an encrypted message is sent to recipients whose encryption certificates aren't available, Outlook asks you to remove these recipients before sending the email.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [S/MIME for message signing and encryption in Exchange Online](/exchange/security-and-compliance/smime-exo/smime-exo)
- [Get started with the new Outlook for Windows](https://support.microsoft.com/topic/656bb8d9-5a60-49b2-a98b-ba7822bc7627)
- [Email encryption](/purview/email-encryption)
