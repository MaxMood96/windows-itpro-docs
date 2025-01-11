---
title: NewsAndInterests Policy CSP
description: Learn more about the NewsAndInterests Area in Policy CSP.
ms.date: 11/27/2024
---

<!-- Auto-Generated CSP Document -->

<!-- NewsAndInterests-Begin -->
# Policy CSP - NewsAndInterests

[!INCLUDE [Windows Insider tip](includes/mdm-insider-csp-note.md)]

<!-- NewsAndInterests-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
<!-- NewsAndInterests-Editable-End -->

<!-- AllowNewsAndInterests-Begin -->
## AllowNewsAndInterests

<!-- AllowNewsAndInterests-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ❌ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ Windows SE <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows 11, version 21H2 [10.0.22000] and later |
<!-- AllowNewsAndInterests-Applicability-End -->

<!-- AllowNewsAndInterests-OmaUri-Begin -->
```Device
./Device/Vendor/MSFT/Policy/Config/NewsAndInterests/AllowNewsAndInterests
```
<!-- AllowNewsAndInterests-OmaUri-End -->

<!-- AllowNewsAndInterests-Description-Begin -->
<!-- Description-Source-ADMX -->
This policy specifies whether the widgets feature is allowed on the device.

Widgets will be turned on by default unless you change this in your settings.

If you turned this feature on before, it will stay on automatically unless you turn it off.
<!-- AllowNewsAndInterests-Description-End -->

<!-- AllowNewsAndInterests-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->

This policy applies to the entire widgets experience, including content on the taskbar.
<!-- AllowNewsAndInterests-Editable-End -->

<!-- AllowNewsAndInterests-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `int` |
| Access Type | Add, Delete, Get, Replace |
| Default Value  | 1 |
<!-- AllowNewsAndInterests-DFProperties-End -->

<!-- AllowNewsAndInterests-AllowedValues-Begin -->
**Allowed values**:

| Value | Description |
|:--|:--|
| 0 | Not allowed. |
| 1 (Default) | Allowed. |
<!-- AllowNewsAndInterests-AllowedValues-End -->

<!-- AllowNewsAndInterests-GpMapping-Begin -->
**Group policy mapping**:

| Name | Value |
|:--|:--|
| Name | AllowNewsAndInterests |
| Friendly Name | Allow widgets |
| Location | Computer Configuration |
| Path | Windows Components > Widgets |
| Registry Key Name | SOFTWARE\Policies\Microsoft\Dsh |
| Registry Value Name | AllowNewsAndInterests |
| ADMX File Name | NewsAndInterests.admx |
<!-- AllowNewsAndInterests-GpMapping-End -->

<!-- AllowNewsAndInterests-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
<!-- AllowNewsAndInterests-Examples-End -->

<!-- AllowNewsAndInterests-End -->

<!-- DisableWidgetsOnLockScreen-Begin -->
## DisableWidgetsOnLockScreen

<!-- DisableWidgetsOnLockScreen-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ❌ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ Windows SE <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows Insider Preview |
<!-- DisableWidgetsOnLockScreen-Applicability-End -->

<!-- DisableWidgetsOnLockScreen-OmaUri-Begin -->
```Device
./Device/Vendor/MSFT/Policy/Config/NewsAndInterests/DisableWidgetsOnLockScreen
```
<!-- DisableWidgetsOnLockScreen-OmaUri-End -->

<!-- DisableWidgetsOnLockScreen-Description-Begin -->
<!-- Description-Source-DDF -->
Disable widgets on lock screen.
<!-- DisableWidgetsOnLockScreen-Description-End -->

<!-- DisableWidgetsOnLockScreen-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
<!-- DisableWidgetsOnLockScreen-Editable-End -->

<!-- DisableWidgetsOnLockScreen-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `int` |
| Access Type | Add, Delete, Get, Replace |
| Default Value  | 0 |
<!-- DisableWidgetsOnLockScreen-DFProperties-End -->

<!-- DisableWidgetsOnLockScreen-AllowedValues-Begin -->
**Allowed values**:

| Value | Description |
|:--|:--|
| 0 (Default) | Enabled. |
| 1 | Disabled. |
<!-- DisableWidgetsOnLockScreen-AllowedValues-End -->

<!-- DisableWidgetsOnLockScreen-GpMapping-Begin -->
**Group policy mapping**:

| Name | Value |
|:--|:--|
| Name | DisableWidgetsOnLockScreen |
| Path | NewsAndInterests > AT > WindowsComponents > NewsAndInterests |
<!-- DisableWidgetsOnLockScreen-GpMapping-End -->

<!-- DisableWidgetsOnLockScreen-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
<!-- DisableWidgetsOnLockScreen-Examples-End -->

<!-- DisableWidgetsOnLockScreen-End -->

<!-- NewsAndInterests-CspMoreInfo-Begin -->
<!-- Add any additional information about this CSP here. Anything outside this section will get overwritten. -->
<!-- NewsAndInterests-CspMoreInfo-End -->

<!-- NewsAndInterests-End -->

## Related articles

[Policy configuration service provider](policy-configuration-service-provider.md)
