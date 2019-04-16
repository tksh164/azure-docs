---
title: How to configure multi-master in Azure Cosmos DB
description: Learn how to configure multi-master in your applications in Azure Cosmos DB
author: markjbrown
ms.service: cosmos-db
ms.topic: sample
ms.date: 2/12/2019
ms.author: mjbrown
---

# How to configure multi-master in your applications that use Azure Cosmos DB

To use multi-master features in your applications you need to enable multi-region writes and configure the multihoming capability. Multihoming is configured by setting the current region where the application is deployed.

## <a id="netv2"></a>.NET SDK v2

To enable multi-master in your applications set `UseMultipleWriteLocations` to true and configure `SetCurrentLocation` to the region in which the application is being deployed and Azure Cosmos DB is replicated.

```csharp
ConnectionPolicy policy = new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp,
        UseMultipleWriteLocations = true
    };
policy.SetCurrentLocation("West US 2");
```

## <a id="netv3"></a>.NET SDK v3 (preview)

To enable multi-master in your applications configure `UseCurrentRegion` to the region in which the application is being deployed and Cosmos DB is replicated.

```csharp
CosmosConfiguration config = new CosmosConfiguration("endpoint", "key");
config.UseCurrentRegion("West US");
CosmosClient client = new CosmosClient(config);
```

## <a id="java"></a>Java Async SDK

To enable multi-master in your applications set `policy.setUsingMultipleWriteLocations(true)` to true and configure `policy.setPreferredLocations` to the region in which the application is being deployed and Cosmos DB is replicated.

```java
ConnectionPolicy policy = new ConnectionPolicy();
policy.setUsingMultipleWriteLocations(true);
policy.setPreferredLocations(Collections.singletonList(region));

AsyncDocumentClient client =
    new AsyncDocumentClient.Builder()
        .withMasterKeyOrResourceToken(this.accountKey)
        .withServiceEndpoint(this.accountEndpoint)
        .withConsistencyLevel(ConsistencyLevel.Eventual)
        .withConnectionPolicy(policy).build();
```

## <a id="javascript"></a>Node.js, JavaScript, TypeScript SDK

To enable multi-master in your applications set `connectionPolicy.UseMultipleWriteLocations` to true and configure `connectionPolicy.PreferredLocations` to the region in which the application is being deployed and Cosmos DB is replicated.

```javascript
const connectionPolicy: ConnectionPolicy = new ConnectionPolicy();
connectionPolicy.UseMultipleWriteLocations = true;
connectionPolicy.PreferredLocations = [region];

const client = new CosmosClient({
  endpoint: config.endpoint,
  auth: { masterKey: config.key },
  connectionPolicy,
  consistencyLevel: ConsistencyLevel.Eventual
});
```

## <a id="python"></a>Python SDK

To enable multi-master in your applications set `connection_policy.UseMultipleWriteLocations` to true and configure `connection_policy.PreferredLocations` to the region in which the application is being deployed and Cosmos DB is replicated.

```python
connection_policy = documents.ConnectionPolicy()
connection_policy.UseMultipleWriteLocations = True
connection_policy.PreferredLocations = [region]

client = cosmos_client.CosmosClient(self.account_endpoint, {'masterKey': self.account_key}, connection_policy, documents.ConsistencyLevel.Session)
```

## Next steps

Learn more about multi-master, global distribution and consistency in Azure Cosmos DB. See the following articles:

* [Utilize session tokens for managing consistency in Azure Cosmos DB](how-to-manage-consistency.md#utilize-session-tokens)

* [Conflict types and resolution policies in Azure Cosmos DB](conflict-resolution-policies.md)

* [High availability in Azure Cosmos DB](high-availability.md)

* [Choosing the right consistency level in Azure Cosmos DB](consistency-levels-choosing.md)

* [Consistency, availability and performance tradeoffs in Azure Cosmos DB](consistency-levels-tradeoffs.md)
