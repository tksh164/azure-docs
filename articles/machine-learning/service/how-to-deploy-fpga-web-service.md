---
title: Deploy models on FPGAs
titleSuffix: Azure Machine Learning service
description: Learn how to deploy a web service with a model running on an FPGA with Azure Machine Learning service for ultra-low latency inferencing. 
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual

ms.reviewer: jmartens
ms.author: tedway
author: tedway
ms.date: 1/29/2019
ms.custom: seodec18
---

# Deploy a model as a web service on an FPGA with Azure Machine Learning service

You can deploy a model as a web service on [field programmable gate arrays (FPGAs)](concept-accelerate-with-fpgas.md).  Using FPGAs provides ultra-low latency inferencing, even with a single batch size.  These models are currently available:
  - ResNet 50
  - ResNet 152
  - DenseNet-121
  - VGG-16   

## Prerequisites

- If you don’t have an Azure subscription, create a free account before you begin. Try the [free or paid version of Azure Machine Learning service](https://aka.ms/AMLFree) today.

- An Azure Machine Learning service workspace and the Azure Machine Learning SDK for Python installed. Learn how to get these prerequisites using the [How to configure a development environment](how-to-configure-environment.md) document.
 
  - Your workspace needs to be in the *East US 2* region.

  - Install the contrib extras:

    ```shell
    pip install --upgrade azureml-sdk[contrib]
    ```

  - Currently only tensorflow version<=1.10 is supported, so install it after all other installations are complete:

    ```shell
    pip install "tensorflow==1.10"
    ```

## Create and deploy your model
Create a pipeline to preprocess the input image, make it a feature using ResNet 50 on an FPGA, and then run the features through a classifier trained on the ImageNet data set.

Follow the instructions to:

* Define the model pipeline
* Deploy the model
* Consume the deployed model
* Delete deployed services

> [!IMPORTANT]
> To optimize latency and throughput, your client should be in the same Azure region as the endpoint.  Currently the APIs are created in the East US Azure region.



### Preprocess image
The first stage of the pipeline is to preprocess the images.

```python
import os
import tensorflow as tf

# Input images as a two-dimensional tensor containing an arbitrary number of images represented a strings
import azureml.contrib.brainwave.models.utils as utils
in_images = tf.placeholder(tf.string)
image_tensors = utils.preprocess_array(in_images)
print(image_tensors.shape)
```

### Add Featurizer
Initialize the model and download a TensorFlow checkpoint of the quantized version of ResNet50 to be used as a featurizer.

```python
from azureml.contrib.brainwave.models import QuantizedResnet50
model_path = os.path.expanduser('~/models')
model = QuantizedResnet50(model_path, is_frozen = True)
feature_tensor = model.import_graph_def(image_tensors)
print(model.version)
print(feature_tensor.name)
print(feature_tensor.shape)
```

### Add Classifier
This classifier has been trained on the ImageNet data set.

```python
classifier_output = model.get_default_classifier(feature_tensor)
```

### Create service definition
Now that you have defined the image preprocessing, featurizer, and classifier that runs on the service, you can create a service definition. The service definition is a set of files generated from the model that is deployed to the FPGA service. The service definition consists of a pipeline. The pipeline is a series of stages that are run in order.  TensorFlow stages, Keras stages, and BrainWave stages are supported.  The stages are run in order on the service, with the output of each stage becoming the input into the subsequent stage.

To create a TensorFlow stage, specify a session containing the graph (in this case default graph is used) and the input and output tensors to this stage.  This information is used to save the graph so that it can be run on the service.

```python
from azureml.contrib.brainwave.pipeline import ModelDefinition, TensorflowStage, BrainWaveStage

save_path = os.path.expanduser('~/models/save')
model_def_path = os.path.join(save_path, 'model_def.zip')

model_def = ModelDefinition()
with tf.Session() as sess:
    model_def.pipeline.append(TensorflowStage(sess, in_images, image_tensors))
    model_def.pipeline.append(BrainWaveStage(sess, model))
    model_def.pipeline.append(TensorflowStage(sess, feature_tensor, classifier_output))
    model_def.save(model_def_path)
    print(model_def_path)
```

### Deploy model
Create a service from the service definition.  Your workspace needs to be in the East US 2 location.

```python
from azureml.core import Workspace

ws = Workspace.from_config()
print(ws.name, ws.resource_group, ws.location, ws.subscription_id, sep = '\n')

from azureml.core.model import Model
model_name = "resnet-50-rtai"
registered_model = Model.register(ws, model_def_path, model_name)

from azureml.core.webservice import Webservice
from azureml.exceptions import WebserviceException
from azureml.contrib.brainwave import BrainwaveWebservice, BrainwaveImage
service_name = "imagenet-infer"
service = None
try:
    service = Webservice(ws, service_name)
except WebserviceException:
    image_config = BrainwaveImage.image_configuration()
    deployment_config = BrainwaveWebservice.deploy_configuration()
    service = Webservice.deploy_from_model(ws, service_name, [registered_model], image_config, deployment_config)
    service.wait_for_deployment(True)
```

### Test the service
To send an image to the API and test the response, add a mapping from the output class ID to the ImageNet class name.

```python
import requests
classes_entries = requests.get("https://raw.githubusercontent.com/Lasagne/Recipes/master/examples/resnet50/imagenet_classes.txt").text.splitlines()
```

Call your service and replace the "your-image.jpg" file name below with an image from your machine. 

```python
with open('your-image.jpg') as f:
    results = service.run(f)
# map results [class_id] => [confidence]
results = enumerate(results)
# sort results by confidence
sorted_results = sorted(results, key=lambda x: x[1], reverse=True)
# print top 5 results
for top in sorted_results[:5]:
    print(classes_entries[top[0]], 'confidence:', top[1])
``` 

### Clean up service
Delete the service.

```python
service.delete()
    
registered_model.delete()
```

## Secure FPGA web services

For information on securing FPGA web services, see the [Secure web services](how-to-secure-web-service.md) document.


## Next steps

Learn how to [Consume a ML Model deployed as a web service](how-to-consume-web-service.md).
