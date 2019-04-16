---
title: Image Analysis cognitive search skill - Azure Search
description: Extract semantic text through image analysis using the ImageAnalysis cognitive skill in an Azure Search enrichment pipeline.
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
#	Image Analysis cognitive skill

The **Image Analysis** skill extracts a rich set of visual features based on the image content. For example, you can generate a caption from an image, generate tags, or identify celebrities and landmarks. This skill uses the machine learning models provided by [Computer Vision](https://docs.microsoft.com/azure/cognitive-services/computer-vision/home) in Cognitive Services. 

> [!NOTE]
> Starting December 21, 2018, you can [attach a Cognitive Services resource](cognitive-search-attach-cognitive-services.md) with an Azure Search skillset. This allows us to start charging for skillset execution. On this date, we also began charging for image extraction as part of the document-cracking stage. Text extraction from documents continues to be offered at no additional cost.
>
> [Built-in cognitive skill](cognitive-search-predefined-skills.md) execution is charged at the [Cognitive Services pay-as-you go price](https://azure.microsoft.com/pricing/details/cognitive-services), at the same rate as if you had performed the task directly. Image extraction is an Azure Search charge, currently offered at preview pricing. For details, see the [Azure Search pricing page](https://go.microsoft.com/fwlink/?linkid=2042400) or [How billing works](search-sku-tier.md#how-billing-works).

## @odata.type  
Microsoft.Skills.Vision.ImageAnalysisSkill 

## Skill parameters

Parameters are case-sensitive.

| Parameter name	 | Description |
|--------------------|-------------|
| defaultLanguageCode	|  A string indicating the language to return. The service returns recognition results in a specified language. If this parameter is not specified, the default value is "en". <br/><br/>Supported languages are: <br/>*en* - English (default) <br/> *zh* - Simplified Chinese|
|visualFeatures |	An array of strings indicating the visual feature types to return. Valid visual feature types include:  <ul><li> *categories* - categorizes image content according to a taxonomy defined in the Cognitive Services [documentation](https://docs.microsoft.com/azure/cognitive-services/computer-vision/category-taxonomy).</li><li> *tags* - tags the image with a detailed list of words related to the image content.</li><li>*description* - describes the image content with a complete English sentence.</li><li>*faces* - detects if faces are present. If present, generates coordinates, gender, and age.</li><li>	*imageType* - detects if image is clip art or a line drawing.</li><li>	*color* - determines the accent color, dominant color, and whether an image is black&white.</li><li>*adult* - detects if the image is pornographic in nature (depicts nudity or a sex act). Sexually suggestive content is also detected.</li></ul> Names of visual features are case-sensitive.|
| details	| An array of strings indicating which domain-specific details to return. Valid visual feature types include: <ul><li>*celebrities* - identifies celebrities if detected in the image.</li><li>*landmarks* - identifies landmarks if detected in the image.</li></ul>
 |

## Skill inputs

| Input name	  | Description                                          |
|---------------|------------------------------------------------------|
| image         | Complex Type. Currently only works with "/document/normalized_images" field, produced by the Azure Blob indexer when ```imageAction``` is set to a value other than ```none```. See the [sample](#sample-output) for more information.|



##	Sample definition
```json
{
    "@odata.type": "#Microsoft.Skills.Vision.ImageAnalysisSkill",
    "context": "/document/normalized_images/*",
    "visualFeatures": [
        "Tags",
        "Faces",
        "Categories",
        "Adult",
        "Description",
        "ImageType",
        "Color"
    ],
    "defaultLanguageCode": "en",
    "inputs": [
        {
            "name": "image",
            "source": "/document/normalized_images/*"
        }
    ],
    "outputs": [
        {
            "name": "categories",
            "targetName": "myCategories"
        },
        {
            "name": "tags",
            "targetName": "myTags"
        },
        {
            "name": "description",
            "targetName": "myDescription"
        },
        {
            "name": "faces",
            "targetName": "myFaces"
        },
        {
            "name": "imageType",
            "targetName": "myImageType"
        },
        {
            "name": "color",
            "targetName": "myColor"
        },
        {
            "name": "adult",
            "targetName": "myAdultCategory"
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
            "data": {
                "image": {
                    "data": "BASE64 ENCODED STRING OF A JPEG IMAGE",
                    "width": 500,
                    "height": 300,
                    "originalWidth": 5000,
                    "originalHeight": 3000,
                    "rotationFromOriginal": 90,
                    "contentOffset": 500
                }
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
            "data": {
                "categories": [
                    {
                        "name": "abstract_",
                        "score": 0.00390625
                    },
                    {
                        "name": "people_",
                        "score": 0.83984375,
                        "detail": {
                            "celebrities": [
                                {
                                    "name": "Satya Nadella",
                                    "faceBoundingBox": {
                                        "left": 597,
                                        "top": 162,
                                        "width": 248,
                                        "height": 248
                                    },
                                    "confidence": 0.999028444
                                }
                            ],
                            "landmarks": [
                                {
                                    "name": "Forbidden City",
                                    "confidence": 0.9978346
                                }
                            ]
                        }
                    }
                ],
                "adult": {
                    "isAdultContent": false,
                    "isRacyContent": false,
                    "adultScore": 0.0934349000453949,
                    "racyScore": 0.068613491952419281
                },
                "tags": [
                    {
                        "name": "person",
                        "confidence": 0.98979085683822632
                    },
                    {
                        "name": "man",
                        "confidence": 0.94493889808654785
                    },
                    {
                        "name": "outdoor",
                        "confidence": 0.938492476940155
                    },
                    {
                        "name": "window",
                        "confidence": 0.89513939619064331
                    }
                ],
                "description": {
                    "tags": [
                        "person",
                        "man",
                        "outdoor",
                        "window",
                        "glasses"
                    ],
                    "captions": [
                        {
                            "text": "Satya Nadella sitting on a bench",
                            "confidence": 0.48293603002174407
                        }
                    ]
                },
                "requestId": "0dbec5ad-a3d3-4f7e-96b4-dfd57efe967d",
                "metadata": {
                    "width": 1500,
                    "height": 1000,
                    "format": "Jpeg"
                },
                "faces": [
                    {
                        "age": 44,
                        "gender": "Male",
                        "faceBoundingBox": {
                            "left": 593,
                            "top": 160,
                            "width": 250,
                            "height": 250
                        }
                    }
                ],
                "color": {
                    "dominantColorForeground": "Brown",
                    "dominantColorBackground": "Brown",
                    "dominantColors": [
                        "Brown",
                        "Black"
                    ],
                    "accentColor": "873B59",
                    "isBwImg": false
                    },
                "imageType": {
                    "clipArtType": 0,
                    "lineDrawingType": 0
                }
            }
        }
    ]
}
```


## Error cases
In the following error cases, no elements are extracted.

| Error Code | Description |
|------------|-------------|
| NotSupportedLanguage | The language provided is not supported. |
| InvalidImageUrl | Image URL is badly formatted or not accessible.|
| InvalidImageFormat | Input data is not a valid image. |
| InvalidImageSize | Input image is too large. |
| NotSupportedVisualFeature  | Specified feature type is not valid. |
| NotSupportedImage | Unsupported image, for example, child pornography. |
| InvalidDetails | Unsupported domain-specific model. |

## See also

+ [Predefined skills](cognitive-search-predefined-skills.md)
+ [How to define a skillset](cognitive-search-defining-skillset.md)
+ [Create Indexer (REST)](https://docs.microsoft.com/rest/api/searchservice/create-indexer)
