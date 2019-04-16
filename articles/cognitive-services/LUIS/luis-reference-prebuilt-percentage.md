---
title: Percentage Prebuilt entity
titleSuffix: Azure
description: This article contains percentage prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 02/28/2019
ms.author: diberry
---

# Percentage prebuilt entity for a LUIS app
Percentage numbers can appear as fractions, `3 1/2`, or as percentage, `2%`. Because this entity is already trained, you do not need to add example utterances containing percentage to the application intents. Percentage entity is supported in [many cultures](luis-reference-prebuilt-entities.md). 

## Types of percentage
Percentage is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-Numbers.yaml#L114) GitHub repository

## Resolution for prebuilt percentage entity
The following example shows the resolution of the **builtin.percentage** entity.

```json
{
  "query": "set a trigger when my stock goes up 2%",
  "topScoringIntent": {
    "intent": "SetTrigger",
    "score": 0.971157849
  },
  "intents": [
    {
      "intent": "SetTrigger",
      "score": 0.971157849
    }
  ],
  "entities": [
    {
      "entity": "2%",
      "type": "builtin.percentage",
      "startIndex": 36,
      "endIndex": 37,
      "resolution": {
        "value": "2%"
      }
    }
  ]
}
```

## Next steps

Learn about the [ordinal](luis-reference-prebuilt-ordinal.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities. 
