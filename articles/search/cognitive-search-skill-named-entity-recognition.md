---
title: Named Entity Recognition cognitive search skill - Azure Search
description: Extract named entities for person, location and organization from text in an Azure Search cognitive search pipeline.
services: search
manager: pablocas
author: luiscabrer

ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: conceptual
ms.date: 02/22/2019
ms.author: luisca
ms.custom: seodec2018
---

#	 Named Entity Recognition cognitive skill

The **Named Entity Recognition** skill extracts named entities from text. Available entities include the types `person`, `location` and `organization`.

> [!IMPORTANT]
> Named entity recognition skill is deprecated, replaced by [Microsoft.Skills.Text.EntityRecognitionSkill](cognitive-search-skill-entity-recognition.md). Support stops on Feburary 15, 2019. Follow the recommendations in [Deprecated Cognitive Search Skills](cognitive-search-skill-deprecated.md) to migrate to a supported skill.

> [!NOTE]
> Starting December 21, 2018, you can [attach a Cognitive Services resource](cognitive-search-attach-cognitive-services.md) with an Azure Search skillset. This allows us to start charging for skillset execution. On this date, we also began charging for image extraction as part of the document-cracking stage. Text extraction from documents continues to be offered at no additional cost.
>
> [Built-in cognitive skill](cognitive-search-predefined-skills.md) execution is charged at the [Cognitive Services pay-as-you go price](https://azure.microsoft.com/pricing/details/cognitive-services), at the same rate as if you had performed the task directly. Image extraction is an Azure Search charge, currently offered at preview pricing. For details, see the [Azure Search pricing page](https://go.microsoft.com/fwlink/?linkid=2042400) or [How billing works](search-sku-tier.md#how-billing-works).

## @odata.type  
Microsoft.Skills.Text.NamedEntityRecognitionSkill

## Data limits
The maximum size of a record should be 50,000 characters as measured by `String.Length`. If you need to break up your data before sending it to the key phrase extractor, consider using the [Text Split skill](cognitive-search-skill-textsplit.md).

## Skill parameters

Parameters are case-sensitive.

| Parameter name	 | Description |
|--------------------|-------------|
| categories	| Array of categories that should be extracted.  Possible category types: `"Person"`, `"Location"`, `"Organization"`. If no category is provided, all types are returned.|
|defaultLanguageCode |	Language code of the input text. The following languages are supported: `de, en, es, fr, it`|
| minimumPrecision	| A number between 0 and 1. If the precision is lower than this value, the entity is not returned. The default is 0.|

## Skill inputs

| Input name	  | Description                   |
|---------------|-------------------------------|
| languageCode	| Optional. Default is `"en"`.  |
| text          | The text to analyze.          |

## Skill outputs

| Output name	  | Description                   |
|---------------|-------------------------------|
| persons	   | An array of strings where each string represents the name of a person. |
| locations  | An array of strings where each string represents a location. |
| organizations  | An array of strings where each string represents an organization. |
| entities | An array of complex types. Each complex type includes the following fields: <ul><li>category (`"person"`, `"organization"`, or `"location"`)</li> <li>value (the actual entity name)</li><li>offset (The location where it was found in the text)</li><li>confidence (A value between 0 and 1 that represents that confidence that the value is an actual entity)</li></ul> |

##	Sample definition

```json
  {
    "@odata.type": "#Microsoft.Skills.Text.NamedEntityRecognitionSkill",
    "categories": [ "Person", "Location", "Organization"],
    "defaultLanguageCode": "en",
    "inputs": [
      {
        "name": "text",
        "source": "/document/content"
      }
    ],
    "outputs": [
      {
        "name": "persons",
        "targetName": "people"
      }
    ]
  }
```
##	Sample input

```json
{
    "values": [
      {
        "recordId": "1",
        "data":
           {
             "text": "This is the loan application for Joe Romero, he is a Microsoft employee who was born in Chile and then moved to Australia… Ana Smith is provided as a reference.",
             "languageCode": "en"
           }
      }
    ]
}
```

##	Sample output

```json
{
  "values": [
    {
      "recordId": "1",
      "data" : 
      {
        "persons": [ "Joe Romero", "Ana Smith"],
        "locations": ["Chile", "Australia"],
        "organizations":["Microsoft"],
        "entities":  
        [
          {
            "category":"person",
            "value": "Joe Romero",
            "offset": 33,
            "confidence": 0.87
          },
          {
            "category":"person",
            "value": "Ana Smith",
            "offset": 124,
            "confidence": 0.87
          },
          {
            "category":"location",
            "value": "Chile",
            "offset": 88,
            "confidence": 0.99
          },
          {
            "category":"location",
            "value": "Australia",
            "offset": 112,
            "confidence": 0.99
          },
          {
            "category":"organization",
            "value": "Microsoft",
            "offset": 54,
            "confidence": 0.99
          }
        ]
      }
    }
  ]
}
```


## Error cases
If the language code for the document is unsupported, an error is returned and no entities are extracted.

## See also

+ [Predefined skills](cognitive-search-predefined-skills.md)
+ [How to define a skillset](cognitive-search-defining-skillset.md)
+ [Entity Recognition Skill](cognitive-search-skill-entity-recognition.md)
