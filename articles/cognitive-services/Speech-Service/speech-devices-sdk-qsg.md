---
title: Get started with the Speech Devices SDK - Speech Services
titleSuffix: Azure Cognitive Services
description: Prerequisites and instructions for getting started with the Speech Devices SDK.
services: cognitive-services
author: erhopf
manager: nitinme

ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 12/06/2018
ms.author: erhopf
ms.custom: seodec18
---

# Get started with the Speech Devices SDK

This article describes how to configure your development PC and Speech device development kit for developing speech-enabled devices by using the Speech Devices SDK. Then you build and deploy a sample application to the device.

The source code for the sample application is included with the Speech Devices SDK. It's also [available on GitHub](https://github.com/Azure-Samples/Cognitive-Services-Speech-Devices-SDK).

## Prerequisites

Before you begin developing with the Speech Devices SDK, gather the information and software you need:

* Get a [development kit from ROOBO](http://ddk.roobo.com/). Kits are available with linear or circular microphone array configurations. Choose the correct configuration for your needs.

    |Development kit configuration|Speaker location|
    |-----------------------------|------------|
    |Circular|Any direction from the device|
    |Linear|In front of the device|

* Get the latest version of the Speech Devices SDK, which includes an Android sample app, from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/). Extract the .zip file to a local folder, like C:\SDSDK.

* Install [Android Studio](https://developer.android.com/studio/) and [Vysor](https://vysor.io/download/) on your PC.

* Get a [Speech Services subscription key](get-started.md). You can get a 30-day free trial or get a key from your Azure dashboard.

* If you want to use the Speech Services' intent recognition, subscribe to the [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) (LUIS) and [get a subscription key](https://docs.microsoft.com/azure/cognitive-services/luis/azureibizasubscription).

    You can [create a simple LUIS model](https://docs.microsoft.com/azure/cognitive-services/luis/) or use the sample LUIS model, LUIS-example.json. The sample LUIS model is available from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/). To upload your model's JSON file to the [LUIS portal](https://www.luis.ai/home), select **Import new app**, and then select the JSON file.

## Set up the development kit

1. The development kit has two micro USB connectors. The left connector is to power the development kit and is highlighted as Power in the image below. The right one is to control it, and is marked Debug in the image.

    ![Connecting the dev kit](media/speech-devices-sdk/qsg-1.png)

1. Power the development kit by using a micro USB cable to connect the power port to a PC or power adapter. A green power indicator will light up under the top board.

1. To control the development kit connect the debug port to a computer by using a second micro USB cable. It is essential to use a high quality cable to ensure reliable communications.

1. Orient your development kit for either the circular or linear configuration.

    |Development kit configuration|Orientation|
    |-----------------------------|------------|
    |Circular|Upright, with microphones facing the ceiling|
    |Linear|On its side, with microphones facing you (shown in the following image)|

    ![Linear dev kit orientation](media/speech-devices-sdk/qsg-2.png)

1. Install the certificates and set the permissions of the sound device. Type the following commands in a Command Prompt window:

   ```
   adb push C:\SDSDK\Android-Sample-Release\scripts\roobo_setup.sh /data/
   adb shell
   cd /data/
   chmod 777 roobo_setup.sh
   ./roobo_setup.sh
   exit
   ```

    > [!NOTE]
    > These commands use the Android Debug Bridge, `adb.exe`, which is part of the Android Studio installation. This tool is located in C:\Users\[user name]\AppData\Local\Android\Sdk\platform-tools. You can add this directory to your path to make it more convenient to invoke `adb`. Otherwise, you must specify the full path to your installation of adb.exe in every command that invokes `adb`.
    >
    > If you see an error `no devices/emulators found` then check your USB cable is conected and is a high quality cable. You can use `adb devices` to check that your computer can talk to the development kit as it will return a list of devices.

    > [!TIP]
    > Mute your PC's microphone and speaker to be sure you are working with the development kit's microphones. This way, you won't accidentally trigger the device with audio from the PC.

1.	Start Vysor on your computer.

    ![Vysor](media/speech-devices-sdk/qsg-3.png)

1.	Your device should be listed under **Choose a device**. Select the **View** button next to the device.

1.	Connect to your wireless network by selecting the folder icon, and then select **Settings** > **WLAN**.

    ![Vysor WLAN](media/speech-devices-sdk/qsg-4.png)

    > [!NOTE]
    > If your company has policies about connecting devices to its Wi-Fi system, you need to obtain the MAC address and contact your IT department about how to connect it to your company's Wi-Fi.
    >
    > To find the MAC address of the dev kit, select the file folder icon on the desktop of the dev kit.
    >
    >  ![Vysor file folder](media/speech-devices-sdk/qsg-10.png)
    >
    > Select **Settings**. Search for "mac address", and then select **Mac address** > **Advanced WLAN**. Write down the MAC address that appears near the bottom of the dialog box.
    >
    > ![Vysor MAC address](media/speech-devices-sdk/qsg-11.png)
    >
    > Some companies might have a time limit on how long a device can be connected to their Wi-Fi system. You might need to extend the dev kit's registration with your Wi-Fi system after a specific number of days.
    >
    > If you want to attach a speaker to the dev kit, you can connect it to the audio line out. You should choose a good-quality, 3.5-mm speaker.
    >
    > ![Vysor audio](media/speech-devices-sdk/qsg-14.png)

## Run a sample application

To run the ROOBO tests and validate your development kit setup, build and install the sample application:

1. Start Android Studio.

1. Select **Open an existing Android Studio project**.

   ![Android Studio - Open an existing project](media/speech-devices-sdk/qsg-5.png)

1. Go to C:\SDSDK\Android-Sample-Release\example. Select **OK** to open the example project.

1. Add your Speech subscription key to the source code. If you want to try intent recognition, also add your [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) subscription key and application ID.

   Your keys and application information go in the following lines in the source file MainActivity.java:

   ```java
   // Subscription
   private static final String SpeechSubscriptionKey = "[your speech key]";
   private static final String SpeechRegion = "westus";
   private static final String LuisSubscriptionKey = "[your LUIS key]";
   private static final String LuisRegion = "westus2.api.cognitive.microsoft.com";
   private static final String LuisAppId = "[your LUIS app ID]"
   ```

1. The default wake word (keyword) is "Computer". You can also try one of the other provided wake words, like "Machine" or "Assistant". The resource files for these alternate wake words are in the Speech Devices SDK, in the keyword folder. For example, C:\SDSDK\Android-Sample-Release\keyword\Computer contains the files used for the wake word "Computer".

    You can also [create a custom wake word](speech-devices-sdk-create-kws.md).

    To use a new wake word, update the following two lines of MainActivity.java, and copy the wake word package to your app. For example to use the wake word 'Machine' from the wake word package kws-machine.zip:

   * Copy the wake word package into the folder “C:\SDSDK\Android-Sample-Release\example\app\src\main\assets\”.
   * Update the MainActivity.java with the keyword and the package name: 
    
     ```java
     private static final String Keyword = "Machine";
     private static final String KeywordModel = "kws-machine.zip" // set your own keyword package name.
     ```

1. Update the following lines, which contain the microphone array geometry settings:

   ```java
   private static final String DeviceGeometry = "Circular6+1";
   private static final String SelectedGeometry = "Circular6+1";
   ```
   The following table describes the available values:

   |Variable|Meaning|Available values|
   |--------|-------|----------------|
   |`DeviceGeometry`|Physical mic configuration|For a circular dev kit: `Circular6+1` |
   |||For a linear dev kit: `Linear4`|
   |`SelectedGeometry`|Software mic configuration|For a circular dev kit that uses all mics: `Circular6+1`|
   |||For a circular dev kit that uses four mics: `Circular3+1`|
   |||For a linear dev kit that uses all mics: `Linear4`|
   |||For a linear dev kit that uses two mics: `Linear2`|


1. To build the application, on the **Run** menu, select **Run 'app'**. The **Select Deployment Target** dialog box appears.

1. Select your device, and then select **OK** to deploy the application to the device.

    ![Select Deployment Target dialog box](media/speech-devices-sdk/qsg-7.png)

1. The Speech Devices SDK example application starts and displays the following options:

   ![Sample Speech Devices SDK example application and options](media/speech-devices-sdk/qsg-8.png)

1. Experiment!

## Troubleshooting

### Certificate failures

If you get certificate failures when using the Speech Services, make sure that your device has the correct date and time:

1. Go to **Settings**. Under **System**, select **Date & time**.

    ![Under Settings, select Date & time](media/speech-devices-sdk/qsg-12.png)

1. Keep the **Automatic date & time** option selected. Under **Select time zone**, select your current time zone.

    ![Select date and time zone options](media/speech-devices-sdk/qsg-13.png)

    When you see that the dev kit's time matches the time on your PC, the dev kit is connected to the internet.

    For more development information, see the [ROOBO development guide](http://dwn.roo.bo/server_upload/ddk/ROOBO%20Dev%20Kit-User%20Guide.pdf).

### Audio

ROOBO provides a tool that captures all audio to flash memory. It might help you troubleshoot audio issues. A version of the tool is provided for each development kit configuration. On the  [ROOBO site](http://ddk.roobo.com/), select your device, and then select the **ROOBO Tools** link at the bottom of the page.
