---
title: Smart Alerts in Azure Monitor Application Insights | Microsoft Docs
description: Application Insights performs automatic deep analysis of your app telemetry and warns you of potential problems or performance degradation. Now alerting on found anomalies
ms.topic: conceptual
ms.date: 02/10/2021

---

# Smart alerts in Application Insights (Preview)

## Overview

Smart Alerts (formerly know as Smart Detections) automatically warn you of potential performance problems and failure anomalies in your web application. It performs proactive analysis of the telemetry that your app sends to [Application Insights](./app-insights-overview.md). If there is a sudden rise in failure rate, or abnormal patterns in server or dependency performance, an alert is triggered. This feature needs no configuration, it operates automatically if your application sends enough telemetry.

When you create an Application Insights resource, Smart Alert rules are created for each of the different detection capabilities. You can manage and configure these rules just like any other Azure Monitor alert rules. You can also configure action groups for these rules, thus enabling multiple methods of taking actions or triggering notification on new detections.

You can access the Smart Alert detections both from the alerts you receive, and from the Application Insights Smart Detection blade in the Azure portal.

> [!NOTE]
> If you have existing Application Insights resources that are not yet migrated to Smart Alerts (preview), you can still use ![Smart Detections](../app/proactive-diagnostics.md) for that resource. You can ![migrate](.alerts-smart-detections-migration.md) to Smart Alerts (preview) at any time.

## Which problems are detected?

Smart Alerts detects and alerts about the following issues:

* [Smart detection - Failure Anomalies](./proactive-failure-diagnostics.md): Alerts if your application experiences an abnormal rise in the rate of HTTP requests or dependency calls that are reported as failed.
* [Smart detection - Response Latency Degradation](./alerts-response-latency-degradation.md): Alerts if your applicationhas started responding to requests more slowly than it used to.
* [Smart detection - Dependency Latency Degradation](./alerts-dependency-latency-degradation.md): Alerts if a dependency your applicationis calling has started responding to requests more slowly than it used to. Example for dependencies could be REST API or a database.
* [Smart detection - Trace Severity Degradation](./alerts-trace-severity-degradation.md): Alerts if the percentage of “bad” traces (logged with a level of Warning, Error, or Fatal) is degrading on a specific day, compared to a baseline calculated over the previous seven days.
* [Smart detection - Exception Anomalies](./alerts-exception-anomalies.md): Alerts if your applicationis exhibiting an abnormal rise in the number of exceptions of a specific type during a day, compared to a baseline calculated over the previous seven days.
* [Smart detection - Potential Memory Leak](./alerts-potential-memory-leak.md): Alerts on a consistent increase in memory consumption over a long period of time, in one or more processes and/or one or more machines, which are part of your application.

## How to view Smart Alerts detections?

You can discover Smart Alerts detections in two ways:

* **You receive an alert notification** from Azure. Here's a typical example of a Smart Alert email notification:
  
    ![Email alert](media/Smart-Detections-Alerts/Smart-Detection-Feed.png)
  
    Click the button "View the alert in Azure Monitor" button to view the alert details in the portal.
  
    ![Alert Details](media/Smart-Detections-Alerts/Smart-Detection-Feed.png)

* **The Smart Detection feed**. In your Application Insights resource blade, select **Smart Detection** under the **Investigate** menu to see a list of recent detections.

![View recent detections](media/Smart-Detections-Alerts/Smart-Detection-Feed.png)

Select a detection to see its details.

![View recent detections](media/Smart-Detections-Alerts/Smart-Detection-Feed.png)

## How to configure Smart Alert rules

You can disable or re-enable Smart Alert rules from the Azure portal, or using Azure Resource Manager ([see template example](./smart-detection-alerts-arm-config.md))

Smart Alert rules are automatically created with an associated [Action Group](../platform/action-groups.md) named **Application Insights Smart Detection** that contains email actions, and can be modified or extended to trigger additional actions when the alert fires.

> [!NOTE]
> By default, the Application Insights Smart Detection action groups is configured to send email notifications to users associated with the subscription's **Monitoring Reader** and **Monitoring Contributor** roles. More information is available [here](./smart-detection-alerts-configuration.md).

> [!NOTE]
> If your Smart Alerts have been migrated from the non-alert Smart Detection, you may have a different action group configuration on some of your Smart Alert rules, depending on your previously configured Smart Detection email settings. See [Smart Detection Alerts migration](./smart-detection-alerts-migration.md) for more details.

[See Manage Application Insights smart detection alert rules configuration](./smart-detection-alerts-configuration.md) for more details.

## Next steps

These Application Insights diagnostic tools help you inspect the telemetry from your app:

* [Metric explorer](../platform/metrics-charts.md)
* [Search explorer](./diagnostic-search.md)
* [Analytics - powerful query language](../log-query/log-analytics-tutorial.md)

Smart Alerts are completely automatic. But maybe you'd like to set up some more alerts?

* [Manually configured metric alerts](../platform/alerts-log.md)
* [Availability web tests](./monitor-web-app-availability.md)
