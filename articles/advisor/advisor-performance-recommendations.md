﻿---
title: Improve performance of Azure applications with Azure Advisor | Microsoft Docs
description: Use Advisor to optimize the performance of your Azure deployments.
services: advisor
documentationcenter: NA
author: kasparks
ms.service: advisor
ms.topic: article
ms.date: 01/29/2019
ms.author: kasparks
---

# Improve performance of Azure applications with Azure Advisor

Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications. You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.

## Reduce DNS time to live on your Traffic Manager profile to fail over to healthy endpoints faster

[Time to Live (TTL) settings](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-performance-considerations) on your Traffic Manager profile allow you to specify how quickly to switch endpoints if a given endpoint stops responding to queries. Reducing the TTL values means that clients will be routed to functioning endpoints faster.

Azure Advisor identifies Traffic Manager profiles with a longer TTL configured and recommends configuring the TTL to either 20 seconds or 60 seconds depending on whether the profile is configured for [Fast Failover](https://azure.microsoft.com/roadmap/fast-failover-and-tcp-probing-in-azure-traffic-manager/).

## Improve database performance with SQL DB Advisor

Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources. It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database. SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history. It then offers recommendations that are best suited for running the database’s typical workload.

> [!NOTE]
> To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity. SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.

For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/documentation/articles/sql-database-advisor/).

## Improve App Service performance and reliability

Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities. Examples of App Services recommendations are:
* Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.
* Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.

For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-best-practices/).

## Use Managed Disks to prevent disk I/O throttling

Advisor will identify virtual machines that belong to a storage account that is reaching its scalability target. This condition makes those VMs susceptible to I/O throttling. Advisor will recommend that they use Managed Disks to prevent performance degradation.

## Improve the performance and reliability of virtual machine disks by using Premium Storage

Advisor identifies virtual machines with standard disks that have a high volume of transactions on your storage account and recommends upgrading to premium disks. 

Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads. Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs). For the best performance for your application, we recommend that you migrated any virtual machine disks requiring high IOPS to premium storage.

## Remove data skew on your SQL data warehouse table to increase query performance

Data skew can cause unnecessary data movement or resource bottlenecks when running your workload. Advisor will detect distribution data skew greater than 15% and recommend that you redistribute your data and revisit your table distribution key selections. To learn more about identifying and removing skew, see [troubleshooting skew](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute#how-to-tell-if-your-distribution-column-is-a-good-choice).

## Create or update outdated table statistics on your SQL data warehouse table to increase query performance

Advisor identifies tables that do not have up-to-date [table statistics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-statistics) and recommends creating or updating table statistics. The SQL data warehouse query optimizer uses up-to-date statics to estimate the cardinality or number of rows in the query result that enables the query optimizer to create a high-quality query plan for fastest performance.

## Scale up to optimize cache utilization on your SQL Data Warehouse tables to increase query performance

Azure Advisor detects if your SQL Data Warehouse has high cache used percentage and a low hit percentage. This condition indicates high cache eviction, which can impact the performance of your SQL Data Warehouse. Advisor suggests that you scale up your SQL Data Warehouse to ensure you allocate enough cache capacity for your workload.

## Convert SQL Data Warehouse tables to replicated tables to increase query performance

Advisor identifies tables that are not replicated tables but would benefit from converting and suggests that you convert these tables. Recommendations are based on the replicated table size, number of columns, table distribution type, and number of partitions of the SQL Data Warehouse table. Additional heuristics may be provided in the recommendation for context. To learn more about how this recommendation is determined, see [SQL Data Warehouse Recommendations](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-concept-recommendations#replicate-tables). 

## Migrate your Storage Account to Azure Resource Manager to get all of the latest Azure features

Migrate your Storage Account deployment model to Azure Resource Manager (Resource Manager) to take advantage of template deployments, additional security options, and the ability to upgrade to a GPv2 account for utilization of Azure Storage's latest features. Advisor will identify any stand-alone storage accounts that are using the Classic deployment model and recommends migrating to the Resource Manager deployment model.

> [!NOTE]
> Classic alerts in Azure Monitor are scheduled to retire in June 2019. We recommended that you upgrade your classic storage account to use Resource Manager to retain alerting functionality with the new platform. For more information, see [Classic Alerts Retirement](https://azure.microsoft.com/updates/classic-alerting-monitoring-retirement/).

## How to access Performance recommendations in Advisor

1. Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).

2.	On the Advisor dashboard, click the **Performance** tab.

## Next steps

To learn more about Advisor recommendations, see:

* [Introduction to Advisor](advisor-overview.md)
* [Get started with Advisor](advisor-get-started.md)
* [Advisor Cost recommendations](advisor-performance-recommendations.md)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md)
* [Advisor Security recommendations](advisor-security-recommendations.md)
