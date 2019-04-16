---
title: Azure PowerShell Samples for Azure Cosmos DB
description: Azure PowerShell Samples - Scripts to help you create and manage Azure Cosmos DB accounts. 
author: SnehaGunda
ms.service: cosmos-db
ms.topic: sample
ms.date: 10/16/2017
ms.author: sngun
---

# Azure PowerShell samples for Azure Cosmos DB

The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB. At this time, you can only manage the Azure Cosmos DB account via PowerShell; other resources such as databases and containers cannot be managed via PowerShell.

| |  |
|---|---|
|**Create an Azure Cosmos DB account**||
|[Create and configure a Cosmos account with SQL API](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a single Azure Cosmos DB account to use with the SQL API. |
|[Create and configure a Cosmos account with Azure Cosmos DB's API for MongoDB](scripts/create-mongodb-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a single Cosmos account with Azure Cosmos DB's API for MongoDB. |
|[Create and configure a Cosmos account with Gremlin API](scripts/create-graph-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a single Azure Cosmos DB account to use with the Gremlin API. |
|[Create and configure a Cosmos account with Cassandra API](scripts/create-and-configure-cassandra-database.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a single Azure Cosmos DB account to use with the Cassandra API. |
|[Create and configure a Cosmos account with Table API](scripts/create-table-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a single Azure Cosmos DB account to use with the Table API. |
|**Scale Azure Cosmos DB**||
|[Replicate Azure Cosmos DB account in multiple regions and configure failover priorities](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Globally replicates account data into multiple regions with a specified failover priority.|
|**Secure Azure Cosmos DB**||
| [Get account keys](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.|
| [Get MongoDB connection string](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.|
|[Regenerate account keys](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Regenerates the master or read-only key for the account.|
|[Create a firewall](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.|
|**High availability, disaster recovery, backup, and restore**||
|[Configure failover policy](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Sets the failover priority of each region in which the account is replicated.|
|||
