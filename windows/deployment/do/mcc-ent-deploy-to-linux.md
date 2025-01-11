---
title: Deploy Microsoft Connected Cache software to a Linux host machine
description: Details on how to deploy Microsoft Connected Cache for Enterprise and Education cache software to a Linux host machine.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 10/30/2024
appliesto: 
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Deploy Microsoft Connected Cache caching software to a Linux host machine

This article describes how to deploy Microsoft Connected Cache for Enterprise and Education caching software to a Linux host machine.

Before deploying Connected Cache to a Linux host machine, ensure that the host machine meets all [requirements](mcc-ent-prerequisites.md), and that you have [created and configured your Connected Cache Azure resource and cache node](mcc-ent-create-resource-and-cache.md).

## Steps to deploy Connected Cache cache node to Linux

# [Azure portal](#tab/portal)

1. Within the Azure portal, navigate to the **Provisioning** tab of your cache node and copy the provisioning command.
1. Download the provisioning package using the option at the top of the Cache Node Configuration page and extract the package onto the host machine.
1. Open a command line window *as administrator* on the host machine, then change directory to the extracted provisioning package.

    >[!Note]
    >* If you are deploying your cache node to a Linux host machine that uses a TLS-inspecting proxy (e.g. ZScaler), ensure that you've [configured the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in the extracted provisioning package directory and add `proxyTlsCertificatePath="/path/to/pem/file"` to the provisioning command.

1. Set access permissions to allow the `provisionmcc.sh` script within the provisioning package directory to execute.
1. Run the provisioning command on the host machine.

# [Azure CLI](#tab/cli)

To deploy a cache node programmatically, you'll need to use Azure CLI to get the cache node's provisioning details and then run the provisioning command on the host machine.

1. To get the cache node's provisioning details, use `az mcc ent node get-provisioning-details`

   ```azurecli-interactive
   az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
   ```

1. Save the resulting output. These values will be passed as parameters within the provisioning command.
1. Download and extract the [Connected Cache provisioning package for Linux](https://aka.ms/MCC-Ent-InstallScript-Linux) to your host machine.
1. Open a command line window *as administrator* on the host machine, then change directory to the extracted provisioning package.

    >[!Note]
    >* If you are deploying your cache node to a host machine that uses a TLS-inspecting proxy (e.g. ZScaler), ensure that you've [configured the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in the extracted provisioning package directory and add `proxyTlsCertificatePath="/path/to/pem/file"` to the provisioning command.

1. Set access permissions to allow the `provisionmcc.sh` script within the provisioning package directory to execute.
1. Replace the values in the following provisioning command before running it on the host machine.

   ```azurepowershell-interactive
   sudo ./provisionmcc.sh customerid="enter mccResourceId here" cachenodeid="enter cacheNodeId here" customerkey=" enter customerKey here " registrationkey="enter registrationKey here" drivepathandsizeingb="enter physicalPath value,enter sizeInGb value here" shoulduseproxy="enter true if present, enter false if not" proxyurl=http://enter proxy hostname:enter port
   ```

---

## Steps to point Windows client devices at Connected Cache node

Once you have successfully deployed Connected Cache to your Linux host machine, you'll need to configure your Windows client devices to request Microsoft content from the Connected Cache node.

You can do this by setting the [DOCacheHost or DOCacheHostSource policies via Intune](./waas-delivery-optimization-reference.md#cache-server-hostname).

## Next step

> [!div class="nextstepaction"]
> [Verify cache node functionality](mcc-ent-verify-cache-node.md)

## Related content

- [Deploy to a Windows host machine](mcc-ent-deploy-to-windows.md)
- [Uninstall Connected Cache node](mcc-ent-uninstall-cache-node.md)