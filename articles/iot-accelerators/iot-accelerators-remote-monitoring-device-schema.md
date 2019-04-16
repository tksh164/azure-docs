---
title: Device schema in remote monitoring solution - Azure | Microsoft Docs
description: This article describes the JSON schema that defines a simulated device in the remote monitoring solution.
author: dominicbetts
manager: philmea
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 12/18/2018
ms.topic: conceptual
---

# Understand the device model schema

You can use simulated devices in the Remote Monitoring solution to test its behavior. The Remote Monitoring solution includes a device simulation service to run simulated devices. When you deploy the Remote Monitoring solution, a collection of simulated devices is provisioned automatically. You can customize the existing simulated devices or create your own.

This article describes the device model schema that specifies the capabilities and behavior of a simulated device. The device model is stored in a JSON file.

> [!NOTE]
> This device model schema is only for simulated devices hosted in the device simulation service. If you want to create a real device, see [Connect your device to the Remote Monitoring solution accelerator](iot-accelerators-connecting-devices.md).

The following articles are related to the current article:

* [Implement the device model behavior](iot-accelerators-remote-monitoring-device-behavior.md) describes the JavaScript files you use to implement the behavior of a simulated device.
* [Create a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md) puts it all together and shows you how to deploy a new simulated device type to your solution.

In this article, you learn how to:

>[!div class="checklist"]
> * Use a JSON file to define a simulated device model
> * Specify the properties the simulated device
> * Specify the telemetry the simulated device sends
> * Specify the cloud-to-device methods the device responds to

[!INCLUDE [iot-accelerators-device-schema](../../includes/iot-accelerators-device-schema.md)]

## Next steps

This article described how to create your own custom simulated device model. This article showed you how to:

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * Use a JSON file to define a simulated device model
> * Specify the properties the simulated device
> * Specify the telemetry the simulated device sends
> * Specify the cloud-to-device methods the device responds to

Now that you've learned about the JSON schema, the suggested next step is to learn how to [implement the behavior of your simulated device](iot-accelerators-remote-monitoring-device-behavior.md).

For more developer information about the Remote Monitoring solution, see:

* [Developer Reference Guide](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
* [Developer Troubleshooting Guide](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Troubleshooting-Guide)
