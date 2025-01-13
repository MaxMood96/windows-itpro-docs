---
title: Personal Data Encryption
description: Personal Data Encryption unlocks user encrypted files at user sign-in instead of at boot.
ms.topic: how-to
ms.date: 09/24/2024
---

# Personal Data Encryption

Starting in Windows 11, version 22H2, Personal Data Encryption is a security feature that provides file-based data encryption capabilities to Windows.

Personal Data Encryption utilizes Windows Hello for Business to link *data encryption keys* with user credentials. When a user signs in to a device using Windows Hello for Business, decryption keys are released, and encrypted data is accessible to the user.\
When a user logs off, decryption keys are discarded and data is inaccessible, even if another user signs into the device.

The use of Windows Hello for Business offers the following advantages:

- It reduces the number of credentials to access encrypted content: users only need to sign-in with Windows Hello for Business
- The accessibility features available when using Windows Hello for Business extend to Personal Data Encryption protected content

Personal Data Encryption differs from BitLocker in that it encrypts files instead of whole volumes and disks. Personal Data Encryption occurs in addition to other encryption methods such as BitLocker.\
Unlike BitLocker that releases data encryption keys at boot, Personal Data Encryption doesn't release data encryption keys until a user signs in using Windows Hello for Business.

## Prerequisites

To use Personal Data Encryption, the following prerequisites must be met:

- Windows 11, version 22H2 and later
- The devices must be [Microsoft Entra joined][ENTRA-1] or [Microsoft Entra hybrid joined][ENTRA-2]. Domain-joined devices aren't supported
- Users must sign in using [Windows Hello for Business](../../../identity-protection/hello-for-business/index.md)

> [!IMPORTANT]
> If you sign in with a password or a [FIDO2 security key][ENTRA-3], you can't access Personal Data Encryption protected content.

[!INCLUDE [personal-data-encryption-pde](../../../../../includes/licensing/personal-data-encryption-pde.md)]

## Personal Data Encryption protection levels

Personal Data Encryption uses *AES-CBC* with a *256-bit key* to protect content and offers two levels of protection. The level of protection is determined based on the organizational needs. These levels can be set via the [Personal Data Encryption APIs](/uwp/api/windows.security.dataprotection.userdataprotectionmanager).

| Item | Level 1 | Level 2 |
|---|---|---|
| Protected data accessible when user has signed in via Windows Hello for Business | Yes | Yes |
| Protected data is accessible at Windows lock screen | Yes | Data is accessible for one minute after lock, then it's no longer available |
| Protected data is accessible after user signs out of Windows | No | No |
| Protected data is accessible when device is shut down | No | No |
| Protected data is accessible via UNC paths | No | No |
| Protected data is accessible when signing with Windows password instead of Windows Hello for Business | No | No |
| Protected data is accessible via Remote Desktop session | No | No |
| Decryption keys used by Personal Data Encryption discarded | After user signs out of Windows | One minute after Windows lock screen is engaged or after user signs out of Windows |

## Personal Data Encryption protected content accessibility

When a file is protected with Personal Data Encryption, its icon will show a padlock. If the user hasn't signed in locally with Windows Hello for Business or an unauthorized user attempts to access Personal Data Encryption protected content, they'll be denied access to the content.

Scenarios where a user will be denied access to Personal Data Encryption protected content include:

- User has signed into Windows via a password instead of signing in with Windows Hello for Business biometric or PIN
- If protected via level 2 protection, when the device is locked
- When trying to access content on the device remotely. For example, UNC network paths
- Remote Desktop sessions
- Other users on the device who aren't owners of the content, even if they're signed in via Windows Hello for Business and have permissions to navigate to the Personal Data Encryption protected content

## Differences between Personal Data Encryption and BitLocker

Personal Data Encryption is meant to work alongside BitLocker. Personal Data Encryption isn't a replacement for BitLocker, nor is BitLocker a replacement for Personal Data Encryption. Using both features together provides better security than using either BitLocker or Personal Data Encryption alone. However there are differences between BitLocker and Personal Data Encryption and how they work. These differences are why using them together offers better security.

| Item | Personal Data Encryption | BitLocker |
|--|--|--|
| Release of decryption key | At user sign-in via Windows Hello for Business | At boot |
| Decryption keys discarded | When user signs out of Windows or one minute after Windows lock screen is engaged | At shutdown |
| Protected content | All files in protected folders | Entire volume/drive |
| Authentication to access protected content | Windows Hello for Business | When BitLocker with TPM + PIN is enabled, BitLocker PIN plus Windows sign-in |

## Differences between Personal Data Encryption and EFS

The main difference between protecting files with Personal Data Encryption instead of EFS is the method they use to protect the file. Personal Data Encryption uses Windows Hello for Business to secure the keys that protect the files. EFS uses certificates to secure and protect the files.

To see if a file is protected with Personal Data Encryption or with EFS:

1. Open the properties of the file
1. Under the **General** tab, select **Advanced...**
1. In the **Advanced Attributes** windows, select **Details**

For Personal Data Encryption protected files, under **Protection status:** there will be an item listed as **Personal Data Encryption is:** and it will have the attribute of **On**.

For EFS protected files, under **Users who can access this file:**, there will be a **Certificate thumbprint** next to the users with access to the file. There will also be a section at the bottom labeled **Recovery certificates for this file as defined by recovery policy:**.

Encryption information including what encryption method is being used to protect the file can be obtained with the [`cipher.exe /c`](/windows-server/administration/windows-commands/cipher) command.

## Recommendations for using Personal Data Encryption

The following are recommendations for using Personal Data Encryption:

- Enable [BitLocker Drive Encryption](../bitlocker/index.md). Although Personal Data Encryption works without BitLocker, it's recommended to enable BitLocker. Personal Data Encryption is meant to work alongside BitLocker for increased security at it isn't a replacement for BitLocker
- Backup solution such as [OneDrive in Microsoft 365](/sharepoint/onedrive-overview). In certain scenarios, such as TPM resets or destructive PIN resets, the keys used by Personal Data Encryption to protect content will be lost making any protected content inaccessible. The only way to recover such content is from a backup. If the files are synced to OneDrive, to regain access you must re-sync OneDrive
- [Windows Hello for Business PIN reset service](../../../identity-protection/hello-for-business/hello-feature-pin-reset.md). Destructive PIN resets will cause keys used by Personal Data Encryption to protect content to be lost, making any content protected with Personal Data Encryption inaccessible. After a destructive PIN reset, content protected with Personal Data Encryption must be recovered from a backup. For this reason, Windows Hello for Business PIN reset service is recommended since it provides non-destructive PIN resets
- [Windows Hello Enhanced Sign-in Security](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security) offers additional security when authenticating with Windows Hello for Business via biometrics or PIN

## Windows out of box applications that support Personal Data Encryption

Certain Windows applications support Personal Data Encryption out of the box. If Personal Data Encryption is enabled on a device, these applications will utilize Personal Data Encryption:

| App name | Details |
|-|-|
| Mail | Supports protecting both email bodies and attachments|

## Next steps

- Learn about the available options to configure Personal Data Encryption and how to configure them via Microsoft Intune or configuration Service Provider (CSP): [Personal Data Encryption settings and configuration](configure.md)
- Review the [Personal Data Encryption FAQ](faq.yml)

<!--links used in this document-->

[ENTRA-1]: /entra/identity/devices/concept-directory-join
[ENTRA-2]: /entra/identity/devices/concept-hybrid-join
[ENTRA-3]: /entra/identity/authentication/howto-authentication-passwordless-security-key-windows#sign-in-with-fido2-security-key
