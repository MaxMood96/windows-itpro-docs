---
title: Updated Windows and Microsoft Copilot experience
description: Learn about changes to the Copilot in Windows experience for commercial environments and how to configure it for your organization.
ms.topic: overview
ms.subservice: windows-copilot
ms.date: 12/12/2024
ms.author: mstewart
author: mestew
ms.collection:
  - windows-copilot
  - magic-ai-copilot
appliesto:
- ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11, version 22H2 or later</a>
---

# Updated Windows and Microsoft Copilot experience
<!--8445848, 9294806-->

>**Looking for consumer information?** See [Welcome to Copilot in Windows](https://support.microsoft.com/topic/675708af-8c16-4675-afeb-85a5a476ccb0). **Looking for more information on Microsoft Copilot experiences?** See [Understanding the different Microsoft Copilot experiences](https://support.microsoft.com/topic/cfff4791-694a-4d90-9c9c-1eb3fb28e842).

## Enhanced data protection with enterprise data protection

The Copilot experience on Windows is changing to enhance data security, privacy, compliance, and simplify the user experience, for users signed in with a Microsoft Entra work or school account. [Microsoft Copilot will offer enterprise data protection](https://techcommunity.microsoft.com/t5/copilot-for-microsoft-365/updates-to-microsoft-copilot-to-bring-enterprise-data-protection/ba-p/4217152) at no additional cost and redirect users to a new simplified interface designed for work and education. [Enterprise data protection (EDP)](/copilot/microsoft-365/enterprise-data-protection) refers to controls and commitments, under the Data Protection Addendum and Product Terms, that apply to customer data for users of Copilot for Microsoft 365 and Microsoft Copilot. This means that security, privacy, compliance controls and commitments available for Copilot for Microsoft 365 will extend to Microsoft Copilot prompts and responses. Prompts and responses are protected by the same terms and commitments that are widely trusted by our customers - not only for Copilot for Microsoft 365, but also for emails in Exchange and files in SharePoint. This is an improvement on top of the previous commercial data protection (CDP) promise. This update is rolling out now. For more information, see the [Microsoft Copilot updates and enterprise data protection FAQ](/copilot/edpfaq).

> [!IMPORTANT]
> To streamline the user experience, updates to the Copilot entry points in Windows are being made for users. **Copilot in Windows (preview) will be removed from Windows**. The experience will slightly vary depending on whether your organization has already opted into using Copilot in Windows (preview) or not. 

## Copilot in Windows (preview) isn't enabled

If your organization hasn't enabled Copilot in Windows (preview), your existing preferences are respected. Neither the Microsoft Copilot app nor the Microsoft 365 app are pinned to the taskbar. To prepare for the eventual removal of the [Copilot in Windows policy](/windows/client-management/mdm/policy-csp-windowsai#turnoffwindowscopilot), admins should [set Microsoft Copilot pinning options](/copilot/microsoft-365/pin-copilot) in the Microsoft 365 admin center.

> [!NOTE]
> Although we won't be pinning any app to the taskbar by default, IT has the capability to use policies to enforce their preferred app pinning.

## Copilot in Windows (preview) is enabled

If you had previously activated Copilot in Windows (in preview) for your workforce, we want to thank you for your enthusiasm. To provide the best Copilot experience for your users moving forward, and support greater efficiency and productivity, we won't automatically pin the Microsoft 365 app to the taskbar in Windows. Rather, we ensure that you have control over how you enable the Copilot experience within your organization. Our focus remains on empowering IT to seamlessly manage AI experiences and adopt those experiences at a pace that suits your organizational needs.

If you have already activated Copilot in Windows (preview) - and want your users to have uninterrupted access to Copilot on the taskbar after the update - use the [configuration options](/windows/configuration/taskbar/?pivots=windows-11) to pin the Microsoft 365 app to the taskbar as Copilot in Windows (preview) icon will be removed from the taskbar.

## Users signing in to new PCs with Microsoft Entra accounts

For users signing in to new PCs with work or school accounts, the following experience occurs:

-	The Microsoft 365 app is pinned to the taskbar - this is the app comes preinstalled with Windows and includes convenient access to Office apps such as Word, PowerPoint, etc. 
-	Users that have the Microsoft 365 Copilot license have Microsoft Copilot pinned by default inside the Microsoft 365 app. 
-	Within the Microsoft 365 app, the Microsoft Copilot icon is situated next to the home button.
    - Microsoft Copilot (`web` grounding chat) isn't the same as Microsoft 365 Copilot (`web` and `work` scope), which is a separate add-on license. 
    - Microsoft Copilot is available at no additional cost to customers with a Microsoft Entra account. Microsoft Copilot is the entry point for Copilot at work. While the Copilot chat experience helps users ground their conversations in web data, Microsoft 365 Copilot allows users to incorporate both web and work data they have access to into their conversations by switching between work and web modes in Business Chat. 
   - For users with the Microsoft 365 Copilot license, they can toggle between the web grounding-based chat capabilities of Microsoft Copilot and the work scoped chat capabilities of Microsoft 365 Copilot. 
-	Customers that don't have a license for Microsoft 365 Copilot are asked if they want to pin Microsoft Copilot to ensure they have easy access to Copilot. To set the default behavior, admins should [set Microsoft Copilot pinning options](/copilot/microsoft-365/pin-copilot) in the Microsoft 365 admin center. 
-	If admins elect not to pin Copilot and indicate that users can be asked, users will be asked to pin it themselves in the Microsoft 365 app, Outlook, and Teams. 
-	If admins elect not to pin Microsoft Copilot and indicate that users can't be asked, Microsoft Copilot won't be available via the Microsoft 365 app, Outlook, or Teams. Users have access to Microsoft Copilot from <www.microsoft.com/copilot> unless that URL is blocked by the IT admin.
-	If the admins make no selection, users will be asked to pin Microsoft Copilot by themselves for easy access. 


## When will this happen?

The update to Microsoft Copilot to offer enterprise data protection is rolling out now.
The shift to the Microsoft 365 app as the entry point for Microsoft Copilot with enterprise data protection (EDP) is coming soon. Changes will be rolled out to managed PCs starting with the September 2024 optional nonsecurity preview release, and following with the October 2024 monthly security update for all supported versions of Windows 11. These changes will be applied to Windows 10 PCs the month after. This update is replacing the current Copilot in Windows experience.
 
The Microsoft Copilot app will be automatically enabled after you install the Windows updates listed above if you haven't previously enabled a group policy to prevent the installation of Copilot. The [AppLocker policy](/windows/security/application-security/application-control/app-control-for-business/applocker/applocker-overview) is available to control this Copilot experience before installing these Windows updates mentioned above or any subsequent Windows updates. 
 
Note that the Microsoft Copilot app doesn't support Microsoft Entra authentication and users trying to sing in to the app using a Microsoft Entra account will be redirected to https://copilot.cloud.microsoft/ in their default browser. For users authenticating with a Microsoft Entra account, they should access Copilot through the Microsoft 365 app as the entry point. We recommend you pin Copilot to the navigation bar of the Microsoft 365 app to enable easy access.


## Policy information for previous Copilot in Windows (preview) experience

Admins should configure the [pinning options](/copilot/microsoft-365/pin-copilot) to enable access to Microsoft Copilot within the Microsoft 365 app in the Microsoft 365 admin center. 

The following policy to manage Copilot in Windows (preview) will be removed in the future and is considered a legacy policy:


| &nbsp; | Setting  |
|---|---|
| **CSP** | ./User/Vendor/MSFT/Policy/Config/WindowsAI/[TurnOffWindowsCopilot](mdm/policy-csp-windowsai.md#turnoffwindowscopilot) |
| **Group policy** | User Configuration > Administrative Templates > Windows Components > Windows Copilot > **Turn off Windows Copilot** |

## Remove or prevent installation of the Copilot app

You can remove or uninstall the Copilot app from your device by using one of the following methods:

1. Enterprise users  can uninstall the Copilot app by going to **Settings** > **Apps** >**Installed Apps**. Select the three dots appearing on the right side of the app and select **Uninstall** from the dropdown list.

1. If you are an IT administrator, you can prevent installation of the app or remove the Copilot app using one of the following methods:
   1. Prevent installation of the Copilot app:
     - Configure [AppLocker policy](/windows/security/application-security/application-control/app-control-for-business/applocker/applocker-overview) before installing Windows update. AppLocker helps you control which apps and files users can run. Note: AppLocker policy should be used instead of the [Turn Off Windows Copilot](mdm/policy-csp-windowsai.md#turnoffwindowscopilot) legacy policy setting and its MDM equivalent, [TurnOffWindowsCopilot](mdm/policy-csp-windowsai.md#turnoffwindowscopilot). The policy is subject to near-term deprecation. 
     - The Applocker policy can be configured by following one of the methods listed in [Edit an AppLocker policy](/windows/security/application-security/application-control/app-control-for-business/applocker/edit-an-applocker-policy) and adding the below text to the policy:
     </br>**Publisher**: CN=MICROSOFT CORPORATION, O=MICROSOFT CORPORATION, L=REDMOND, S=WASHINGTON, C=US
     </br> **Package name**: MICROSOFT.COPILOT
    </br> **Package version**: * (and above)

   1. Remove the Copilot app using PowerShell script:
      1. Open a Windows PowerShell window. You can do this by opening the Start menu, typing `PowerShell`, and selecting **Windows PowerShell** from the results.
      1. Once the PowerShell window is open, enter the following commands:
       ```powershell
       # Get the package full name of the Microsoft Copilot app
       $packageFullName = Get-AppxPackage -Name "Microsoft.Copilot" | Select-Object -ExpandProperty PackageFullName
       # Remove the Microsoft Copilot app
       Remove-AppxPackage -Package $packageFullName
       ```


## Implications for the Copilot hardware key
<!--9598546-->
The Microsoft Copilot app is now available only to consumer users authenticating with a Microsoft account and won't work for commercial users authenticating with a Microsoft Entra account. With this change, IT admins need to take steps to ensure users authenticating with a Microsoft Entra account can still access Copilot with the Copilot key. Users attempting to sign in to the Copilot app with their Microsoft Entra account will be redirected to the browser version of Microsoft Copilot with enterprise data protection (https://copilot.cloud.microsoft). 

For the optimal experience, enterprise customers should go to Windows client policies, such as Group Policy or Configuration Service Provider (CSP) policies to update the target of the key to the Microsoft 365 app so that users can access Copilot within the Microsoft 365 app. End users can also configure this from the **Settings** page. 

The Microsoft 365 app comes preinstalled on all Windows 11 PCs. If your organization uninstalled the Microsoft 365 app, we suggest you reinstall it from the Microsoft Store or your preferred application management solution so that the Copilot key can be remapped to the Microsoft 365 app. We also suggest you [Pin Microsoft Copilot](/copilot/microsoft-365/pin-copilot) to the navigation bar of the Microsoft 365 app. 

To avoid confusion for users as to which entry point for Microsoft Copilot to use, we recommend you uninstall the Copilot app.

Use the table below to help determine the experience for your managed organization:

| Configuration | Copilot experience | Copilot key invokes |
| ---| --- | --- |
| Copilot **not enabled** in environment | Neither Copilot in Windows (preview) nor the Microsoft Copilot app are present. | Windows Search |
| Copilot **enabled** + **do not authenticate** with Microsoft Entra | Copilot in Windows (preview) is removed and replaced by the Microsoft Copilot app, which is not pinned to the taskbar unless you elect to do so. | Microsoft Copilot app | 
| Copilot **enabled** + **authenticate** with Microsoft Entra + **new device** |  Copilot in Windows (preview) is not present. Microsoft Copilot is accessed through the Microsoft 365 app (after post-setup update). | Microsoft Copilot within the Microsoft 365 app (after post-setup update). |
|  Copilot **enabled** + **authenticate** with Microsoft Entra + **existing device** | Copilot in Windows (preview) is removed. Existing users with Copilot enabled on their devices will still see the Microsoft Copilot app. | IT admins should use policy to remap the Copilot key to the Microsoft 365 app, or prompt users to choose. |


## Policies to manage the Copilot key

Policies are available to configure the target app of the Copilot hardware key. For more information, see [WindowsAI Policy CSP](mdm/policy-csp-windowsai.md). 

To configure the Copilot key, use the following policy:

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetCopilotHardwareKey](mdm/policy-csp-windowsai.md#setcopilothardwarekey) |
| **Group policy** | User Configuration > Administrative Templates > Windows Components > Windows Copilot > **Set Copilot Hardware Key** |


## End user settings for the Copilot key

If you choose to provide users in your organization with the choice to manage their own experience, a protocol to launch the **Settings** app remap the Copilot key is available. The following can be used by apps and scripts to bring the user to the setting so they can modify it to meet their needs:

`ms-settings:personalization-textinput-copilot-hardwarekey`

:::image type="content" border="true" source="./images/9598546-copilot-key-settings.png" alt-text="Screenshot of the text input page in Settings." lightbox="./images/9598546-copilot-key-settings.png":::



If a user signed in with their Microsoft Entra account doesn't already have the key mapped to the Microsoft 365 app, they can select the app by going to **Settings** > **Personalization** > **Text input**, then selecting from the dropdown menu in the setting called **Customize Copilot key on keyboard**. This dropdown has options for: **Search**, **Custom**, or a currently mapped app if one is selected.

To map the key to the Microsoft 365 app, the user should select **Custom** and then choose the Microsoft 365 app from the app picker. If this app picker is empty or doesn't include the Microsoft 365 app, they should reinstall it from the Microsoft Store. 

Users can also choose to have the Copilot key launch an app that is MSIX packaged and signed, ensuring the app options the Copilot key can remap to meet security and privacy requirements.   


## Copilot installation with Windows updates and controls

If you're an IT administrator and have enabled group policies to prevent the installation of Copilot, the Copilot app won't be installed on the configured devices. If you haven't enabled a group policy, you can remove the Copilot app by following one of the steps in the [Remove or prevent installation of the Copilot app](#remove-or-prevent-installation-of-the-copilot-app) section or configure the [AppLocker policy](/windows/security/application-security/application-control/app-control-for-business/applocker/applocker-overview) before installing Windows updates. When the AppLocker policy for Copilot is enabled, it will:

- Prevent the app from being installed if it isn't already on the device.
- Block the app from being launched if it's already installed.