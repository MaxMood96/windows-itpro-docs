---
title: Update Microsoft Connected Cache for Enterprise and Education cache nodes
description: Details on how Microsoft Connected Cache for Enterprise and Education cache nodes are updated by Microsoft.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.author: andyriv
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a> 
ms.date: 10/30/2024
---
# Configure container update frequency for Microsoft Connected Cache for Enterprise and Education

Microsoft Connected Cache for Enterprise and Education caching software is deployed to host machines as a container. The container OS and any software component within the container need to be updated to address security vulnerabilities and improve quality and performance. These Microsoft-published container updates are referred to as "Connected Cache updates" in this article.

Microsoft silently deploys Connected Cache updates to your cache nodes based on the **Update Ring** setting you configure for each cache node.

## Update rings

Connected Cache nodes can be configured to either the `Fast` or `Slow` update ring. If configured to update as part of the Fast ring, the cache node will be silently updated by Microsoft soon after the update is made available. If configured to update as part of the `Slow` ring, the cache node is silently updated by Microsoft within five weeks of the update becoming available.

In other words, configuring cache nodes to update as part of the `Slow` ring provides users with the option to delay the update process until they have validated that the latest Connected Cache update works within their environment. For example, a user could configure a test cache node to update as part of the `Fast` ring and validate that clients can successfully interact with the test cache node after the latest Connected Cache update has been applied. This builds confidence that service won't be interrupted when the production cache nodes are updated as part of the `Slow` ring.

### Update ring options

>[!IMPORTANT]
> In the event of a critical security patch, Microsoft may elect to initiate a Connected Cache update to your cache node as soon as possible (even if the cache node has been set to the `Slow` Ring). Visit the [Release notes](mcc-ent-release-notes.md) page for a detailed changelog of each Connected Cache update.

#### Fast Ring

All Connected Cache nodes are configured to update as part of the `Fast` ring by default. Connected Cache nodes in the `Fast` ring will be updated soon after an update is made available. The update will silently update cache nodes at a time of day when update traffic is likely to be minimal, such as 3:00 AM (local time) on Saturday.

#### Slow Ring

Configuring a Connected Cache node to update as part of the `Slow` ring provides users with the option to delay Connected Cache software updates until the update can be validated. There are three settings that control when Connected Cache updates will be applied to Connected Cache nodes. All update ring settings can be managed from the Azure portal or through the Azure CLI.

| Setting | Description |
| --- | --- |
| Week of the month | 1st to 4th week can be selected. There are three to four months in a year that could have a fifth week. If there's a fifth week, the update could be applied during that fifth week if the day of the week falls near the last day of the month.|
| Day of the week | Monday through Sunday can be selected. |
| Time of day | Time of day is based on UTC and a 24 hour clock. |

## Update process

When Microsoft publishes a Connected Cache update, the Connected Cache service attempts to update all Connected Cache nodes based on their **Update Ring** membership. If a cache node can't complete the silent Connected Cache update within 6 hours of starting, an error message is surfaced in the Azure portal.

## Update terminology, criteria, and information

Connected Cache updates are released based on need instead of on a set cadence.

| Update type | Criteria and information |
| --- | --- |
| Security | Security updates are the highest priority and are released based on the severity rating of the vulnerability. Updates for [Critical and High](https://nvd.nist.gov/vuln-metrics/cvss) vulnerabilities are released by Microsoft within 60 days of discovery. Updates for [Medium and Low](https://nvd.nist.gov/vuln-metrics/cvss) vulnerabilities are released by Microsoft within 120 days. |
| Quality | Quality updates fix a specific problem and addresses a noncritical, non-security-related bug. Quality updates could include performance fixes for a specific problem or changes related to cache efficiency or maximum egress for example. Quality updates are released along with security updates or when necessary to ensure proper functioning of the Microsoft Connected Cache software. |

For information on all released Microsoft Connected Cache updates, see the [Connected Cache release notes](mcc-ent-release-notes.md).
