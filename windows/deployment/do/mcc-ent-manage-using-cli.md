---
title: Manage Microsoft Connected Cache nodes using CLI
description: Details on how to manage Microsoft Connected Cache for Enterprise cache nodes via Azure CLI commands.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
manager: aaroncz
ms.author: nidos
author: doshnid
ms.reviewer: mstewart
ms.collection: tier3
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 10/30/2024
---

# Manage cache nodes using CLI

<br>

This article outlines how to create, configure, and deploy Microsoft Connected Cache for Enterprise cache nodes using Azure CLI.

 
## Prerequisites:
1. **Install Azure CLI**: [How to install the Azure CLI](/cli/azure/install-azure-cli)
1. **Install Connected Cache extension**: Install Connected Cache extension via the command below

```azurecli-interactive
az extension add --name mcc
```

To learn more about installing extensions, see [Install the Connected Cache extension.](/cli/azure/azure-cli-extensions-overview#how-to-install-extensions)

<br>
<br>

### 1. Create a Resource group

The first step is to create a resource group if you don't already have one.
An Azure resource group is a logical container into which Azure resources are deployed and managed.

To create a resource group, use `az group create`. You can find more details on this CLI command [here](/cli/azure/group#az-group-create).
<br>

```azurecli-interactive
az group create --name myrg --location westus
```

Once the resource group is created, you'll need to create a Microsoft Connected Cache for Enterprise resource.

### 2. Create a Connected Cache Azure resource

A Connected Cache Azure resource is a top-level Azure resource under which cache nodes can be created.

To create a Connected Cache Azure resource, use `az mcc ent resource create`

```azurecli-interactive
az mcc ent resource create --mcc-resource-name mymccresource --resource-group myrg
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating your Connected Cache resource.

<br>

The next step is to create a cache node under this resource.


### 3. Create a cache node

To create a cache node, use `az mcc ent node create`

```azurecli-interactive
az mcc ent node create --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg --host-os <linux or windows>
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating cache node.

<br>

### 4. Confirm cache node creation

Before you can start configuring your cache node, you need to confirm that the cache node was successfully created.

To confirm cache node creation, use `az mcc ent node show`

<br>

```azurecli-interactive
az mcc ent node show --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg  
```

>[!IMPORTANT]
>In the output look for cacheNodeState. If **cacheNodeState = Not Configured**, you can continue with cache node configuration.
>If **cacheNodeState = Registration in Progress**, then the cache node is still in process of being created. Please wait for a minute or two more and run the command again.

<br>

Once successful cache node creation is confirmed, you can proceed to configure the cache node.


### 5. Configure cache node

To configure your cache node, use `az mcc ent node update`

The below example configures a Linux cache node with proxy enabled:

```azurecli-interactive
az mcc ent node update --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg>
--cache-drive "[{physical-path:</physical/path>,size-in-gb:<size of cache drive>},{</physical/path>,size-in-gb:<size of cache drive>}...]"> --proxy <enabled> --proxy-host <"proxy host name"> --proxy-port <proxy port>  --auto-update-day <day of week> --auto-update-time <time of day> --auto-update-week <week of month> --auto-update-ring <update ring>
```

>[!Note]
>* For a cache node that is to be deployed on Windows host OS, the physical path of the cache drive <u>must</u> be **/var/mcc**.<br>
>* In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully updated the cache node. You will also see that cacheNodeState will show *Not Provisioned*. <br>
>* Please save values for <u>physicalPath, sizeInGb, proxyPort, proxyHostName</u> as these values will be needed to construct the provisioning script.


<br>

### 6. Get provisioning details for the cache node

After successfully configuring the cache node, the next step is to deploy the cache node to a host machine. To deploy the cache node, you'll need to create a provisioning script with relevant information.

To get the relevant information for provisioning script, use `az mcc ent node get-provisioning-details`

```azurecli-interactive
az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
```

>[!IMPORTANT]
>* Save the resulting values for cacheNodeId, customerKey, mccResourceId, registrationKey. These GUIDs are needed to create the provisioning script.
>* In the output look for cacheNodeState. If **cacheNodeState = Not Provisioned**, you can continue with cache node provisioning.
>* If **cacheNodeState = Not Configured**, then the cache node has not been configured. Configure the cache node before provisioning.

<br>

## Next step

To deploy the cache node to a **Windows** host machine, see 
>[!div class="nextstepaction"]
>[Deploy cache node to Windows](mcc-ent-deploy-to-windows.md)

To deploy the cache node to a **Linux** host machine, see 
>[!div class="nextstepaction"]
>[Deploy cache node to Linux](mcc-ent-deploy-to-linux.md)

<br>

### Example script to bulk create and configure multiple cache nodes:

Below is a pseudocode example of how to script bulk creation and configuration of a Connected Cache Azure resource and multiple Connected Cache cache nodes:

<!--# [Bash](#tab/bash)

:::code language="azurecli" source="~/azure_cli_scripts/azure-cli/create-azure-resources-at-scale/bash/create-azure-resources-at-scale.sh" id="step4":::

In your console output, are you missing the last row in your CSV file?  This can be caused by a missing line continuation character after the last line. Add a blank line at the end of your CSV file to fix the issue.

# [PowerShell](#tab/powershell)

:::code language="azurecli" source="~/azure_cli_scripts/azure-cli/create-azure-resources-at-scale/powershell/create-azure-resources-at-scale.ps1" id="step4":::

-->

# [PowerShell](#tab/powershell)

```powershell
#Define variables
$mccResourceName = "myMCCResource"
$cacheNodeName = "demo-node"
$cacheNodeOperatingSystem = "Windows"
$resourceGroup = "myRG"
$resourceLocation = "westus"
$cacheNodesToCreate = 2
$proxyHost = "myProxy.com"
$proxyPort = "8080"
$waitTime = 3

# Create Microsoft Connected Cache Azure resource
az mcc ent resource create --mcc-resource-name $mccResourceName --location $resourceLocation --resource-group $resourceGroup

#Loop through $cacheNodesToCreate iterations
for ($cacheNodeNumber = 1; $cacheNodeNumber -le $cacheNodesToCreate; $cacheNodeNumber++) {
    $iteratedCacheNodeName = $cacheNodeName + "-" + $cacheNodeNumber
    
    #Create cache node
    az mcc ent node create --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --host-os $cacheNodeOperatingSystem --resource-group $resourceGroup

    #Get cache node state
    $cacheNodeState = $(az mcc ent node show --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --resource-group $resourceGroup --query "cacheNodeState") | ConvertFrom-Json

    $howLong = 0
    #Wait until cache node state returns "Not Configured"
    while ($cacheNodeState -ne "Not Configured") {
        Write-Output "Waiting for cache node creation to complete...$howLong seconds"
        Start-Sleep -Seconds $waitTime
        $howLong += $waitTime
    
        $cacheNodeState = $(az mcc ent node show --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --resource-group $resourceGroup --query "cacheNodeState") | ConvertFrom-Json
    }

    #Configure cache node
    az mcc ent node update --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --resource-group $resourceGroup --cache-drive  "[{physical-path:/var/mcc,size-in-gb:50}]" --proxy enabled --proxy-host $proxyHost --proxy-port $proxyPort
}
```
---

