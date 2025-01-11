---
title: Hotpatch updates
description: Use Hotpatch updates to receive security updates without restarting your device
ms.date: 11/19/2024
ms.service: windows-client
ms.subservice: autopatch
ms.topic: how-to
ms.localizationpriority: medium
author: tiaraquan
ms.author: tiaraquan
manager: aaroncz
ms.reviewer: adnich
ms.collection:
  - highpri
  - tier1
---

# Hotpatch updates (public preview)

[!INCLUDE [windows-autopatch-applies-to-all-licenses](../includes/windows-autopatch-applies-to-all-licenses.md)]

> [!IMPORTANT]
> This feature is in public preview. It's being actively developed and might not be complete. They're made available on a "Preview" basis. You can test and use these features in production environments and scenarios and provide feedback.

Hotpatch updates are [Monthly B release security updates](/windows/deployment/update/release-cycle#monthly-security-update-release) that can be installed without requiring you to restart the device. Hotpatch updates are designed to reduce downtime and disruptions. By minimizing the need to restart, these updates help ensure faster compliance, making it easier for organizations to maintain security while keeping workflows uninterrupted.

## Key benefits

- Hotpatch updates streamline the installation process and enhance compliance efficiency.
- No changes are required to your existing update ring configurations. Your existing ring configurations are honored alongside Hotpatch policies.
- The [Hotpatch quality update report](../monitor/windows-autopatch-hotpatch-quality-update-report.md) provides a per policy level view of the current update statuses for all devices that receive Hotpatch updates.

## Operating system configuration prerequisites 

To prepare a device to receive Hotpatch updates, configure the following operating system settings on the device. You must configure these settings for the device to be offered the Hotpatch update and to apply all Hotpatch updates.

### Virtualization based security (VBS)

VBS must be turned on for a device to be offered Hotpatch updates. For information on how to set and detect if VBS is enabled, see [Virtualization-based Security (VBS)](/windows/security/hardware-security/enable-virtualization-based-protection-of-code-integrity?tabs=security).

### Arm 64 devices must disable compiled hybrid PE usage (CHPE) (Arm 64 CPU Only)

This requirement only applies to Arm 64 CPU devices when using Hotpatch updates. Hotpatch updates aren't compatible with servicing CHPE OS binaries located in the `%SystemRoot%\SyChpe32` folder. To ensure all the Hotpatch updates are applied, you must set the CHPE disable flag and restart the device to disable CHPE usage. You only need to set this flag one time. The registry setting remains applied through updates. To disable CHPE, set the following registry key:
Path: `**HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management**`
Key value: `**HotPatchRestrictions=1**`

> [!IMPORTANT]
> This setting is required because it forces the operating system to use the emulation x86-only binaries instead of CHPE binaries on Arm 64 devices. CHPE binaries include native Arm 64 code to improve performance, excluding the CHPE binaries might affect performance or compatibility. Be sure to test application compatibility and performance before rolling out Hotpatch updates widely on Arm 64 CPU based devices.

If you choose to no longer use Hotpatch updates, clear the CHPE disable flag (`HotPatchRestrictions=0`) then restart the device to turn on CHPE usage.  

## Eligible devices

To benefit from Hotpatch updates, devices must meet the following prerequisites:

- Operating System: Devices must be running Windows 11 24H2 or later.
- VBS (Virtualization-based security): VBS must be enabled to ensure secure installation of Hotpatch updates.
- Latest Baseline Release: Devices must be on the latest baseline release version to qualify for Hotpatch updates. Microsoft releases Baseline updates quarterly as standard cumulative updates. For more information on the latest schedule for these releases, see [Release notes for Hotpatch](https://support.microsoft.com/topic/release-notes-for-hotpatch-in-azure-automanage-for-windows-server-2022-4e234525-5bd5-4171-9886-b475dabe0ce8?preview=true).

## Ineligible devices

Devices that don't meet one or more prerequisites automatically receive the Latest Cumulative Update (LCU) instead. Latest Cumulative Update (LCU) contains monthly updates that supersede the previous month's updates containing both security and nonsecurity releases.  

LCUs requires you to restart the device, but the LCU ensures that the device remains fully secure and compliant.

> [!NOTE]
> If devices aren't eligible for Hotpatch updates, these devices are offered the LCU. The LCU keeps your configured Update ring settings, it doesn't change the settings.

## Release cycles

For more information about the release calendar for Hotpatch updates, see [Release notes for Hotpatch](https://support.microsoft.com/topic/release-notes-for-hotpatch-in-azure-automanage-for-windows-server-2022-4e234525-5bd5-4171-9886-b475dabe0ce8?preview=true).  

- Baseline Release Months: January, April, July, October
- Hotpatch Release Months: February, March, May, June, August, September, November, December

## Enroll devices to receive Hotpatch updates

> [!NOTE]
> If you're using Autopatch groups and want your devices to receive Hotpatch updates, you must create a Hotpatch policy and assign devices to it. Turning on Hotpatch updates doesn't change the deferral setting applied to devices within an Autopatch group.

**To enroll devices to receive Hotpatch updates:**

1. Go to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. Go to the **Quality updates** tab.
1. Select **Create**, and select **Windows quality update policy (preview)**.
1. Under the **Basics** section, enter a name for your new policy and select Next.
1. Under the **Settings** section, set **"When available, apply without restarting the device ("Hotpatch")** to **Allow**. Then, select **Next**.
1. Select the appropriate Scope tags or leave as Default and select **Next**.
1. Assign the devices to the policy and select **Next**.
1. Review the policy and select **Create**.

These steps ensure that targeted devices, which are [eligible](#eligible-devices) to receive Hotpatch updates, are configured properly. [Ineligible devices](#ineligible-devices) are offered the latest cumulative updates (LCU).

> [!NOTE]
> Turning on Hotpatch updates doesn't change the existing deadline-driven or scheduled install configurations on your managed devices. Deferral and active hour settings still apply.
