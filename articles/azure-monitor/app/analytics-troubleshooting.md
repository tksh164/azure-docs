---
title: Troubleshoot Analytics in Azure Application Insights | Microsoft Docs
description: 'Problems with Application Insights analytics? Start here. '
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm

ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 02/08/2019
ms.author: mbullwin

---
# Troubleshoot Analytics in Application Insights
Problems with [Application Insights Analytics](analytics.md)? Start here. Analytics is the powerful search tool of Azure Application Insights.

## Limits
* At present, query results are limited to just over a week of past data.
* Browsers we test on: latest editions of Chrome, Microsoft Edge, and Internet Explorer.

## Known incompatible browser extensions
* Ghostery

Disable the extension or use a different browser.

## <a name="e-a"></a> "Unexpected error"
![Unexpected error screen](media/analytics-troubleshooting/010.png)

Internal error occurred during portal runtime unhandled exception.

* Clean the browser's cache.

## <a name="e-b"></a>403 ... please try to reload
![403 ... please try to reload](media/analytics-troubleshooting/020.png)

An authentication related error occurred (during authentication or during access token generation). The portal may have no way to  recover without changing browser settings.

* Verify [third party cookies are enabled](#cookies) in the browser. 

## <a name="authentication"></a>403 ... verify security zone
![403 ...verify security zone](media/analytics-troubleshooting/030.png)

An authentication related error occurred (during authentication or during access token generation). The portal may have no way to  recover without changing browser settings.

1. Verify [third party cookies are enabled](#cookies) in the browser. 
2. Did you use a favorite, bookmark or saved link to open the Analytics portal? Are you signed in with different credentials than you used when you saved the link?
3. Try using an in-private/incognito browser window (after closing all such windows). You'll have to provide your credentials. 
4. Open another (ordinary) browser window and go to [Azure](https://portal.azure.com). Sign out. Then open your link and sign in with the correct credentials.
5. Microsoft Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.
   
    Verify both [Analytics portal](https://portal.azure.com) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:
   
   * In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:
     
     ![Internet Options dialog, adding a site to Trusted Sites](media/analytics-troubleshooting/033.png)
     
     In the Websites list, if any of the following URLs are included, make sure that the others are included also:
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Resource not found
![404 ... resource not found](media/analytics-troubleshooting/040.png)

Application resource was deleted from Application Insights and isn't available anymore. This can happen if you saved the URL to the Analytics page.

## <a name="e-e"></a>403 ... No authorization
![403 ... not authorized](media/analytics-troubleshooting/050.png)

You don't have permission to open this application in Analytics.

* Did you get the link from someone else? Ask them to make sure you are in the [readers or contributors for this resource group](../../azure-monitor/app/resources-roles-access-control.md).
* Did you save the link using different credentials? Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.

## <a name="html-storage"></a>403 ... HTML5 Storage
Our portal uses HTML5 localStorage and sessionStorage.

* Chrome: Settings, privacy, content settings.
* Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage

![403 ... try to enable HTML5 storage](media/analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Subscription not found
![404 ... Subscription not found](media/analytics-troubleshooting/070.png)

The URL is invalid. 

* Open the app resource in [Application Insights portal](https://portal.azure.com). Then use the Analytics button.

## <a name="e-h"></a>404 ... page doesn't exist
![404 ... Page does not exist](media/analytics-troubleshooting/080.png)

The URL is invalid.

* Open the app resource in [Application Insights portal](https://portal.azure.com). Then use the Analytics button.

## <a name="cookies"></a>Enable third-party cookies
  See [how to disable third party cookies](https://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.


[!INCLUDE [app-insights-analytics-footer](../../../includes/app-insights-analytics-footer.md)]

