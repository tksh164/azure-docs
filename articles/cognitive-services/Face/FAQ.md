---
title: Frequently asked questions - Face API
titlesuffix: Azure Cognitive Services
description: Here are answers to the most popular questions about the Face API Service.
services: cognitive-services
author: SteveMSFT
manager: nitinme

ms.service: cognitive-services
ms.subservice: face-api
ms.topic: conceptual
ms.date: 01/26/2017
ms.author: sbowles
---

# Face API Frequently Asked Questions

> [!TIP]
> If you can't find answers to your questions in this FAQ, try asking the Face API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).

-----
**Question**: What factors can reduce Face API's accuracy for Recognition, Verification, or Find Similar?

**Answer**: Generally it is the same cases where humans have difficulty identifying someone including:
* Obstructions blocking one or both eyes
* Harsh lighting (for example, severe backlighting)
* Changes to hair style or facial hair
* Changes due to age
* Extreme facial expressions (for example, screaming)

Face API is often successful in challenging cases like the above, but accuracy can be reduced. To make recognition more robust and address these challenges, train your Persons with photos that include a diversity of angles and lighting.

-----
**Question**:  I am passing the binary image data in but I get an "Invalid face image" error.

**Answer**:  This error implies that the algorithm had an issue parsing the image. Causes include:
* The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.
* Image file size should be no larger than 4 MB
* The detectable face size range is 36x36 to 4096x4096 pixels. Faces out of this range won't be detected
* Some faces may not be detected because of technical challenges, for example large face angles (head-pose), large occlusion. Frontal and near-frontal faces have the best results

-----
