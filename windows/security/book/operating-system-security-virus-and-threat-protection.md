---
title: Windows 11 security book - Virus and threat protection
description: Operating System security chapter - Virus and threat protection.
ms.topic: overview
ms.date: 11/18/2024
---

# Virus and threat protection in Windows 11

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

Today's threat landscape is more complex than ever. This new world requires a new approach to threat prevention, detection, and response. Microsoft Defender Antivirus, along with many other features that are built into Windows 11, is at the frontlines, protecting customers against current and emerging threats.

## Microsoft Defender SmartScreen

Microsoft Defender SmartScreen protects against phishing, malware websites and applications, and the downloading of potentially malicious files.

SmartScreen determines whether a site is potentially malicious by:

- Analyzing visited webpages to find indications of suspicious behavior. If it determines a page is suspicious, it will show a warning page advising caution
- Checking the visited sites against a dynamic list of reported phishing sites and malicious software sites. If it finds a match, SmartScreen warns that the site might be malicious

SmartScreen also determines whether a downloaded app or app installer is potentially malicious by:

- Checking downloaded files against a list of reported malicious software sites and programs known to be unsafe. If it finds a match, SmartScreen warns that the file might be malicious
- Checking downloaded files against a list of well-known files. If the file is of a dangerous type and not well-known, SmartScreen displays a caution alert

With enhanced phishing protection in Windows 11, SmartScreen also alerts people when they're entering their Microsoft credentials into a potentially risky location, regardless of which application or browser is used. IT can customize which notifications appear through Microsoft Intune<sup>[\[4\]](conclusion.md#footnote4)</sup>. This protection runs in audit mode by default, giving IT admins full control to make decisions around policy creation and enforcement.

Because Windows 11 comes with these enhancements already built in and enabled, users have extra security from the moment they turn on their device.

The app and browser control section contains information and settings for Microsoft Defender SmartScreen. IT administrators and IT pros can get configuration guidance in the [Microsoft Defender SmartScreen documentation library](/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/).

## Network protection

While Microsoft Defender Smartscreen works with Microsoft Edge, for third-party browsers and processes, Windows 11 has Network protection that protects against phishing scams, malware websites, and the downloading of potentially malicious files.

When using Network Protection with Microsoft Defender for Endpoint, you'll be able to use Indicators of Compromise to block specific URL's and/or ip addresses.
Also integrates with Microsoft Defender for Cloud Apps to block unsactioned web apps in your organization.  Allow or block access to websites based on category with Microsoft Defender for Endpoint's Web Content Filtering.

[Network Protection library](/defender-endpoint/network-protection)
[Web protection library](/defender-endpoint/web-protection-overview)

## Tamper protection

Attacks like ransomware attempt to disable security features, such as anti-virus protection. Bad actors like to disable security features to get easier access to user's data, to install malware, or otherwise exploit user's data, identity, and devices without fear of being blocked. Tamper protection helps prevent these kinds of activities.

With tamper protection, malware is prevented from taking actions such as:

- Disabling real-time protection
- Turning off behavior monitoring
- Disabling antivirus protection, such as Scan all downloaded files and attachments (IOfficeAntivirus (IOAV))
- Disabling cloud-delivered protection
- Removing security intelligence updates
- Disabling automatic actions on detected threats
- Disabling archived files
- Altering exclusions
- Disabling notifications in the Windows Security app

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Tamper protection](/defender-endpoint/prevent-changes-to-security-settings-with-tamper-protection)

## Microsoft Defender Antivirus

Microsoft Defender Antivirus is a next-generation protection solution included in all versions of Windows 10 and Windows 11. From the moment you turn on Windows, Microsoft Defender Antivirus continually monitors for malware, viruses, and security threats. In addition to real-time protection, updates are downloaded automatically to help keep your device safe and protect it from threats. If you have another antivirus app installed and turned on, Microsoft Defender Antivirus turns off automatically. If you uninstall the other app, Microsoft Defender Antivirus turns back on.

Microsoft Defender Antivirus includes real-time, behavior-based, and heuristic antivirus protection. This combination of always-on content scanning, file and process behavior monitoring, and other heuristics effectively prevents security threats. Microsoft Defender Antivirus continually scans for malware and threats and also detects and blocks potentially unwanted applications (PUA), applications deemed to negatively impact your device but aren't considered malware.

Microsoft Defender Antivirus always-on protection is integrated with cloud-delivered protection, which helps ensure near-instant detection and blocking of new and emerging threats. This combination of local and cloud-delivered technologies including advanced memory scanning, behavior monitoring, and machine learning, provides award-winning protection at home and at work.

:::image type="content" source="images/defender-antivirus.png" alt-text="Diagram of the Microsoft Defender Antivirus components." border="false":::

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft Defender Antivirus in Windows Overview](/defender-endpoint/microsoft-defender-antivirus-windows).

## Attack surface reduction rules

Attack surface reduction rules help prevent actions and applications or scripts that are often abused to compromise devices and networks. By controlling when and how executables and/or script can run, thereby reducing the attack surface, you can reduce the overall vulnerability of your organization. Administrators can configure specific attack surface reduction rules to help block certain behaviors, such as:

- Launching executable files and scripts that attempt to download or run files
- Running obfuscated or otherwise suspicious scripts
- Performing behaviors that apps don't usually initiate during normal day-to-day work

For example, an attacker might try to run an unsigned script from a USB drive or have a macro in an Office document make calls directly to the Win32 API. Attack surface reduction rules can constrain these kinds of risky behaviors and improve the defensive posture of the device. For comprehensive protection, follow steps for enabling hardware-based isolation

For Microsoft Edge and reducing the attack surface across applications, folders, device,
network, and firewall.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Attack surface reduction](/defender-endpoint/overview-attack-surface-reduction)

## Controlled folder access

You can protect your valuable information in specific folders by managing app access to them. Only trusted apps can access protected folders, which are specified when controlled folder access is configured. Typically, commonly used folders, such as those used for documents, pictures, and downloads, are included in the list of controlled folders.

Controlled folder access works with a list of trusted apps. Apps that are included in the list of trusted software work as expected. Apps that aren't included in the trusted list are prevented from making any changes to files inside protected folders.

Controlled folder access helps protect user's valuable data from malicious apps and threats such as ransomware.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Controlled folder access](/defender-endpoint/controlled-folders)

## Exploit Protection

Exploit Protection automatically applies several exploit mitigation techniques to operating system processes and apps. Exploit Protection works best with Microsoft Defender for Endpoint<sup>[\[4\]](conclusion.md#footnote4)</sup>, which gives organizations detailed reporting into Exploit Protection events and blocks as part of typical alert investigation scenarios. You can enable Exploit Protection on an individual device and then use policy settings to distribute the configuration XML file to multiple devices simultaneously.

When a mitigation is encountered on the device, a notification will be displayed from the Action Center. You can customize the notification with your company details and contact information. You can also enable the rules individually to customize which techniques the feature monitors.

You can use audit mode to evaluate how Exploit Protection would impact your organization if it were enabled. And go through safe deployment practices (SDP).

Windows 11 provides configuration options for Exploit Protection. You can prevent users from modifying these specific options with device management solutions like Microsoft Intune or group policy.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Protecting devices from exploits](/defender-endpoint/enable-exploit-protection)