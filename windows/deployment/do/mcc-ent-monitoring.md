---
title: Monitor usage of Microsoft Connected Cache nodes
description: Details on how to monitor the usage of Microsoft Connected Cache for Enterprise cache nodes.
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
ms.date: 10/30/2024
---

# Monitor cache node usage

Tracking the status and performance of your Connected Cache node is essential to making sure you're getting the most out of the service.

For basic monitoring, navigate to the **Overview** tab. Here you can view a collection of predefined metrics and charts. All the monitoring in this section will function right after your Connected Cache node has been deployed. You can view more details about each cache node by navigating to the **Cache Nodes** section under the **Cache Node Management** tab. This page displays cache node information such as Status, Host machine OS, Software Version, and Cache Node ID.

For advanced monitoring, navigate to the **Metrics** section under the **Monitoring** tab. Here you can access more sampled metrics (hits, misses, inbound traffic) and specify different aggregations (count, avg, min, max, sum). You can then use this data to create customized charts and configure alerts.

Using the two monitoring sections, you can gather essential insights into the health, performance, and efficiency of your Connected Cache nodes.

## Basic Monitoring

### Cache node summary

Below are the metrics found in the **Cache Node Summary** dashboard, along with their descriptions. This dashboard only reflects data received from cache nodes in the last 24 hours.

![Screenshot of cache node summary in the Azure portal interface.](../images/mcc-ent-cache-node-summary.png)

| Metric | Description |
| --- | --- |
| Healthy nodes | Your Connected Cache node will periodically send heartbeat messages to the Connected Cache service. If the Connected Cache service has received a heartbeat message from your Connected Cache node in the last 24 hours, the node is labeled as healthy. |
| Unhealthy nodes | If the Connected Cache service hasn't received a heartbeat message from your Connected Cache node in the last 24 hours, the node is labeled as unhealthy. |
| Max in | The maximum ingress in Megabits per second (Mbps) that your node has pulled from Content Delivery Network (CDN) endpoints in the last 24 hours. |
| Max out | The minimum egress in Mbps that your node has sent to Windows devices in its network over the last 24 hours. |
| Average in | The average ingress in Mbps that your node has pulled from CDN endpoints in the last 24 hours. |
| Average out | The average egress in Mbps that your node has sent to Windows devices in its network over the last 24 hours. |
| Cache efficiency | The percentage of all content requests your Connected Cache node receives that can be fulfilled using your node's cached content. A well-performing node should have an efficiency > 90%. |

### Key metric charts

The two predefined charts on the Overview page visually represent the egress and types of content served by your Connected Cache node. The filters that are displayed below the cache node summary dashboard only affect the data shown in the key metric charts.

![Screenshot of key metric charts in the Azure portal interface.](../images/mcc-ent-key-metric-charts.png)

#### Filters

There are two filter controls that can be used to configure the key metric charts.

- Timespan: Select how far back the chart should display
- Cache nodes: Select which Connected Cache nodes the chart should display data for

#### Outbound Traffic Chart

This chart displays the average egress in bits per second (b/s) that your selected Connected Cache nodes delivered over the specified timespan.

#### Volume by Content Type

This chart displays the volume of each supported content type in bytes (B) that your selected Connected Cache nodes delivered over the specified timespan. See [Microsoft Connected Cache content and services endpoints](delivery-optimization-endpoints.md) for a complete list of supported content types.

The content types displayed in the chart each have a distinct color and are sorted in descending order of volume. The bar chart is stacked such that you can visually compare total volume being delivered at different points in time.

### Cache node details

The **Cache Nodes** section under the **Cache Node Management** tab displays cache node information such as Status, Host machine OS, Software Version, and Cache Node ID.

![Screenshot of cache node details in the Azure portal interface.](../images/mcc-ent-cache-node-details.png)

| Metric | Description |
| --- | --- |
| Cache node name | The user-defined name of the cache node. |
| Status | The heartbeat status of the cache node. |
| OS | The host machine OS that this cache node is compatible with. |
| Software version | The version number of the cache node's Connected Cache container. |
| Cache node ID | The unique identifier of the cache node. |

## Advanced Monitoring

To expand upon the metrics shown in the Overview tab, navigate to the **Metrics** tab in the left side toolbar of Azure portal.

Listed below are the metrics you can access in this section:

| Metric | Description |
| --- | --- |
| Inbound | The number of content requests your Connected Cache node receives over a specified period of time. |
| Hits | The number of times your Connected Cache node fulfills a content request by pulling from its cache. |
| Misses | The number of times your Connected Cache node isn't able to fulfill a content request by pulling from its cache |

### Customizable Dashboards

Once you select the charts you would like to track, you can save them to a personalized dashboard. You can configure the chart title, filters, range, legend, and more. You can also use this personalized dashboard to set up alerts that notify you if your Connected Cache node dips in performance.

Some example scenarios where you would want to set up a custom alert:

- My Connected Cache node is being shown as unhealthy and I want to know exactly when it stopped egressing last
- A new Microsoft Word update was released last night and I want to know if my Connected Cache node is helping deliver this content to my Windows devices

## Client-Side Metrics

Your Connected Cache node can keep track of how much content has been sent to requesting Windows devices, but the node can't track whether the content was successfully received by the device. For more information on accessing client-side data from your Windows devices, see [Monitor Delivery Optimization](waas-delivery-optimization-monitor.md).
