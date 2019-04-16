---
title: Phone number Prebuilt entities
titleSuffix: Azure
description: This article contains phone number prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 03/04/2019
ms.author: diberry
---

# Phonenumber prebuilt entity for a LUIS app
The `phonenumber` entity extracts a variety of phone numbers including country code. Because this entity is already trained, you do not need to add example utterances to the application. The `phonenumber` entity is supported in `en-us` culture only. 

## Types of phonenumber
Phonenumber is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-PhoneNumbers.yaml) GitHub repository

## Resolution for prebuilt phonenumber entity
The following example shows the resolution of the **builtin.phonenumber** entity.

```json
{
  "query": "my mobile is 00 44 161 1234567",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.8448457
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.8448457
    }
  ],
  "entities": [
    {
      "entity": "00 44 161 1234567",
      "type": "builtin.phonenumber",
      "startIndex": 13,
      "endIndex": 29,
      "resolution": {
        "value": "00 44 161 1234567"
      }
    }
  ]
}
```


## Next steps

Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities. 
