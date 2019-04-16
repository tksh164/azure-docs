---
title: Manage read replicas for Azure Database for PostgreSQL from the Azure CLI
description: Learn how to manage Azure Database for PostgreSQL read replicas from the Azure CLI.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 04/05/2019
---

# Create and manage read replicas from the Azure CLI

In this article, you learn how to create and manage read replicas in Azure Database for PostgreSQL from the Azure CLI. To learn more about read replicas, see the [overview](concepts-read-replicas.md).

## Prerequisites
- An [Azure Database for PostgreSQL server](quickstart-create-server-up-azure-cli.md) to be the master server.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later. To see the version installed, run the `az --version` command. If you need to install or upgrade, see [Install Azure CLI]( /cli/azure/install-azure-cli). 


## Prepare the master server
These steps must be used to prepare a master server in the General Purpose or Memory Optimized tiers.

The `azure.replication_support` parameter must be set to **REPLICA** on the master server. When this static parameter is changed, a server restart is required for the change to take effect.

1. Set `azure.replication_support` to REPLICA.

   ```azurecli-interactive
   az postgres server configuration set --resource-group myresourcegroup --server-name mydemoserver --name azure.replication_support --value REPLICA
   ```

2. Restart to apply the change to the server.

   ```azurecli-interactive
   az postgres server restart --name mydemoserver --resource-group myresourcegroup
   ```

## Create a read replica

The [az postgres server replica create](/cli/azure/postgres/server/replica?view=azure-cli-latest#az-postgres-server-replica-create) command requires the following parameters:

| Setting | Example value | Description  |
| --- | --- | --- |
| resource-group | myresourcegroup |  The resource group where the replica server will be created.  |
| name | mydemoserver-replica | The name of the new replica server that is created. |
| source-server | mydemoserver | The name or resource ID of the existing master server to replicate from. |

```azurecli-interactive
az postgres server replica create --name mydemoserver-replica --source-server mydemoserver --resource-group myresourcegroup
```

If you haven't set the `azure.replication_support` parameter to **REPLICA** on a General Purpose or Memory Optimized master server and restarted the server, you receive an error. Complete those two steps before you create a replica.

A replica is created by using the same server configuration as the master. After a replica is created, several settings can be changed independently from the master server: compute generation, vCores, storage, and back-up retention period. The pricing tier can also be changed independently, except to or from the Basic tier.

> [!IMPORTANT]
> Before a master server configuration is updated to new values, update the replica configuration to equal or greater values. This action ensures the replica can keep up with any changes made to the master.

## List replicas
You can view the list of replicas of a master server by using [az postgres server replica list](/cli/azure/postgres/server/replica?view=azure-cli-latest#az-postgres-server-replica-list) command.

```azurecli-interactive
az postgres server replica list --server-name mydemoserver --resource-group myresourcegroup 
```

## Stop replication to a replica server
You can stop replication between a master server and a read replica by using [az postgres server replica stop](/cli/azure/postgres/server/replica?view=azure-cli-latest#az-postgres-server-replica-stop) command.

After you stop replication to a master server and a read replica, it can't be undone. The read replica becomes a standalone server that supports both reads and writes. The standalone server can't be made into a replica again.

```azurecli-interactive
az postgres server replica stop --name mydemoserver-replica --resource-group myresourcegroup 
```

## Delete a master or replica server
To delete a master or replica server, you use the [az postgres server delete](/cli/azure/postgres/server?view=azure-cli-latest#az-postgres-server-delete) command.

When you delete a master server, replication to all read replicas is stopped. The read replicas become standalone servers that now support both reads and writes.

```azurecli-interactive
az postgres server delete --name myserver --resource-group myresourcegroup
```

## Next steps
Learn more about [read replicas in Azure Database for PostgreSQL](concepts-read-replicas.md).