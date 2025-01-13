---
author: paolomatarazzo
ms.author: paoloma
ms.date: 11/04/2024
ms.topic: include
---

### Disable Account Notifications

This policy controls the notifications to Microsoft account (MSA) and local users in the Start's user tile:

- When enabled, Windows doesn't send account related notifications for local and MSA users to the user tile in Start
- Wen disabled or not configured, Windows sends account related notifications for local and MSA users to the user tile in Start

Notifications include getting users to:

- reauthenticate
- back up their device
- manage cloud storage quotas
- manage their Microsoft 365 or XBOX subscription

|  | Path |
|--|--|
| **CSP** | `./User/Vendor/MSFT/Policy/Config/Notifications/`[DisableAccountNotifications](/windows/client-management/mdm/policy-csp-notifications#disableaccountnotifications) |
| **GPO** | **User Configuration** > **Administrative Templates** > **Windows Components** > **Account Notifications** > **Turn off account notifications in Start** |
