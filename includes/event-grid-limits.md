---
 title: include file
 description: include file
 services: event-grid
 author: tfitzmac
 ms.service: event-grid
 ms.topic: include
 ms.date: 04/30/2018
 ms.author: tomfitz
 ms.custom: include file
---

The following limits apply to Azure Event Grid system topics and custom topics, *not* event domains.

| Resource | Limit |
| --- | --- |
| Custom topics per Azure subscription | 100 |
| Event subscriptions per topic | 500 |
| Publish rate for a custom topic (ingress) | 5,000 events per second per topic |

The following limits apply to event domains only.

| Resource | Limit |
| --- | --- |
| Topics per event domain | 1,000 during public preview |
| Event subscriptions per topic within a domain | 50 during public preview |
| Domain scope event subscriptions | 50 during public preview |
| Publish rate for an event domain (ingress) | 5,000 events per second during public preview |