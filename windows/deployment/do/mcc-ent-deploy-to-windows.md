---
title: Deploy Microsoft Connected Cache software to a Windows host machine
description: Details on how to deploy Microsoft Connected Cache for Enterprise and Education cache software to a Windows host machine.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 10/30/2024
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Deploy Microsoft Connected Cache caching software to a Windows host machine

This article describes how to deploy Microsoft Connected Cache for Enterprise and Education caching software to a Windows host machine.

Deploying Connected Cache to a Windows host machine requires designating a [Group Managed Service Account (gMSA)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts) or a [local user account](https://support.microsoft.com/topic/20de74e0-ac7f-3502-a866-32915af2a34d) as the Connected Cache runtime account. This prevents tampering with the Connected Cache container and the cached content on the host machine.

Before deploying Connected Cache to a Windows host machine, ensure that the host machine meets all [requirements](mcc-ent-prerequisites.md), and that you have [created and configured your Connected Cache Azure resource](mcc-ent-create-resource-and-cache.md).

## Steps to deploy Connected Cache node to Windows

# [Azure portal](#tab/portal)

1. Within the Azure portal, navigate to the **Provisioning** tab of your cache node and copy the provisioning command.
1. Download the provisioning package using the option at the top of the Cache Node Configuration page and extract the archive onto the host machine.

   >[!Note]
   >* The provisioning package should be extracted to a directory that isn't synced to OneDrive, as the sychronization process will interfere with the installation. It is recommended to extract the provisioning package to the root directory of the host machine (e.g. C:\mccInstaller)

1. Open a PowerShell window *as administrator* on the host machine, then change directory to the extracted provisioning package.

   >[!Note]
   >* If you are deploying your cache node to a Windows host machine that uses a TLS-inspecting proxy (e.g. ZScaler), ensure that you've [configured the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in the extracted provisioning package directory and add `-proxyTlsCertificatePemFileName "mycert.pem"` to the provisioning command.

1. Set the Execution Policy to *Unrestricted* to allow the provisioning scripts to run.
1. Create a `$User` PowerShell variable containing the username of the account you intend to designate as the Connected Cache runtime account.

    For gMSAs, the `$User` PowerShell variable should be formatted as `"Domain\Username$"`. For local user accounts, `$User` PowerShell variable should be formatted as `"LocalMachineName\Username"`.

   If you're using a local user account as the Connected Cache runtime account, you'll also need to create a [PSCredential Object](/dotnet/api/system.management.automation.pscredential) named `$myLocalAccountCredential`.

   >[!Note]
   >* You'll need to apply a local security policy to permit the local user account to `Log on as a batch job`.

1. Run the provisioning command on the host machine.

# [Azure CLI](#tab/cli)

To deploy a cache node programmatically, you'll need to use Azure CLI to get the cache node's provisioning details and then run the provisioning command on the host machine.

1. To get the cache node's provisioning details, use `az mcc ent node get-provisioning-details`.

   ```azurecli-interactive
   az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
   ```

1. Save the resulting output. These values will be passed as parameters within the provisioning command.
1. Download and extract the [Connected Cache provisioning package for Windows](https://aka.ms/MCC-Ent-InstallScript-WSL) to your host machine.

   >[!Note]
   >* The provisioning package should be extracted to a directory that isn't synced to OneDrive, as the sychronization process will interfere with the installation. It is recommended to extract the provisioning package to the root directory of the host machine (e.g. C:\mccInstaller)

1. Open a PowerShell window *as administrator* on the host machine, then change directory to the extracted provisioning package.

   >[!Note]
   >* If you are deploying your cache node to a host machine that uses a TLS-inspecting proxy (e.g. ZScaler), ensure that you've [configured the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in the extracted provisioning package directory and add `-proxyTlsCertificatePath "path/to/pem/file"` to the provisioning command.

1. Set the Execution Policy to *Unrestricted* to allow the provisioning scripts to run.
1. Create a `$User` PowerShell variable containing the username of the account you intend to designate as the Connected Cache runtime account.

    For gMSAs, the `$User` PowerShell variable should be formatted as `"Domain\Username$"`. For local user accounts, the `$User` PowerShell variable should be formatted as `"LocalMachineName\Username"`.

   If you're using a local user account as the Connected Cache runtime account, you'll also need to create a [PSCredential Object](/dotnet/api/system.management.automation.pscredential) named `$myLocalAccountCredential`.

   >[!Note]
   >* You'll need to apply a local security policy to permit the local user account to `Log on as a batch job`.

1. Replace the values in the following provisioning command before running it on the host machine.

   ```powershell-interactive
   ./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid [enter mccResourceId here] -cachenodeid [enter cacheNodeId here] -customerkey [enter customerKey here] -registrationkey [enter registration key] -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy [enter true if present, enter false if not] -proxyurl "http://[enter proxy host name]:[enter port]"  -mccRunTimeAccount $User -mccLocalAccountCredential $myLocalAccountCredential
   ```

---

## Steps to point Windows client devices at Connected Cache node

Once you have successfully deployed Connected Cache to your Windows host machine, you'll need to configure your Windows client devices to request Microsoft content from the Connected Cache node.

You can do this by setting the [DOCacheHost or DOCacheHostSource policies via Intune](./waas-delivery-optimization-reference.md#cache-server-hostname).

## Next step

> [!div class="nextstepaction"]
> [Verify cache node functionality](mcc-ent-verify-cache-node.md)

## Related content

- [Deploy to a Linux host machine](mcc-ent-deploy-to-linux.md)
- [Uninstall Connected Cache node](mcc-ent-uninstall-cache-node.md)
