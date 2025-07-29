---
title: Microsoft Connected Cache for Enterprise and Education troubleshooting
description: Details on how to troubleshoot common issues for Microsoft Connected Cache for Enterprise.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
manager: naengler
ms.author: lichris
author: chrisjlin
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 07/28/2025
---


# Troubleshoot Microsoft Connected Cache for Enterprise and Education

This article contains instructions on how to troubleshoot different issues you may encounter while using Connected Cache. These issues are categorized by the task in which they may be encountered.

## Known issues

This section describes known issues with the latest release of Microsoft Connected Cache for Enterprise and Education. See the [Release Notes page](mcc-ent-release-notes.md) for more details on the fixes included in the latest release.

### Connected Cache Azure resource is missing from Scope selection under the "Metrics" tab

You can create custom charts on the Connected Cache Azure portal by selecting the **Metrics** tab under the **Monitoring** section of the Connected Cache Azure resource. The Connected Cache Azure resource is correctly selected as the Scope by default, but if you change the selected Scope you're unable to reselect the Connected Cache Azure resource, preventing subsequent creation of custom charts.

As a temporary workaround, you can navigate away from the **Metrics** tab and then return to it. The Connected Cache Azure resource is once again correctly selected as the Scope.

### importCert.ps1 limitations

The `importCert.ps1` script is used to import certificates into the Windows certificate store as part of the HTTPS configuration process for Windows-hosted cache nodes. This script doesn't currently support cache nodes deployed to Windows Server 2022 with a gMSA Connected Cache runtime account.

### Connected Cache Windows installer application limitations

The Connected Cache Windows installer application is an MSIX package that is used to deploy Connected Cache to Windows host machines. The installer application doesn't currently support Windows Server Core.

### Patched in latest release

[GA release: 7/23/2025](mcc-ent-release-notes.md)

* Connected Cache installation fails when Windows host machine is configured with a non-EN locale.
* Windows-hosted Connected Cache nodes can grow past their configured cache drive size.

## Steps to obtain an Azure subscription ID

<!--Using include file, get-azure-subscription.md, do/mcc-isp.md for shared content-->
[!INCLUDE [Get Azure subscription](includes/get-azure-subscription.md)]

## Troubleshooting Azure resource creation

[Connected Cache Azure resource creation](mcc-ent-create-resource-and-cache.md) can be initiated using either the Azure portal user interface or the Azure CLI command set.

If you're encountering an error during resource creation, [check that you have the necessary permissions to create Azure resources under your subscription](/azure/role-based-access-control/check-access) and have filled out all required fields during the resource creation process.

## Troubleshooting cache node configuration

[Configuration of your Connected Cache node](mcc-ent-create-resource-and-cache.md) can be done using either the Azure portal user interface or the Azure CLI command set.

If you're encountering a validation error, check that you have filled out all required configuration fields.

If your configuration doesn't appear to be taking effect, check that you have selected the **Save** option at the top of the configuration page in the Azure portal user interface.

If you have changed the proxy configuration, you need to redeploy the Connected Cache software on the host machine for the proxy configuration to take effect.

## Troubleshooting cache node deployment to Windows host machine

### Collecting Windows-hosted installation logs

[Deploying a Connected Cache node to a Windows host machine](mcc-ent-deploy-to-windows.md) involves running a series of PowerShell scripts contained within the Connected Cache Windows application. These scripts attempt to write log files to the Connected Cache application's script directory, specified by `deliveryoptimization-cli mcc-get-scripts-path`.

There are three types of installation log files:

1. **WSL_Mcc_Install_Transcript**: This log file records the lines printed to the PowerShell window when running the installation script
1. **WSL_Mcc_Install_FromRegisteredTask_Status**: This log file records the high level status that is written during the registered tasks install
1. **WSL_Mcc_Install_FromRegisteredTask_Transcript**: This log file records the detailed status that is written during the registered tasks install

The Registered Task Transcript is usually the most useful for diagnosing the installation issue.

### Collecting other Windows-hosted logs

Once the cache node has been successfully installed on the Windows host machine, it will periodically write log files to the installation directory (`C:\mccwsl01\` by default).

You can expect to see the following types of log files:

1. **WSL_Mcc_Monitor_FromRegisteredTask_Transcript**: This log file records the output of the "MCC_Monitor_Task" scheduled task that is responsible for ensuring that the Connected Cache continues running.
1. **WSL_Mcc_UserUninstall_Transcript**: This log file records the output of the "uninstallmcconwsl.ps1" script that the user can run to uninstall Connected Cache software from the host machine.
1. **WSL_Mcc_Uninstall_FromRegisteredTask_Transcript**: This log file records the output of the "MCC_Uninstall_Task" scheduled task that is responsible for uninstalling the Connected Cache software from the host machine when called by the "uninstallmcconwsl.ps1" script.

### Lauching a PowerShell process as the Connected Cache runtime account

To troubleshoot issues with the Connected Cache software on a Windows host machine, you may need to run commands as the Connected Cache runtime account. You can do this by launching a PowerShell process as the runtime account specified during the Connected Cache installation.

* **If the runtime account is a local account**, you can launch a PowerShell process as the runtime account by running the following command in an elevated PowerShell window:

    ```powershell
    Start-Process powershell.exe -Credential (Get-Credential "<RuntimeAccountName>") -ArgumentList '-NoExit'
    ```

* **If the runtime account is a domain or service account**, you can launch a PowerShell process as the runtime account by running the following command in an elevated PowerShell window:

    ```powershell
    Start-Process powershell.exe -Credential (Get-Credential "<Domain>\<RuntimeAccountName>") -ArgumentList '-NoExit'
    ```

* **If the runtime account is a Group Managed Service Account (gMSA)**, you must use [PsExec](/sysinternals/downloads/psexec) to launch a PowerShell process as the runtime account by running the following command in an elevated PowerShell window:

    ```powershell
    psexec.exe -i -u <DOMAIN\GmsaAccountName$> -p ~ powershell.exe 
    ```

### Checking if the Connected Cache container is running

Once the Connected Cache software has been successfully deployed to the Windows host machine, you can check if the cache node is running properly by doing the following on the Windows host machine:

1. Launch a PowerShell process as the account specified as the runtime account during the Connected Cache install
1. Run `wsl -d Ubuntu-24.04-Mcc` to access the Linux distribution that hosts the Connected Cache container
1. Run `sudo iotedge list` to show which containers are running within the IoT Edge runtime

If it shows the **edgeAgent** and **edgeHub** containers but doesn't show **MCC**, you can view the status of the IoT Edge security manager using `sudo iotedge system logs -- -f`.

You can also reboot the IoT Edge runtime using `sudo systemctl restart iotedge`.

### Connected Cache installation fails during cache node registration

As part of the installation process on Windows host machines, Connected Cache will attempt to register itself with the Delivery Optimization service by calling a registration endpoint `geomcc.prod.do.dsp.mp.microsoft.com`. This call originates from within the WSL2 distribution that hosts the Connected Cache container, and must be successful for the cache node to be installed.

To troubleshoot the connection, you can try running the following commands from an elevated PowerShell window as the Connected Cache runtime account.

First, access the WSL2 distribution that hosts the Connected Cache container:

```powershell
wsl -d Ubuntu-24.04-Mcc
```

Then, run the following bash command to check DNS resolution of the registration endpoint:

```bash
nslookup geomcc.prod.do.dsp.mp.microsoft.com
```

Check TCP connectivity (port 443 for HTTPS) to the registration endpoint:

```bash
nc -vz geomcc.prod.do.dsp.mp.microsoft.com 443
```

Check HTTPS response from the registration endpoint:

```bash
curl -v https://geomcc.prod.do.dsp.mp.microsoft.com
```

### MCC_Install_Task scheduled task fails to run

Connected Cache installation on Windows host machines relies on the "MCC_Install_Task" scheduled task to perform installation actions as the designated Connected Cache runtime account. If this task fails to run, it may be due to one of the following reasons.

#### Group Policy Object conflicts with Scheduled Task registration

Enabling the Group Policy Object: [Network access: Do not allow storage of passwords and credentials for network authentication](/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/network-access-do-not-allow-storage-of-passwords-and-credentials-for-network-authentication) will prevent the Connected Cache software from registering the scheduled tasks necessary for successful cache node registration and operation.

#### MCC runtime account doesn't have permissions to log on as batch job

Ensure that you have granted the Connected Cache runtime account the "Log on as a batch job" permission. This permission is required for the Connected Cache runtime account to run scheduled tasks.

#### Enterprise security policy prevents execution of PowerShell scripts

Ensure that the PowerShell execution policy on the Windows host machine allows the execution of scripts. You can check the current execution policy by running the following command in an elevated PowerShell window:

```powershell
Get-ExecutionPolicy
```

### WSL2 fails to install with message "A specified logon session doesn't exist"

If you're encountering this failure message when attempting to run the PowerShell command `wsl.exe --install --no-distribution` on your Windows host machine, verify that you're logged on as a local administrator and running the command from an elevated PowerShell window.

### Updating the WSL2 kernel

If the Connected Cache installation is failing due to WSL-related issues, try running `wsl.exe --update` to get the latest version of the WSL kernel.

### MCC_Monitor_Task scheduled task fails to run

Once the Connected Cache container is running, the MCC_Monitor_Task scheduled task periodically runs under the Connected Cache runtime account to keep WSL from stopping the Connected Cache WSL distribution. If your cache node goes offline without any user action, it may be due to the "MCC_Monitor_Task" scheduled task not running properly.

You can use Task Scheduler on the host machine to check the status of this scheduled task.

1. Open Task Scheduler on the host machine
1. Navigate to the Active Tasks section and double-click on **MCC_Monitor_Task**
1. Check the **Last Run Time** and **Last Run Result** columns to see if the operation completed successfully.
1. Select the **Triggers** tab and confirm that the Status is **Enabled**
1. Select the **History** tab and check for any errors or warnings related to the task execution.

If the **MCC_Monitor_Task** is failing to run successfully, it may be due to expired Connected Cache runtime account credentials. In this case, you can use the `updatetaskpasswords.ps1` script to update the credentials.

1. Open a PowerShell process as Administrator.
1. Change directory to the script directory and verify the presence of `updatetaskpasswords.ps1`.
    * If you installed Connected Cache using the Public Preview deployment package, the script directory is located within the installationFolder specified in the original deployment command ("C:\mccwsl01\MccScripts" by default).
    * If you installed Connected Cache using the Connected Cache Windows application, the script directory is located within the directory returned by `deliveryoptimization-cli mcc-get-scripts-path`.
1. Create a [PSCredential Object](/dotnet/api/system.management.automation.pscredential) named `$myLocalAccountCredential` representing the Connected Cache runtime account with the new password.
1. Run the `updatetaskpasswords.ps1` script with the following command:

    ```powershell-interactive
    .\updatetaskpasswords.ps1 -Credential $myLocalAccountCredential
    ```

### Cache node successfully deployed but not serving requests

If your cache node isn't responding to requests outside of localhost, it may be because the host machine's port forwarding rules weren't correctly set during Connected Cache installation. Since WSL2 uses a virtualized ethernet adapter by default, port forwarding rules are needed to allow traffic to reach the WSL2 instance from your LAN. For more information, see [Accessing network applications with WSL](/windows/wsl/networking#accessing-a-wsl-2-distribution-from-your-local-area-network-lan).

To check your host machine's port forwarding rules, use the following PowerShell command.

`netsh interface portproxy show v4tov4`

If you don't see any port forwarding rules for port 80 to 0.0.0.0, you can run the following command from an elevated PowerShell instance to set the proper forwarding to WSL.

`netsh interface portproxy add v4tov4 listenport=80 listenaddress=0.0.0.0 connectport=80 connectaddress=<WSL IP Address>`

You can retrieve the WSL IP Address from the `wslip.txt` file that should be present in the Connected Cache application's installation directory (`C:\mccwsl01` by default).

### Missing WSL port forwarding rules (443, 5000)

In order to successfully configure your Windows-hosted cache nodes to support HTTPS, you must create a port forwarding rule to forward traffic from port 443 on the host machine to port 443 on the WSL2 distribution that hosts the Connected Cache container.

In order to remote access your Windows-hosted cache node's Terse Summary page, you must create a port forwarding rule to forward traffic from port 5000 on the host machine to port 5000 on the WSL2 distribution that hosts the Connected Cache container.

You can create these port forwarding rules by running the following commands in an elevated PowerShell window after completing cache node deployment.

```powershell
$ipFilePath = Join-Path ([System.Environment]::GetEnvironmentVariable("MCC_INSTALLATION_FOLDER", "Machine")) "wslIp.txt"

$ipAddress = (Get-Content $ipFilePath | Select-Object -First 1).Trim()

netsh interface portproxy add v4tov4 listenport=443 listenaddress=0.0.0.0 connectport=443 connectaddress=$ipAddress
netsh interface portproxy add v4tov4 listenport=5000 listenaddress=0.0.0.0 connectport=5000 connectaddress=$ipAddress
```

You'll also need to ensure that the host machine's firewall allows inbound traffic on ports 443 and 5000. You can do this by running the following commands in an elevated PowerShell window:

```powershell
[void](New-NetFirewallRule -DisplayName "WSL2 Port Bridge (HTTPS)" -Direction Inbound -Action Allow -Protocol TCP -LocalPort "443"

[void](New-NetFirewallRule -DisplayName "WSL2 Port Bridge (HTTPS)" -Direction Outbound -Action Allow -Protocol TCP -LocalPort "443"

[void](New-NetFirewallRule -DisplayName "WSL2 Port Bridge (MCC SUMMARY)" -Direction Inbound -Action Allow -Protocol TCP -LocalPort "5000"
```

### Cache node deployment to Windows fails with "ERROR: cannot verify certificate"

If you're encountering an error during cache node deployment that states "ERROR: cannot verify certificate," it may be due to your network's TLS-inspecting proxy (e.g. ZScaler) intercepting the communication between the Connected Cache software and the Delivery Optimization service. This interception breaks the certificate chain and prevents Connected Cache from successfully deploying.

To resolve this issue, you must configure your network environment to allow calls to and from "*.prod.do.dsp.mp.microsoft.com" to **bypass** the TLS-inspecting proxy.

You must also [configure the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in your desired **installationFolder** path and add `-proxyTlsCertificatePemFileName "mycert.pem"` to the deployment command. For example, place the .pem file in `C:\mccwsl01\mycert.pem` and add `-proxyTlsCertificatePemFileName "mycert.pem"` to the deployment command.

## Troubleshooting cache node deployment to Linux host machine

[Deploying a Connected Cache node to a Linux host machine](mcc-ent-deploy-to-linux.md) involves running a series of Bash scripts contained within the Linux deployment package.

Once the Connected Cache software has been successfully deployed to the Linux host machine, you can check if the cache node is running properly by doing the following on the Linux host machine:

1. Run `sudo iotedge list` to show which containers are running within the IoT Edge runtime

If it shows the **edgeAgent** and **edgeHub** containers but doesn't show **MCC**, you can view the status of the IoT Edge security manager using `sudo iotedge system logs -- -f`.

You can also reboot the IoT Edge runtime using `sudo systemctl restart iotedge`.

>[!NOTE]
> After redeploying a Linux cache node so that it's migrated to the GA release container, the user must run `chmod 777 -R /cachedrivepath` and then restart the Connected Cache container `sudo iotedge restart MCC`.
> Otherwise the redeployed node will be up and running, but requests for content will fail.

### Cache node deployment to Linux fails with "ERROR: cannot verify certificate"

If you're encountering an error during cache node deployment that states "ERROR: cannot verify certificate," it may be due to your network's TLS-inspecting proxy (e.g. ZScaler) intercepting the communication between the Connected Cache software and the Delivery Optimization service. This interception breaks the certificate chain and prevents Connected Cache from successfully deploying.

To resolve this issue, you must configure your network environment to allow calls to and from "*.prod.do.dsp.mp.microsoft.com" to **bypass** the TLS-inspecting proxy.

You must also [configure the proxy settings](mcc-ent-create-resource-and-cache.md#proxy-settings) for your cache node, then place the proxy certificate file (.pem) in the extracted deployment package directory and add `proxytlscertificatepath="/path/to/pem/file"` to the deployment command.

## Generating cache node diagnostic support bundle

You can generate a support bundle with detailed diagnostic information by running the `collectMccDiagnostics.sh` script included in the installation package.

For **Windows** host machines, you need to do the following:

1. Launch a PowerShell process as the account specified as the runtime account during the Connected Cache install
1. Change directory to the "MccScripts" directory within the Connected Cache application's installation directory (specified by `deliveryoptimization-cli mcc-get-scripts-path`) and verify the presence of `collectmccdiagnostics.sh`
1. Run `wsl bash collectmccdiagnostics.sh` to generate the diagnostic support bundle
1. Once the script has completed, note the console output describing the location of the diagnostic support bundle

    For example, "Successfully zipped package, please send file created at /etc/mccdiagnostics/support_bundle_2024_12_03__11_05_39__AM.tar.gz"

1. Run the `wsl cp` command to copy the support bundle from the location within the Ubuntu distribution to the Windows host OS

    For example, `wsl cp /etc/mccdiagnostics/support_bundle_2024_12_03__11_05_39__AM.tar.gz /mnt/c/mccwsl01/SupportBundles/`

For **Linux** host machines, you need to do the following:

1. Change directory to the "MccScripts" directory within the extracted Connected Cache deployment package and verify the presence of `collectmccdiagnostics.sh`
1. Run `collectmccdiagnostics.sh` to generate the diagnostic support bundle
1. Once the script completes, note the console output describing the location of the diagnostic support bundle

    For example, "Successfully zipped package, please send file created at /etc/mccdiagnostics/support_bundle_2024_12_03__11_05_39__AM.tar.gz"

## Troubleshooting HTTPS configuration

If your Certificate Authority (CA) is only able to generate signed certificates in .pem or .cer formats, you can change the file extension of the certificate file to .crt if the file is in Base64 encoding.

## Troubleshooting cache node monitoring

Connected Cache node status and performance can be [monitored using the Azure portal user interface](mcc-ent-monitoring.md).

If the [basic monitoring](mcc-ent-monitoring.md#basic-monitoring) visuals on the Overview tab are showing unexpected or erroneous values, refresh the browser window.

If the issue persists, check that you have configured the Timespan and Cache node filters as desired.

## Diagnose and Solve

You can also use the **Diagnose and solve problems** functionality provided by the Azure portal interface. This tab within the Microsoft Connected Cache Azure resource walks you through a few prompts to help narrow down the solution to your issue.
