---
title: Windows 11 security book - Cloud services - Protect your work information
description: Cloud services chapter - Protect your work information.
ms.topic: overview
ms.date: 11/04/2024
---

# Protect your work information

:::image type="content" source="images/cloud-security.png" alt-text="Diagram containing a list of security features for cloud security." lightbox="images/cloud-security.png" border="false":::

## :::image type="icon" source="images/microsoft-entra-id.svg" border="false"::: Microsoft Entra ID

Microsoft Entra ID is a comprehensive cloud-based identity management solution that helps enable secure access to applications, networks, and other resources and guard against threats. Microsoft Entra ID can also be used with Windows Autopilot for zero-touch provisioning of devices preconfigured with corporate security policies.

Organizations can deploy Microsoft Entra ID joined devices to enable access to both cloud and on-premises apps and resources. Access to resources can be controlled based on the Microsoft Entra ID account and Conditional Access policies applied to the device. For the most seamless and delightful end to end single sign-on (SSO) experience, we recommend users configure Windows Hello for Business during the out of box experience for easy passwordless sign-in to Entra ID .

:::row:::
    :::column:::
        For users wanting to connect to Microsoft Entra on their personal devices, they can do so by adding their work or school account to Windows. This action registers the user's personal device with Microsoft Entra ID, allowing IT admins to support users in bring your own device (BYOD) scenarios. Credentials are authenticated and bound to the joined device, and can't be copied to another device without explicit reverification.
    :::column-end:::
    :::column:::
:::image type="content" source="images/device-registration.png" alt-text="Screenshot of the Entra account registration page." border="false" lightbox="images/device-registration.png":::
    :::column-end:::
:::row-end:::

To provide more security and control for IT and a seamless experience for users, Microsoft Entra ID works with apps and services, including on-premises software and thousands of software-as-a-service (SaaS) applications. Microsoft Entra ID protections include single sign-on, multifactor authentication, conditional access policies, identity protection, identity governance, and privileged identity management.

Windows 11 works with Microsoft Entra ID to provide secure access, identity management, and single sign-on to apps and services from anywhere. Windows has built-in settings to add work or school accounts by syncing the device configuration to an Active Directory domain or Microsoft Entra ID tenant.

:::image type="content" source="images/access-work-or-school.png" alt-text="Screenshot of the add work or school account in Settings." border="false":::

When a device is Microsoft Entra ID joined and managed with Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, it receives the following security benefits:

- Default managed user and device settings and policies
- Single sign-in to all Microsoft Online Services
- Full suite of authentication management capabilities using Windows Hello for Business
- Single sign-on (SSO) to enterprise and SaaS applications
- No use of consumer Microsoft account identity

Organizations and users can join or register their Windows devices with Microsoft Entra ID to get a seamless experience to both native and web applications. In addition, users can set up Windows Hello for Business or FIDO2 security keys with Microsoft Entra ID and benefit from greater security with passwordless authentication.

In combination with Microsoft Intune, Microsoft Entra ID offers powerful security control through Conditional Access to restrict access to organizational resources to healthy and compliant devices. Note that Microsoft Entra ID is only supported on Windows Pro and Enterprise editions.

Every Windows device has a built-in local administrator account that must be secured and protected to mitigate any Pass-the-Hash (PtH) and lateral traversal attacks. Many customers have been using our standalone, on-premises Windows Local Administrator Password Solution (LAPS) to manage their domain-joined Windows machines. We heard from many customers that LAPS support was needed as they modernized their Windows environment to join directly to Microsoft Entra ID.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft Entra ID documentation][LINK-1]
- [Microsoft Entra plans and pricing][LINK-2]

### Microsoft Entra Private Access

Microsoft Entra Private Access provides organizations the ability to manage and give users access to private or internal fully qualified domain names (FQDNs) and IP addresses. With Private Access, you can modernize how your organization's users access private apps and resources. Remote workers don't need to use a VPN to access these resources if they have the Global Secure Access Client installed. The client quietly and seamlessly connects them to the resources they need.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft Entra Private Access][LINK-4]

### Microsoft Entra Internet Access

Microsoft Entra Internet Access provides an identity-centric Secure Web Gateway (SWG) solution for Software as a Service (SaaS) applications and other Internet traffic. It protects users, devices, and data from the Internet's wide threat landscape with best-in-class security controls and visibility through Traffic Logs.

> [!NOTE]
> Both Microsoft Entra Private Access and Microsoft Entra Internet Access requires Microsoft Entra ID and Microsoft Entra Joined devices for deployment. The two solutions use the Global Secure Access client for Windows, which secures and controls the features.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft Entra Internet Access][LINK-3]
- [Global Secure Access client for Windows][LINK-6]
- [Microsoft's Security Service Edge Solution Deployment Guide for Microsoft Entra Internet Access Proof of Concept][LINK-5]

### Enterprise State Roaming

Available to any organization with a Microsoft Entra ID Premium<sup>[\[4\]](conclusion.md#footnote4)</sup> license, Enterprise State Roaming provides users with a unified Windows Settings experience across their Windows devices and reduces the time needed for configuring a new device.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Enterprise State Roaming in Microsoft Entra ID][LINK-7]

## :::image type="icon" source="images/azure-attestation.svg" border="false"::: Azure Attestation service

Remote attestation helps ensure that devices are compliant with security policies and are operating in a trusted state before they're allowed to access resources. Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup> integrates with Azure Attestation service to review Windows device health comprehensively and connect this information with Microsoft Entra ID<sup>[\[4\]](conclusion.md#footnote4)</sup> Conditional Access.

**Attestation policies are configured in the Azure Attestation service which can then:**

- Verify the integrity of evidence provided by the Windows Attestation component by validating the signature and ensuring the Platform Configuration Registers (PCRs) match the values recomputed by replaying the measured boot log
- Verify that the TPM has a valid Attestation Identity Key issued by the authenticated TPM
- Verify that security features are in the expected states

Once this verification is complete, the attestation service returns a signed report with the security features state to the relying party - such as Microsoft Intune - to assess the trustworthiness of the platform relative to the admin-configured device compliance specifications. Conditional access is then granted or denied based on the device's compliance.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Azure Attestation overview][LINK-8]

## :::image type="icon" source="images/defender-for-endpoint.svg" border="false"::: Microsoft Defender for Endpoint

Microsoft Defender for Endpoint<sup>[\[4\]](conclusion.md#footnote4)</sup> is an enterprise endpoint detection and response solution that helps security teams detect, disrupt, investigate, and respond to advanced threats. Organizations can use the rich event data and attack insights Defender for Endpoint provides to investigate incidents.

Defender for Endpoint brings together the following elements to provide a more complete picture of security incidents:

- Endpoint behavioral sensors: Embedded in Windows, these sensors collect and process behavioral signals from the operating system and send this sensor data to your private, isolated cloud instance of Microsoft Defender for Endpoint
- With Automatic Attack Disruption uses AI, machine learning, and Microsoft Security Intelligence to analyze the entire attack and respond at the incident level, where it's able to contain a device, and/or a user which reduces the impact of attacks such as ransomware, human-operated attacks, and other advanced attacks.
- Cloud security analytics: Behavioral signals are translated into insights, detections, and recommended responses to advanced threats. These analytics leverage big data, device learning, and unique Microsoft optics across the Windows ecosystem, enterprise cloud products such as Microsoft 365<sup>[\[4\]](conclusion.md#footnote4)</sup>, and online assets
- Threat intelligence: Microsoft processes over 43 trillion security signals every 24 hours, yielding a deep and broad view into the evolving threat landscape. Combined with our global team of security experts and cutting-edge artificial intelligence and machine learning, we can see threats that others miss. This threat intelligence helps provide unparalleled protection for our customers. The protections built into our platforms and products blocked attacks that include 31 billion identity threats and 32 billion email threats
- Rich response capabilities: Defender for Endpoint empowers SecOps teams to isolate, remediate, and remote into machines to further investigate and stop active threats in their environment, as well as block files, network destinations, and create alerts for them. In addition, Automated Investigation and Remediation can help reduce the load on the SOC by automatically performing otherwise manual steps towards remediation and providing
detailed investigation outcomes

Defender for Endpoint is also part of Microsoft Defender XDR, our end-to-end, cloud-native extended detection and response (XDR) solution that combines best-of-breed endpoint, email, and identity security products. It enables organizations to prevent, detect, investigate, and remediate attacks by delivering deep visibility, granular context, and actionable insights generated from raw signals harnessed across the Microsoft 365 environment and other
platforms, all synthesized into a single dashboard. This solution offers tremendous value to organizations of any size, especially those that are looking to break away from the added complexity of multiple point solutions, keeping them protected from sophisticated attacks and saving IT and security teams' time and resources.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft 365 Defender](/defender-xdr/microsoft-365-defender)

## Cloud-native device management

Microsoft recommends cloud-based device management so that IT professionals can manage company security policies and business applications without compromising user privacy on corporate or employee-owned devices. With cloud-native device management solutions like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, IT can manage Windows 11 using industry standard protocols. To simplify setup for users, management features are built directly into Windows, eliminating the need for a separate device management client.

Windows 11 built-in management features include:

- The enrollment client, which enrolls and configures the device to securely communicate with the enterprise device management server
- The management client, which periodically synchronizes with the management server to check for updates and apply the latest policies set by IT

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Mobile device management overview][LINK-9]

### Remote wipe

When a device is lost or stolen, IT administrators might want to remotely wipe data stored in memory and hard disks. A helpdesk agent might also want to reset devices to fix issues encountered by remote workers. A remote wipe can also be used to prepare a previously used device for a new user.

Windows 11 supports the Remote Wipe configuration service provider (CSP) so that device management solutions can remotely initiate any of the following operations:

- Reset the device and remove user accounts and data
- Reset the device and clean the drive
- Reset the device but persist user accounts and data

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Remote wipe CSP][LINK-10]

## :::image type="icon" source="images/microsoft-intune.svg" border="false"::: Microsoft Intune

Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup> is a comprehensive cloud-native endpoint management solution that helps secure, deploy, and manage users, apps, and devices. Intune brings together technologies like Microsoft Configuration Manager and Windows Autopilot to simplify provisioning, configuration management, and software updates across the organization.

Intune works with Microsoft Entra ID to manage security features and processes, including multifactor authentication and conditional access.

Organizations can cut costs while securing and managing remote devices through the cloud in compliance with company policies<sup>[\[11\]](conclusion.md#footnote11)</sup>. For example, organizations can save time and money by provisioning preconfigured devices to remote employees using Windows Autopilot.

Windows 11 enables IT professionals to move to the cloud while consistently enforcing security policies. Windows 11 provides expanded support for group policy administrative templates (ADMX-backed policies) in cloud-native device management solutions like Microsoft Intune, enabling IT professionals to easily apply the same security policies to both on-premises and remote devices.

Customers have asked for App Control for Business (previously called *Windows Defender Application Control*) to support manage installer for a long time. Now it's possible to enable allowlisting of Win32 apps to proactively reduce the number of malware infections.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [What is Microsoft Intune][LINK-12]

### Windows enrollment attestation

When a device enrolls into device management, the administrator expects it to receive the appropriate policies to secure and manage the PC. However, in some cases, malicious actors can remove enrollment certificates and use them on unmanaged PCs, making them appear enrolled but without the intended security and management policies.

With Windows enrollment attestation, Microsoft Entra and Microsoft Intune certificates are bound to a device using the Trusted Platform Module (TPM). This ensures that the certificates can't be transferred from one device to another, maintaining the integrity of the enrollment process.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows enrollment attestation][LINK-13]

### Microsoft Cloud PKI

Microsoft Cloud PKI is a cloud-based service included in the Microsoft Intune Suite<sup>[\[4\]](conclusion.md#footnote4)</sup> that simplifies and automates the management of a Public Key Infrastructure (PKI) for organizations. It eliminates the need for on-premises servers, hardware, and connectors, making it easier to set up and manage a PKI compared to, for instance, Microsoft Active Directory Certificate Services (AD CS) combined with the Certificate Connector for Microsoft Intune.

Key features include:

- Certificate lifecycle management: automates the lifecycle of certificates, including issuance, renewal, and revocation, for all devices managed by Intune
- Multi-platform support: supports certificate management for Windows, iOS/iPadOS, macOS, and Android devices
- Enhanced security: enables certificate-based authentication for Wi-Fi, VPN, and other scenarios, improving security over traditional password-based methods. All certificate requests leverage Simple Certificate Enrollment Protocol (SCEP), making sure that the private key never leaves the requesting client
- Simplified management: provides easy management of certification authorities (CAs), registration authorities (RAs), certificate revocation lists (CRLs), monitoring, and reporting

With Microsoft Cloud PKI, organizations can accelerate their digital transformation and achieve a fully managed cloud PKI service with minimal effort.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Overview of Microsoft Cloud PKI for Microsoft Intune](/mem/intune/protect/microsoft-cloud-pki-overview)

### Endpoint Privilege Management (EPM)

Intune Endpoint Privilege Management supports organizations' Zero Trust journeys by helping them achieve a broad user base running with least privilege, while still permitting users to run elevated tasks allowed by the organization to remain productive.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Endpoint Privilege Management][LINK-14]

### Mobile application management (MAM)

With Intune, organizations can also extend MAM App Config, MAM App Protection, and App Protection Conditional Access capabilities to Windows. This enables people to access protected organizational content without having the device managed by IT. The first application to support MAM for Windows is Microsoft Edge.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Data protection for Windows MAM][LINK-15]

## Security baselines

Every organization faces security threats. However, different organizations can be concerned with different types of security threats. For example, an e-commerce company might focus on protecting its internet-facing web apps, while a hospital on confidential patient information. The one thing that all organizations have in common is a need to keep their apps and devices secure. These devices must be compliant with the security standards (or security baselines) defined by the organization.

A security baseline is a group of Microsoft-recommended configuration settings that explains their security implications. These settings are based on feedback from Microsoft security engineering teams, product groups, partners, and customers.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Security baselines][LINK-11]

### Security baseline for cloud-based device management solutions

Windows 11 can be configured with Microsoft's security baseline, designed for cloud-based device management solutions like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>. These security baselines function similarly to group policy-based ones and can be easily integrated into existing device management tools.

The security baseline includes policies for:

- Microsoft inbox security technologies such as BitLocker, Microsoft Defender SmartScreen, Virtualization-based security, Exploit Guard, Microsoft Defender Antivirus, and Windows Firewall
- Restricting remote access to devices
- Setting credential requirements for passwords and PINs
- Restricting the use of legacy technology

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Intune security baseline overview][LINK-16]
- [List of the settings in the Windows security baseline in Intune][LINK-17]

## Windows Local Administrator Password Solution (LAPS)

Windows Local Administrator Password Solution (LAPS) is a feature that automatically manages and backs up the password of a local administrator account on Microsoft Entra joined and Active Directory-joined devices. It helps enhance security by regularly rotating and managing local administrator account passwords, protecting against pass-the-hash and lateral-traversal attacks.

Windows LAPS can be configured via group policy or with a device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>.

[!INCLUDE [new-24h2](includes/new-24h2.md)]

Several enhancements have been made to improve manageability and security. Administrators can now configure LAPS to automatically create managed local accounts, integrating with existing policies to enhance security and efficiency. Policy settings have been updated to generate more readable passwords by ignoring certain characters and to support the generation of readable passphrases, with options to choose from three separate word source list and control passphrase length. Additionally, LAPS can detect when a computer rolls back to a previous image, ensuring password consistency between the computer and Active Directory.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows LAPS overview][LINK-18]

## Windows Autopilot

Traditionally, IT professionals spend significant time building and customizing images that will later be deployed to devices. If you're purchasing new devices or managing device refresh cycles, you can use Windows Autopilot to set up and preconfigure new devices, getting them ready for productive use. Autopilot helps you ensure your devices are delivered locked down and compliant with corporate security policies. The solution can also be used to reset, repurpose, and recover devices with zero touch by your IT team and no infrastructure to manage, enhancing efficiency with a process that's both easy and simple.

With Windows Autopilot, there's no need to reimage or manually set-up devices before giving them to the users. Your hardware vendor can ship them, ready to go, directly to the users. From a user perspective, they turn on their device, go online, and Windows Autopilot delivers apps and settings.

Windows Autopilot enables you to:

- Automatically join devices to Microsoft Entra ID or Active Directory via Microsoft Entra hybrid join
- Autoenroll devices into a device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup> (requires a Microsoft Entra ID Premium subscription for configuration)
- Create and autoassignment of devices to configuration groups based on a device's profile
- Customize of the out-of-box experience (OOBE) content specific to your organization

Existing devices can also be quickly prepared for a new user with Windows Autopilot Reset. The reset capability is also useful in break/fix scenarios to quickly bring a device back to a business-ready state.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Autopilot][LINK-19]
- [Windows Autopilot Reset][LINK-20]

## Windows Update for Business

Windows Update for Business empowers IT administrators to ensure that their organization's Windows client devices are consistently up to date with the latest security updates and features. By directly connecting these systems to the Windows Update service, administrators can maintain a high level of security and functionality.

Administrators can utilize group policy or a device management solution like Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, to configure Windows Update for Business settings. These settings control the timing and manner in which updates are applied, allowing for thorough reliability and performance testing on a subset of devices before deploying updates across the entire organization.

This approach not only provides control over the update process but also ensures a seamless and positive update experience for all users within the organization. By using Windows Update for Business, organizations can achieve a more secure and efficient operational environment.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Update for Business documentation][LINK-21]

## Windows Autopatch

Cybercriminals commonly exploit obsolete or unpatched software to infiltrate networks. It's essential to maintain current updates to seal security gaps. Windows Autopatch is a cloud service that automates Windows, Microsoft 365 Apps for enterprise, Microsoft Edge, and Microsoft Teams updates to improve security and productivity across your organization. Autopatch helps you minimize the involvement of your scarce IT resources in the planning and deployment of updates so your IT Admins can focus on other activities and tasks.

There's a lot more to learn about Windows Autopatch: this [Forrester Consulting Total Economic Impact&trade; Study][LINK-22] commissioned by Microsoft, features insights from customers who deployed Windows Autopatch and its impact on their organizations. You can also find out more information about new Autopatch features and the future of the service in the regularly published Windows IT Pro Blog and Windows Autopatch community.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Autopatch documentation](/windows/deployment/windows-autopatch/)
- [Windows updates API overview](/graph/windowsupdates-concept-overview)
- [Windows IT Pro Blog](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/bg-p/Windows-ITPro-blog/label-name/Windows%20Autopatch)
- [Windows Autopatch community](https://techcommunity.microsoft.com/t5/windows-autopatch/bd-p/Windows-Autopatch)

## :::image type="icon" source="images/soon-button-title.svg" border="false"::: Windows Hotpatch

Windows Hotpatch is a feature designed to enhance security and minimize disruptions. With Windows Hotpatch, organizations can apply critical security updates without requiring a system restart, reducing the time to adopt a security update by 60% from the moment the update is offered. Hotpatch updates streamline the installation process, enhance compliance efficiency, and provide a per-policy level view of update statuses for all devices.

By utilizing hotpatching through Windows Autopatch, the number of system restarts for Windows updates can be reduced from 12 times a year to just 4, ensuring consistent protection and uninterrupted productivity. This means less downtime, a streamlined experience for users, and a reduction in security risks. This technology, proven in the Azure Server environment, is now expanding to Windows 11, offering immediate security from day one without the need for a restart.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows Autopatch documentation](/windows/deployment/windows-autopatch/)

## :::image type="icon" source="images/onedrive.svg" border="false"::: OneDrive for work or school

OneDrive for work or school is a cloud storage service that allows users to store, share, and collaborate on files. It's a part of Microsoft 365 and is designed to help organizations protect their data and comply with regulations. OneDrive for work or school is protected both in transit and at rest.

When data transits either into the service from clients or between datacenters, it's protected using transport layer security (TLS) encryption. OneDrive only permits secure access.

Authenticated connections aren't allowed over HTTP and instead redirect to HTTPS.

There are several ways that OneDrive for work or school is protected at rest:

- Physical protection: Microsoft understands the importance of protecting customer data and is committed to securing the datacenters that contain it. Microsoft datacenters are designed, built, and operated to strictly limit physical access to the areas where customer data is stored. Physical security at datacenters is in alignment with the defense-in-depth principle. Multiple security measures are implemented to reduce the risk of unauthorized users accessing data and other datacenter resources. Learn more [here](/compliance/assurance/assurance-datacenter-physical-access-security).
- Network protection: The networks and identities are isolated from the corporate network. Firewalls limit traffic into the environment from unauthorized locations
- Application security: Engineers who build features follow the security development lifecycle. Automated and manual analyses help identify possible vulnerabilities. The [Microsoft Security Response Center](https://technet.microsoft.com/security/dn440717.aspx) helps triage incoming vulnerability reports and evaluate mitigations. Through the [Microsoft Cloud Bug Bounty Terms](https://technet.microsoft.com/dn800983), people across the world can earn money by reporting vulnerabilities
- Content protection: Each file is encrypted at rest with a unique AES-256 key. These unique keys are encrypted with a set of master keys that are stored in Azure Key Vault

[!INCLUDE [learn-more](includes/learn-more.md)]

- [How OneDrive safeguards data in the cloud](https://support.microsoft.com/topic/23c6ea94-3608-48d7-8bf0-80e142edd1e1)

## :::image type="icon" source="images/universal-print.svg" border="false"::: Universal Print

Universal Print eliminates the need for on-premises print servers. It also eliminates the need for print drivers from the users' Windows devices and makes the devices secure, reducing the malware attacks that typically exploit vulnerabilities in driver model. It enables Universal Print-ready printers (with native support) to connect directly to the Microsoft Cloud. All major printer OEMs have these [models][LINK-23]. It also supports existing printers by using the connector software that comes with Universal Print.

Unlike traditional print solutions that rely on Windows print servers, Universal Print is a Microsoft-hosted cloud subscription service that supports a Zero Trust security model when using the Universal Print-ready printers. Customers can enable network isolation of printers, including the Universal Print connector software, from the rest of the organization's resources. Users and their devices don't need to be on the same local network as the printers or the Universal Print connector.

Universal Print supports Zero Trust security by requiring that:

- Each connection and API call to Universal Print cloud service requires authentication validated by Microsoft Entra ID<sup>[\[4\]](conclusion.md#footnote4)</sup>. A hacker would have to have knowledge of the right credentials to successfully connect to the Universal Print service
- Every connection established by the user's device (client), the printer, or another cloud service to the Universal Print cloud service uses SSL with TLS 1.2 protection. This protects network snooping of traffic to gain access to sensitive data
- Each printer registered with Universal Print is created as a device object in the customer's Microsoft Entra ID tenant and issued its own device certificate. Every connection from the printer is authenticated using this certificate. The printer can access only its own data and no other device's data
- Applications can connect to Universal Print using either user, device, or application authentication. To ensure data security, it's highly recommended that only cloud applications use application authentication
- Each acting application must register with Microsoft Entra ID and specify the set of permission scopes it requires. Microsoft's own acting applications - for example, the Universal Print connector - are registered with the Microsoft Entra ID service. Customer administrators need to provide their consent to the required permission scopes as part of onboarding the application to their tenant
- Each authentication with Microsoft Entra ID from an acting application can't extend the permission scope as defined by the acting client app. This prevents the app from requesting additional permissions if the app is breached

Additionally, Windows 11 includes device management support to simplify printer setup for users. With support from Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>, admins can now configure policy settings to provision specific printers onto the user's Windows devices.

Universal Print stores the print data in cloud securely in Office Storage, the same storage used by other Microsoft 365 products.

More information about handling of Microsoft 365 data (this includes Universal Print data) can be found [here][LINK-24].

The Universal Print secure release platform ensures user privacy, secures organizational data, and reduces print wastage. It eliminates the need for people to rush to a shared printer as soon as they send a print job to ensure that no one sees the private or confidential content. Sometimes, printed documents are picked up by another person or not picked up at all and discarded. Detailed support and configuration information can be found [here][LINK-25].

Universal Print supports Administrative Units in Microsoft Entra ID to enable the assignments of a *Printer Administrator* role to specific teams in the organization. The assigned team can configure only the printers that are part of the same Administrative Unit.

For customers who want to stay on print servers, we recommend using the Microsoft IPP Print driver. For features beyond what's covered in the standard IPP driver, use Print Support Applications (PSA) for Windows from the respective printer OEM.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Universal Print][LINK-26]
- [Data handling in Universal Print][LINK-27]
- [Delegate Printer Administration with Administrative Units][LINK-28]
- [Print support app design guide][LINK-29]

<!--links-->

[LINK-1]: /entra
[LINK-2]: https://www.microsoft.com/security/business/microsoft-entra-pricing
[LINK-3]: /entra/global-secure-access/concept-internet-access
[LINK-4]: /entra/global-secure-access/concept-private-access
[LINK-5]: /entra/architecture/sse-deployment-guide-internet-access
[LINK-6]: /entra/global-secure-access/how-to-install-windows-client
[LINK-7]: /entra/identity/devices/enterprise-state-roaming-enable
[LINK-8]: /azure/attestation/overview
[LINK-9]: /windows/client-management/mdm-overview
[LINK-10]: /windows/client-management/mdm/remotewipe-csp
[LINK-11]: /windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines
[LINK-12]: /mem/intune/fundamentals/what-is-intune
[LINK-13]: /mem/intune/enrollment/windows-enrollment-attestation
[LINK-14]: /mem/intune/protect/epm-overview?formCode=MG0AV3
[LINK-15]: /mem/intune/apps/protect-mam-windows?formCode=MG0AV3
[LINK-16]: /mem/intune/protect/security-baselines
[LINK-17]: /mem/intune/protect/security-baseline-settings-mdm-all
[LINK-18]: /windows-server/identity/laps/laps-overview
[LINK-19]: /autopilot/overview
[LINK-20]: /mem/autopilot/windows-autopilot-reset
[LINK-21]: /windows/deployment/update/waas-manage-updates-wufb
[LINK-22]: https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RW10vlw
[LINK-23]: /universal-print/fundamentals/universal-print-partner-integrations
[LINK-24]: /microsoft-365/enterprise/m365-dr-overview
[LINK-25]: /universal-print/fundamentals/universal-print-qrcode
[LINK-26]: https://www.microsoft.com/microsoft-365/windows/universal-print
[LINK-27]: /universal-print/data-handling
[LINK-28]: /universal-print/portal/delegated-admin
[LINK-29]: /windows-hardware/drivers/devapps/print-support-app-design-guide
