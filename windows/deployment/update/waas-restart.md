---
title: Manage device restarts after updates
description: Use group policy settings, mobile device management (MDM), or registry to configure when devices will restart after a Windows update is installed.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: aaroncz
ms.collection:
  - highpri
  - tier2
ms.localizationpriority: medium
appliesto:
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
ms.date: 10/25/2024
---

# Manage device restarts after updates

> **Looking for consumer information?** See [Windows Update: FAQ](https://support.microsoft.com/windows/windows-update-faq-8a903416-6f45-0718-f5c7-375e92dddeb2)

You can use group policy settings, mobile device management (MDM), or the Windows registry to configure when devices will restart after a Windows update is installed. You can schedule update installation and set policies for restart, configure active hours for when restarts shouldn't occur, or you can do both.

> [!NOTE]
> Directly editing the Windows registry isn't recommended.

## Schedule update installation

In group policy, within **Configure Automatic Updates**, you can configure a forced restart after a specified installation time.

To set the time, go to **Configure Automatic Updates**, select option **4 - Auto download and schedule the install**, and then use **Scheduled install time** to enter a time. Alternatively, you can specify that installation occurs during the automatic maintenance time. To configure this alternative method, use **Computer Configuration\Administrative Templates\Windows Components\Maintenance Scheduler**.

The setting to **Always automatically restart at the scheduled time** forces a restart after the specified installation time. It lets you configure a timer to warn a signed-in user that a restart is going to occur.

While not recommended, you can achieve the same result with the Windows registry. Under `HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate\AU`, set `AuOptions` to `4` and set the install time with `ScheduledInstallTime`. Enable `AlwaysAutoRebootAtScheduledTime` and specify the delay in minutes through `AlwaysAutoRebootAtScheduledTimeMinutes`. Similar to group policy, `AlwaysAutoRebootAtScheduledTimeMinutes` sets the timer to warn a signed-in user that a restart is going to occur.

For a detailed description of these registry keys, see [Registry keys used to manage restart](#registry-keys-used-to-manage-restart).

## Delay automatic restart

When you enable **Configure Automatic Updates** in group policy, you can also enable one of the following policies to delay an automatic restart after update installation:

- **Turn off auto-restart for updates during active hours** prevents automatic restart during active hours.

- **No auto-restart with logged on users for scheduled automatic updates installations** prevents automatic restart when a user is signed in. If a user schedules the restart in the update notification, the device restarts at the time the user specifies even if a user is signed in at the time. This policy only applies when **Configure Automatic Updates** is set to option **4 - Auto download and schedule the install**.

> [!NOTE]
> When using Remote Desktop Protocol (RDP) connections, only active RDP sessions are considered signed-in users. Devices that don't have locally signed-in users, or active RDP sessions, are restarted.

You can also use the Windows registry, to prevent automatic restarts when a user is signed in. Under `HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate\AU`, set `AuOptions` to `4` and enable `NoAutoRebootWithLoggedOnUsers`. As with group policy, if a user schedules the restart in the update notification, it overrides this setting.

For a detailed description of these registry keys, see [Registry keys used to manage restart](#registry-keys-used-to-manage-restart).

## Configure active hours

*Active hours* identify the period of time when you expect the device to be in use. Automatic restarts after an update occur outside of the active hours.

By default, active hours are from 8 AM to 5 PM on PCs. Users can manually change the active hours.

You can also specify the max active hours range. The specified range is counted from the active hours start time.

### Configure active hours with group policy

To configure active hours using group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and open the **Turn off auto-restart for updates during active hours** policy setting. When the policy is enabled, you can set the start and end times for active hours.

:::image type="content" source="images/waas-active-hours-policy.png" alt-text="A screenshot of the group policy setting to 'Turn off auto-restart for updates during active hours' set to Enabled and the default active hours specified." lightbox="images/waas-active-hours-policy.png":::

### Configure active hours with MDM

To configure active hours, MDM uses the following settings in the [Update Policy CSP](/windows/client-management/mdm/policy-csp-update):

- [ActiveHoursStart](/windows/client-management/mdm/policy-csp-update#activehoursstart)
- [ActiveHoursEnd](/windows/client-management/mdm/policy-csp-update#activehoursend)
- [ActiveHoursMaxRange](/windows/client-management/mdm/policy-csp-update#activehoursmaxrange)

### Configure active hours through the Windows registry

This method isn't recommended, and should only be used when you can't use group policy or MDM. Any settings configured through the registry might conflict with any existing configuration that uses any of the other methods.

Configure active hours by setting a combination of the following registry values:

Under `HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate` use `SetActiveHours` to enable or disable active hours and `ActiveHoursStart` and `ActiveHoursEnd` to specify the range of active hours.

For a detailed description of these registry keys, see [Registry keys used to manage restart](#registry-keys-used-to-manage-restart).

> [!TIP]
> To manually configure active hours on a device, go to **Settings** > **Windows Update** > **Advanced options** and select **Active hours**.

### Configure active hours maximum range

You can specify the maximum active hours range that users can set. This option gives you flexibility to leave some of the decision for active hours on the user's side, while making sure you allow enough time for updates to install. The maximum range is calculated from the active hours start time.

To configure the maximum range for active hours through group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and open the setting to **Specify active hours range for auto-restarts**.

To configure the maximum range for active hours through MDM, use [ActiveHoursMaxRange](/windows/client-management/mdm/policy-csp-update#activehoursmaxrange).

## Limit restart delays

After Windows installs an update, it attempts to automatically restart outside of active hours. If the restart doesn't succeed after a default period of seven days, the user sees a notification that a restart is required. To change the delay, use the setting to **Specify deadline before auto-restart for update installation**. The minimum value is two days and the maximum value is two weeks (14 days).

## Control restart notifications

### Display options for update notifications

You can define which Windows Update notifications are displayed to the user. This policy doesn't control how and when updates are downloaded and installed.

To configure this behavior through group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and select the policy for **Display options for update notifications**. Configure the following values:

- `0` (default): Use the default Windows Update notifications.
- `1`: Turn off most notifications but keep restart warnings.
- `2`: Turn off all notifications including restart warnings.

To configure this behavior through MDM, use [UpdateNotificationLevel](/windows/client-management/mdm/policy-csp-update#updatenotificationlevel).

Starting in Windows 11, version 22H2, **Apply only during active hours** was added as another option for **Display options for update notifications**. When you select **Apply only during active hours**, the notifications are only disabled during active hours when you use options `1` or `2`. To ensure that the device stays updated, a notification is still shown during active hours if you select **Apply only during active hours**, and once a deadline is reached when you configure [Specify deadlines for automatic updates and restarts](wufb-compliancedeadlines.md). <!--6286260-->

To configure this behavior through MDM, use [UpdateNotificationLevel](/windows/client-management/mdm/policy-csp-update#updatenotificationlevel).

### Automatic restart notifications

You can override the default behavior for the automatic restart required notification. By default, this notification dismisses automatically.

- To configure this behavior through group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and select the policy to **Configure auto-restart required notification for updates**. When configured to **2 - User Action**, a user that gets this notification must manually dismiss it.

- To configure this behavior through MDM, use [AutoRestartRequiredNotificationDismissal](/windows/client-management/mdm/policy-csp-update#autorestartrequirednotificationdismissal).

You can also configure the period before an update that this notification shows up. The default value is 15 minutes.

- To change it through group policy, select **Configure auto-restart-reminder notifications for updates** under **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and select the period in minutes.

- To change it through MDM, use [AutoRestartNotificationSchedule](/windows/client-management/mdm/policy-csp-update#autorestartnotificationschedule).

In some cases, you don't need a notification to show up.

- To do so through group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and select the setting to **Turn off auto-restart notifications for update installations**.

- To do so through MDM, use [SetAutoRestartNotificationDisable](/windows/client-management/mdm/policy-csp-update#setautorestartnotificationdisable).

### Scheduled automatic restart warnings

Since users aren't able to postpone a scheduled restart once the deadline is reached, you can configure a warning reminder before the scheduled restart. You can also configure a warning before the restart, to notify users once the restart is imminent and allow them to save their work.

To configure both through group policy, find the setting to **Configure auto-restart warning notifications schedule for updates** under **Computer Configuration\Administrative Templates\Windows Components\Windows Update**. The warning reminder can be configured by **Reminder (hours)** and the warning before an imminent automatic restart can be configured by **Warning (mins)**.

In MDM, to configure the warning reminder, use [ScheduleRestartWarning](/windows/client-management/mdm/policy-csp-update#schedulerestartwarning). To configure the automatic restart imminent warning, use [ScheduleImminentRestartWarning](/windows/client-management/mdm/policy-csp-update#scheduleimminentrestartwarning).

### Engaged restart

Engaged restart is the period of time when users are required to schedule a restart. Initially, Windows auto-restarts outside of working hours. Once the default seven day period ends, Windows transitions to user scheduled restarts.

You can adjust the following settings for engaged restart:

- Period of time before automatic restart transitions to engaged restart.

- The number of days that users can snooze engaged restart reminder notifications.

- The number of days before a pending restart automatically executes outside of working hours.

In group policy, go to **Computer Configuration\Administrative Templates\Windows Components\Windows Update** and use the setting to **Specify engaged restart transition and notification schedule for updates**.

In MDM, use the following policies:

- [EngagedRestartTransitionSchedule](/windows/client-management/mdm/policy-csp-update#engagedrestarttransitionschedule)
- [EngagedRestartSnoozeSchedule](/windows/client-management/mdm/policy-csp-update#engagedrestartsnoozeschedule)
- [EngagedRestartDeadline](/windows/client-management/mdm/policy-csp-update#engagedrestartdeadline)

## Group policy settings for restart

In the group policy editor, the policy settings for restart behavior are in **Computer Configuration\Administrative Templates\Windows Components\Windows Update**. The following table shows which policies apply to Windows 10.

| Policy | Applies to Windows 10 | Notes |
| --- | --- | --- |
| Turn off auto-restart for updates during active hours | Yes | Use this policy to configure active hours, during which the device won't restart. This policy has no effect if the **No auto-restart with logged on users for scheduled automatic updates installations** or **Always automatically restart at the scheduled time** policies are enabled.  |
| Always automatically restart at the scheduled time | Yes | Use this policy to configure a restart timer (between 15 and 180 minutes) that will start immediately after Windows Update installs important updates. This policy has no effect if the **No auto-restart with logged on users for scheduled automatic updates installations** policy is enabled. |
| Specify deadline before auto-restart for update installation | Yes | Use this policy to specify how many days (between 2 and 14) an automatic restart can be delayed. This policy has no effect if the **No auto-restart with logged on users for scheduled automatic updates installations** or **Always automatically restart at the scheduled time** policies are enabled.  |
| No auto-restart with logged on users for scheduled automatic updates installations | Yes | Use this policy to prevent automatic restart when a user is logged on. This policy applies only when you configure the policy to **Configure Automatic Updates** to schedule the installation. |
| Re-prompt for restart with scheduled installations | No |   |
| Delay Restart for scheduled installations | No |   |
| Reschedule Automatic Updates scheduled installations | No |   |

> [!NOTE]
>
> - You can only choose one path for restart behavior.
> - If you set conflicting restart policies, the actual restart behavior may not be what you expected.
> - When using RDP, only active RDP sessions are considered as signed-in users.

## Registry keys used to manage restart

The following tables list registry values that correspond to the group policy settings for controlling restarts after updates in Windows 10.

### `HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate`

| Registry key | Key type | Value |
| --- | --- | --- |
| `ActiveHoursEnd` | `REG_DWORD` | `0-23`: Set active hours to end at a specific hour. </br>It starts with 12 AM (`0`) and ends with 11 PM (`23`). |
| `ActiveHoursStart` | `REG_DWORD` | `0-23`: Set active hours to start at a specific hour. </br>It starts with 12 AM (`0`) and ends with 11 PM (`23`.) |
| `SetActiveHours` | `REG_DWORD` | `0`: Disable automatic restart after updates outside of active hours. </br>`1`: Enable automatic restart after updates outside of active hours. |

### `HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate\AU`

| Registry key | Key type | Value |
| --- | --- | --- |
| `AlwaysAutoRebootAtScheduledTime` | `REG_DWORD` | `0`: Disable automatic restart after update installation at the scheduled time. </br>`1`: Enable automatic restart after update installation at a scheduled time. |
| `AlwaysAutoRebootAtScheduledTimeMinutes` | `REG_DWORD` | `15-180`: Set automatic restart to occur after the specified number of minutes. |
| `AUOptions` | `REG_DWORD` | `2`: Notify for download and notify for installation of updates. </br>`3`: Automatically download and notify for installation of updates. </br>`4`: Automatically download and schedule installation of updates. </br>`5`: Allow the local administrator to configure these settings. </br>**Note:** To configure restart behavior, set this value to `4`. |
| `NoAutoRebootWithLoggedOnUsers` | `REG_DWORD` | `0`: If users are signed in, automatically restart ("disable don't reboot"). </br>`1`: If a user is signed in, don't restart after an update installation. </br>**Note:** If disabled (`0`), Automatic Updates notifies the user that the computer is scheduled to automatically restart in five minutes to complete the installation. |
| `ScheduledInstallTime` | `REG_DWORD` | `0-23`: Schedule update installation time to a specific hour. </br>It starts with 12 AM (`0`) and ends with 11 PM (`23`). |

There are three different registry combinations for controlling restart behavior:

- To set active hours:
  - `SetActiveHours` should be `1`.
  - Then to define the time range, use `ActiveHoursStart` and `ActiveHoursEnd`.

- To schedule a specific installation and restart time:
  - `AUOptions` should be `4`.
  - `ScheduledInstallTime` should specify the installation time.
  - Set `AlwaysAutoRebootAtScheduledTime` to `1`.
  - `AlwaysAutoRebootAtScheduledTimeMinutes` should specify the number of minutes to wait before restarting.

- To delay restarting if a user is signed in:
  - `AUOptions` should be `4`.
  - Set `NoAutoRebootWithLoggedOnUsers` to `1`.

## More resources

- [Overview of Windows as a service](waas-overview.md)
- [Configure Delivery Optimization for Windows updates](../do/waas-delivery-optimization.md)
- [Configure Windows Update for Business](waas-configure-wufb.md)
- [Walkthrough: use group policy to configure Windows Update for Business](waas-wufb-group-policy.md)
- [Manage Windows software updates in Microsoft Intune](/mem/intune/protect/windows-update-for-business-configure)
