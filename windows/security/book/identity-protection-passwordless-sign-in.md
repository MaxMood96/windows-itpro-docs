---
title: Windows 11 security book - Passwordless sign-in
description: Identity protection chapter - Passwordless sign-in.
ms.topic: overview
ms.date: 11/18/2024
---

# Passwordless sign-in

:::image type="content" source="images/identity-protection.png" alt-text="Diagram containing a list of security features." lightbox="images/identity-protection.png" border="false":::

Passwords are a fundamental part of digital security, but they're often inconvenient and vulnerable to cyberattacks. With Windows 11, users can enjoy passwordless protection, which offers a more secure and user-friendly alternative. After a secure authorization process, credentials are safeguarded by multiple layers of hardware and software security, providing users with seamless, passwordless access to their apps and cloud services.

## Windows Hello

Too often, passwords are weak, stolen, or forgotten. Organizations are moving toward passwordless sign-in to reduce the risk of breaches, lower the cost of managing passwords, and improve productivity and satisfaction for their users and customers. Microsoft is committed to helping organizations move toward a secure, passwordless future with Windows Hello, a cornerstone of Windows security and identity protection.

Windows Hello can enable passwordless sign-in using biometric or PIN verification and provides built-in support for the FIDO2 passwordless industry standard. As a result, people no longer need to carry external hardware like a security key for authentication.

The secure, convenient sign-in experience can augment or replace passwords with a stronger authentication model based on a PIN or biometric data such as facial or fingerprint recognition secured by the Trusted Platform Module (TPM). Step-by-step guidance makes setup easy.

Using asymmetric keys provisioned in the TPM, Windows Hello protects authentication by binding a user's credentials to their device. Windows Hello validates the user based on either a PIN or biometrics match and only then allows the use of cryptographic keys bound to that user in the TPM.

PIN and biometric data stay on the device and can't be stored or accessed externally. Since the data can't be accessed by anyone without physical access to the device, credentials are protected against replay attacks, phishing, and spoofing as well as password reuse and leaks.

Windows Hello can authenticate users to a Microsoft account (MSA), identity provider services, or the relying parties that also implement the FIDO2 or WebAuthn standards.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Configure Windows Hello][LINK-1]

### Windows Hello PIN

The Windows Hello PIN, which can only be entered by someone with physical access to the device, can be used for strong multifactor authentication. The PIN is protected by the TPM and, like biometric data, never leaves the device. When a user enters their PIN, an authentication key is unlocked and used to sign a request sent to the authenticating server.

The TPM protects against threats including PIN brute-force attacks on lost or stolen devices. After too many incorrect guesses, the device locks. IT admins can set security policies for PINs, such as complexity, length, and expiration requirements.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

If your device doesn't have built-in biometrics, Windows Hello has been enhanced to use Virtualization-based Security (VBS) by default to isolate credentials. This added layer of protection helps guard against admin-level attacks. Even when you sign in with a PIN, your credentials are stored in a secure container, ensuring protection on devices with or without built-in biometric sensors.

### Windows Hello biometric

Windows Hello biometric sign-in enhances both security and productivity with a quick and convenient sign-in experience. There's no need to enter your PIN; just use your biometric data for an easy and delightful sign-in.

Windows devices that support biometric hardware, such as fingerprint or facial recognition cameras, integrate directly with Windows Hello, enabling access to Windows client resources and services. Biometric readers for both face and fingerprint must comply with Windows Hello biometric requirements. Windows Hello facial recognition is designed to authenticate only from trusted cameras used at the time of enrollment.

If a peripheral camera is attached to the device after enrollment, it can be used for facial authentication once validated by signing in with the internal camera. For added security, external cameras can be disabled for use with Windows Hello facial recognition.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Hello biometric requirements][LINK-4]

## Windows presence sensing

Windows presence sensing<sup>[\[9\]](conclusion.md#footnote9)</sup> provides another layer of data security protection for hybrid workers. Windows 11 devices can intelligently adapt to a user's presence to help them stay secure and productive, whether they're working at home, the office, or a public environment.

Windows presence sensing combines presence detection sensors with Windows Hello facial recognition to sign the user in hands-free and automatically locks the device when the user leaves. With adaptive dimming, the PC dims the screen when the user looks away on compatible devices with presence sensors. It's also easier than ever to configure presence sensors on devices, with easy enablement in the out-of-the-box experience and new links in Settings to help find presence sensing features. Device manufacturers can customize and build extensions for the presence sensor.

Privacy is top of mind and more important than ever. Customers want to have greater transparency and control over the use of their information. The new app privacy settings enable users to allow or block access to their presence sensor information. Users can decide on these settings during the initial Windows 11 setup.

Users can also take advantage of more granular settings to easily enable and disable differentiated presence sensing features like wake on approach, lock on leave, and adaptive dimming. We're also supporting developers with new APIs for presence sensing for third-party applications. Third-party applications can now access user presence information on devices with presence sensors.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Presence sensing][LINK-7]
- [Manage presence sensing settings in Windows 11][LINK-8]

## Windows Hello for Business

Windows Hello for Business extends Windows Hello to work with an organization's Active Directory and Microsoft Entra ID accounts. It provides single sign-on access to work or school resources such as OneDrive, work email, and other business apps. Windows Hello for Business also gives IT admins the ability to manage PIN and other sign-in requirements for devices connecting to work or school resources.

After Windows Hello for Business is provisioned, users can use a PIN, face, or fingerprint to unlock credentials and sign into their Windows device.

Provisioning methods include:

- Passkeys (preview), which provide a seamless way for users to authenticate to Microsoft Entra ID without entering a username or password
- Temporary Access Pass (TAP), a time-limited passcode with strong authentication requirements issued through Microsoft Entra ID
- Existing multifactor authentication with Microsoft Entra ID, including the Microsoft Authenticator app

Windows Hello for Business enhances security by replacing traditional usernames and passwords with a combination of a security key or certificate and a PIN or biometric data. This setup securely maps the credentials to a user account.

There are various deployment models available for Windows Hello for Business, providing flexibility to meet the diverse needs of different organizations. Among these, the *Hybrid cloud Kerberos trust* model is recommended and considered the simplest for organizations operating in hybrid environments.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Hello for Business overview][LINK-2]
- [Enable passkeys (FIDO2) for your organization][LINK-9]

### PIN reset

The Microsoft PIN Reset Service allows users to reset their forgotten Windows Hello PINs without requiring re-enrollment. After registering the service in the Microsoft Entra ID tenant, the capability must be enabled on the Windows devices using group policy or a device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>.

Users can initiate a PIN reset from the Windows lock screen or from the sign-in options in Settings. The process involves authenticating and completing multifactor authentication to reset the PIN.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [PIN reset][LINK-15]

### Multi-factor unlock

For organizations that need an extra layer of sign-in security, multi-factor unlock enables IT admins to configure Windows to require a combination of two unique trusted signals to sign in. Trusted signal examples include a PIN or biometric data (face or fingerprint) combined with either a PIN, Bluetooth, IP configuration, or Wi-Fi.

Multi-factor unlock is useful for organizations who need to prevent information workers from sharing credentials or need to comply with regulatory requirements for a two-factor authentication policy.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Multi-factor unlock][LINK-6]

### Windows passwordless experience

**Windows Hello for Business now support a fully passwordless experience.**

IT admins can configure a policy on Microsoft Entra ID joined machines so users no longer see the option to enter a password when accessing company resources. Once the policy is configured, passwords are removed from the Windows user experience, both for device unlock and in-session authentication scenarios. However, passwords aren't eliminated from the identity directory yet. Users are expected to navigate through their core authentication scenarios using strong, phish-resistant, possession-based credentials like Windows Hello for Business and FIDO2 security keys. If necessary, users can use passwordless recovery mechanisms such as Microsoft PIN reset service or web sign-in.

Users authenticate directly with Microsoft Entra ID, helping speed access to on-premises applications and other resources.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows passwordless experience][LINK-3]

## Enhanced Sign-in Security (ESS)

Windows Hello supports Enhanced Sign-in Security, which uses specialized hardware and software components to raise the security bar even higher for biometric sign-in.

Enhanced Sign-in Security biometrics uses Virtualization-based security (VBS) and the TPM to isolate user authentication processes and data and secure the pathway by which the information is communicated.

These specialized components protect against a class of attacks that includes biometric sample injection, replay, and tampering. For example, fingerprint readers must implement Secure Device Connection Protocol, which uses key negotiation and a Microsoft-issued certificate to protect and securely store user authentication data. For facial recognition, components such as the Secure Devices (SDEV) table and process isolation with trustlets help prevent more attack classes.

Enhanced Sign-in Security is configured by device manufacturers during the manufacturing process and is most typically supported in secured-core PCs. For facial recognition, Enhanced Sign-in Security is supported by specific silicon and camera combinations -  check with the specific device manufacturer. Fingerprint authentication is available across all processor types. Reach out to specific OEMs for support details.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Hello Enhanced Sign-in Security][LINK-5]

## FIDO2

The FIDO Alliance, the Fast Identity Online industry standards body, was established to promote authentication technologies and standards that reduce reliance on passwords. FIDO Alliance and World Wide Web Consortium (W3C) worked together to define the Client to Authenticator Protocol (CTAP2) and Web Authentication (WebAuthn) specifications. These specifications are the industry standard for providing strong, phishing-resistant, user friendly, and privacy preserving authentication across the web and apps. FIDO standards and certifications are becoming recognized as the leading standard for creating secure authentication solutions across enterprises, governments, and consumer markets.

Windows 11 can also use external FIDO2 security keys for authentication alongside or in addition to Windows Hello and Windows Hello for Business, which is also a FIDO2-certified passwordless solution. As a result, Windows 11 can be used as a FIDO authenticator for many popular identity management services.

### Passkeys

Windows 11 makes it much harder for hackers who exploit stolen passwords via phishing attacks by empowering users to replace passwords with passkeys. Passkeys are the cross-platform future of secure sign-in. Microsoft and other technology leaders are supporting passkeys across their platforms and services.

A passkey is a unique, unguessable cryptographic secret that is securely stored on the device. Instead of using a username and password to sign in to a website or application, Windows 11 users can create and use a passkey with Windows Hello, a third-party passkey provider, an external FIDO2 security key, or their mobile device. Passkeys on Windows work in any browsers or apps that support them for sign in.

Passkeys created and saved with Windows Hello are protected by Windows Hello or Windows Hello for Business. Users can sign in to the site or app using their face, fingerprint, or device PIN. Users can manage their passkeys from **Settings** > **Accounts** > **Passkeys**.

:::row:::
    :::column span="2":::
[!INCLUDE [coming-soon](includes/coming-soon.md)]

The plug-in model for third-party passkey providers enables users to manage their passkeys with third-party passkey managers. This model ensures a seamless platform experience, regardless of whether passkeys are managed directly by Windows or by a third-party authenticator. When a third-party passkey provider is used, the passkeys are securely protected and managed by the third-party provider.
    :::column-end:::
    :::column span="2":::
:::image type="content" border="false" source="images/passkey-save-3p.png" alt-text="Screenshot of the save passkey dialog box showing third-party providers."  lightbox="images/passkey-save-3p.png":::
    :::column-end:::
:::row-end:::

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Support for passkeys in Windows][LINK-10]
- [Enable passkeys (FIDO2) for your organization][LINK-9]

## Microsoft Authenticator

The Microsoft Authenticator app, which runs on iOS and Android devices, helps keeping Windows 11 users secure and productive. Microsoft Authenticator with Microsoft Entra passkeys can be used as a phish-resistant method to bootstrap Windows Hello for Business.

Microsoft Authenticator also enables easy, secure sign-in for all online accounts using multifactor authentication, passwordless phone sign-in, phishing-resistant authentication (passkeys), or password autofill. The accounts in the Authenticator app are secured with a public/private key pair in hardware-backed storage such as the Keychain in iOS and Keystore on Android. IT admins can use different tools to nudge their users to set up the Authenticator app, provide them with extra context about where the authentication is coming from, and ensure that they're actively using it.

Individual users can back up their credentials to the cloud by enabling the encrypted backup option in settings. They can also see their sign-in history and security settings for Microsoft personal, work, or school accounts.

Using this secure app for authentication and authorization enables people to be in control of how, where, and when their credentials are used. To keep up with an ever-changing security landscape, the app is constantly updated, and new capabilities are added to stay ahead of emerging threat vectors.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Authentication methods in Microsoft Entra ID - Microsoft Authenticator app][LINK-11]

## Web sign-in

With the support of web sign-in, users can sign in without a password using the Microsoft Authenticator app or a Temporary Access Pass (TAP). Web sign in also enables federated sign in with a SAML-P identity provider.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Web sign-in for Windows][LINK-13]

## Federated sign-in

Windows 11 supports federated sign-in with external education identity management services. For students unable to type easily or remember complex passwords, this capability enables secure sign-in through methods like QR codes or pictures.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Configure federated sign-in for Windows devices][LINK-14]

## Smart cards

Organizations can also opt for smart cards, an authentication method that existed before biometric authentication. These tamper-resistant, portable storage devices enhance Windows security by authenticating users, signing code, securing e-mails, and signing in with Windows domain accounts.

Smart cards provide:

- Ease of use in scenarios such as healthcare, where users need to sign in and out quickly without using their hands or when sharing a workstation
- Isolation of security-critical computations that involve authentication, digital signatures, and key exchange from other parts of the computer. These computations are performed on the smart card
- Portability of credentials and other private information between computers at work, home, or on the road

Smart cards can only be used to sign in to domain accounts or Microsoft Entra ID accounts.

When a password is used to sign in to a domain account, Windows uses the Kerberos Version 5 (V5) protocol for authentication. If you use a smart card, the operating system uses Kerberos V5 authentication with X.509 V3 certificates. On Microsoft Entra ID joined devices, a smart card can be used with Microsoft Entra ID certificate-based authentication. Smart cards can't be used with local accounts.

Windows Hello for Business and FIDO2 security keys are modern, two-factor authentication methods for Windows. Customers using virtual smart cards are encouraged to move to Windows Hello for Business or FIDO2. For new Windows installations, we recommend Windows Hello for Business or FIDO2 security keys.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Smart Card technical reference][LINK-12]

## Enhanced phishing protection in Microsoft Defender SmartScreen

As malware protection and other safeguards evolve, cybercriminals look for new ways to circumvent security measures. Phishing is a leading threat, with apps and websites designed to steal credentials by tricking people into voluntarily entering passwords. As a result, many organizations are transitioning to the ease and security of passwordless sign-in with Windows Hello or Windows Hello for Business.

We know that people are in different parts of their passwordless journey. To help on that journey for people still using passwords, Windows 11 offers powerful credential protection. Microsoft Defender SmartScreen now includes enhanced phishing protection to automatically detect when a user's Microsoft password is entered into any app or website. Windows then identifies if the app or site is securely authenticating to Microsoft and warns if the credentials are at risk. Because the user is alerted at the moment of potential credential theft, they can take preemptive action before the password is used against them or their organization.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Enhanced phishing protection in Microsoft Defender SmartScreen][LINK-16]

<!--links-->

[LINK-1]: https://support.microsoft.com/topic/dae28983-8242-bb2a-d3d1-87c9d265a5f0
[LINK-2]: /windows/security/identity-protection/hello-for-business
[LINK-3]: /windows/security/identity-protection/passwordless-experience
[LINK-4]: /windows-hardware/design/device-experiences/windows-hello-biometric-requirements
[LINK-5]: /windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security
[LINK-6]: /windows/security/identity-protection/hello-for-business/feature-multifactor-unlock
[LINK-7]: /windows-hardware/design/device-experiences/sensors-presence-sensing
[LINK-8]: https://support.microsoft.com/topic/82285c93-440c-4e15-9081-c9e38c1290bb
[LINK-9]: /entra/identity/authentication/how-to-enable-passkey-fido2
[LINK-10]: /windows/security/identity-protection/passkeys
[LINK-11]: /entra/identity/authentication/concept-authentication-authenticator-app
[LINK-12]: /windows/security/identity-protection/smart-cards/smart-card-windows-smart-card-technical-reference
[LINK-13]: /windows/security/identity-protection/web-sign-in
[LINK-14]: /education/windows/federated-sign-in
[LINK-15]: /windows/security/identity-protection/hello-for-business/pin-reset
[LINK-16]: /windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/enhanced-phishing-protection
