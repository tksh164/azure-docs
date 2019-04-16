---
title: Sources of data in Azure Monitor | Microsoft Docs
description: Describes the data available to monitor the health and performance of your Azure resources and the applications running on them.
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn

ms.service: azure-monitor
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/13/2018
ms.author: bwren

---

# Sources of data in Azure Monitor
This article describes the sources of data collected by Azure Monitor to monitor the health and performance of your  resources and the applications running on them. These resources could be in Azure, in another cloud, or on-premises.  See [Data collected by Azure Monitor](data-platform.md) for details on how this data stored and how you can view it.

Monitoring data in Azure comes from a variety of sources that can be organized into tiers, the highest tiers being your application and any operating systems and the lower tiers being components of Azure platform. This is illustrated in the following diagram with each tier described in detail in the following sections.

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-log-analytics-rebrand.md)]

![Tiers of monitoring data](media/data-sources/monitoring-tiers.png)

## Azure Tenant
Telemetry related to your Azure tenant is collected from tenant-wide services such as Azure Active Directory.

![Azure tenant collection](media/data-sources/tenant-collection.png)

### Azure Active Directory Audit Logs
[Azure Active Directory reporting](../../active-directory/reports-monitoring/overview-reports.md) contains the history of sign-in activity and audit trail of changes made within a particular tenant. These audit logs can be written to Azure Monitor logs to analyze them with other log data.


## Azure platform
Telemetry related to the health and operation of Azure itself includes data about the operation and management of your Azure subscription. It includes service health data stored in the Azure Activity log and audit logs from Azure Active Directory.

![Azure subscription collection](media/data-sources/azure-collection.png)

### Azure Service Health
[Azure Service Health](service-notifications.md) provides information about the health of the Azure services in your subscription that your application and resources rely on. You can create alerts to be notified of current and expected critical issues that may affect your application. Service Health records are stored in the [Azure Activity log](activity-logs-overview.md), so you can view them in the Activity Log Explorer and copy them into Azure Monitor logs.

### Azure Activity Log
The [Azure Activity Log](activity-logs-overview.md) includes service health records along with records on any configuration changes made to your Azure resources. The Activity log is available to all Azure resources and represents their _external_ view. The specific types of records in the Activity Log are described in [Azure Activity Log event schema](activity-log-schema.md).

You can view the Activity Log for a particular resource on its page in the Azure portal or view logs from multiple resources in the [Activity Log Explorer](activity-logs-overview.md). It's particularly useful to copy the log entries to Azure Monitor to combine it with other monitoring data. You can also send them to other locations using [Event Hubs](activity-logs-stream-event-hubs.md).



## Azure Services
Metrics and resource level diagnostic logs provide information about the _internal_ operation of Azure resources. These are available for most Azure services, and management solutions provide additional insights into particular services.

![Azure resource collection](media/data-sources/azure-resource-collection.png)


### Metrics
Most Azure services will generate [platform metrics](data-platform-metrics.md) that reflect their performance and operation. The specific [metrics will vary for each type of resource](metrics-supported.md).  They are accessible from metrics analytics and can be copied to logs for trending and other analysis using Log Analytics.


### Resource diagnostic Logs
While the Activity Log provides information about operations performed on an Azure resources, resource level [Diagnostic logs](diagnostic-logs-overview.md) provide insights into the operation of the resource itself.   The configuration requirements and content of these logs [varies by resource type](diagnostic-logs-schema.md).

You can't directly view diagnostic logs in the Azure portal, but you can [send them to Azure storage for archiving](archive-diagnostic-logs.md) and export them to [Event Hub](../../event-hubs/event-hubs-about.md) for redirection to other services, or [to Azure Monitor](diagnostic-logs-stream-log-store.md) for analysis. Some resources can write directly to Azure Monitor while others write to a storage account before being [imported into Log Analytics](azure-storage-iis-table.md#use-the-azure-portal-to-collect-logs-from-azure-storage).

### Monitoring Solutions
 [Monitoring solutions](../../azure-monitor/insights/solutions.md) collect data to provide additional insight into the operation of a particular service or application. They collect data into Azure Monitor logs where it may be analyzed using the [query language](../../azure-monitor/log-query/log-query-overview.md) or [views](view-designer.md) that are typically included in the solution.


## Guest operating system
Compute resources in Azure, in other clouds, and on-premises have a guest operating system to monitor. With the installation of one or more agents, you can gather telemetry from the guest into the same monitoring tools as the Azure services themselves.

![Azure compute resource collection](media/data-sources/compute-resource-collection.png)

### Azure Diagnostic extension
With the Azure Diagnostics extension, it provides a basic level of monitoring by collecting logs and performance data from the client operating system of Azure compute resources.   

### Log Analytics agent
Comprehensive monitoring and management of your Windows or Linux virtual machines or physical computer is delivered with the Log Analytics agent. The virtual machine can be running in Azure, another cloud, or on-premises and the agent connects to Azure Monitor either directly or through System Center Operations Manager and allows you to collect data from [data sources](agent-data-sources.md) that you configure or from [monitoring solutions](../../azure-monitor/insights/solutions.md) that provide additional insights into applications running on the virtual machine.


### Dependency agent
[Service Map](../insights/service-map.md) and [Azure Monitor for VMs](../../azure-monitor/insights/vminsights-overview.md) requires a Dependency Agent on Windows and Linux virtual machines. This integrates with the Log Analytics agent to collects discovered data about processes running on the virtual machine and external process dependencies. It stores this data in Azure Monitor and visualizes the discovered interconnected components.  

To further understand the differences between the agents and which to use depending on your monitoring requirements, see [monitoring agents overview](agents-overview.md).

## Applications
In addition to telemetry that your application may write to the guest operating system, detailed application monitoring is done with [Application Insights](https://docs.microsoft.com/azure/application-insights/). Application Insights can collect data from applications running on a variety of platforms. The application can be running in Azure, another cloud, or on-premises.

![Application data collection](media/data-sources/application-collection.png)


### Application data
When you enable Application Insights for an application by installing an instrumentation package, it collects metrics and logs related to the performance and operation of the application. This includes detailed information about page views, application requests, and exceptions. Application Insights stores the data it collects in Azure Monitor. It includes extensive tools for analyzing this data, but you can also analyze it with data from other sources using tools such as metric analytics and log analytics.

You can also use Application Insights to [create a custom metric](../../application-insights/app-insights-api-custom-events-metrics.md).  This allows you to define your own logic for calculating a numeric value and then storing that value with other metrics that can be accessed from metric analytics and used for [Autoscale](autoscale-custom-metric.md) and metric alerts.


### Dependencies
In order to monitor different logical operations of an application, you must [collect telemetry across multiple components](../../application-insights/app-insights-transaction-diagnostics.md). Application Insights supports [distributed telemetry correlation](../../application-insights/application-insights-correlation.md) which identifies the dependencies between components allowing you to analyze them together.

### Availability tests
[Availability tests](../../application-insights/app-insights-monitor-web-app-availability.md) in Application Insights allow you to test the availability and responsiveness of your application from different locations on the public Internet. You can do a simple ping test to verify that the application is alive or use Visual Studio to create a web test that simulates a user scenario.  Availability tests don't require any instrumentation in the application.

## Custom sources
In addition to the standard tiers of an application, you may need to monitor other resources that have telemetry that can't be collected with the other data sources. For these resources, you need to write this data using an Azure Monitor API.

![Custom data collection](media/data-sources/custom-collection.png)

### Data Collector API
Azure Monitor can collect log data from any REST client using the [Data Collector API](../../azure-monitor/platform/data-collector-api.md). This allows you to create custom monitoring scenarios and extend monitoring to resources that don't expose telemetry through other sources.

## Next steps

- Learn more about the [types of monitoring data collected by Azure Monitor](data-platform.md) and how to view and analyze this data.
