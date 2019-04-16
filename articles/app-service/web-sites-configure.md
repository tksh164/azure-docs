---
title: Configure apps - Azure App Service
description: How to configure an app in Azure App Service
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''

ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: cephalin
ms.custom: seodec18

---
# Configure apps in Azure App Service

This topic explains how to configure a web app, mobile back end, or API app using the [Azure Portal].

## Application settings
1. In the [Azure Portal], open the blade for the app.
2. Click **Application settings**.

![Application Settings][configure01]

The **Application settings** blade has settings grouped under several categories.

### General settings
**Framework versions**. Set these options if your app uses any these frameworks: 

* **.NET Framework**: Set the .NET framework version. 
* **PHP**: Set the PHP version, or **OFF** to disable PHP. 
* **Java**: Select the Java version or **OFF** to disable Java. Use the **Web Container** option to choose between Tomcat and Jetty versions.
* **Python**: Select the Python version, or **OFF** to disable Python.

For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.

<a name="platform"></a>
**Platform**. Selects whether your app runs in a 32-bit or 64-bit environment. The 64-bit environment requires Basic or Standard tier. Free and Shared tier always run in a 32-bit environment.

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

**Web Sockets**. Set **ON** to enable the WebSocket protocol; for example, if your app uses [ASP.NET SignalR] or [socket.io](https://socket.io/).

<a name="alwayson"></a>
**Always On**. By default, apps are unloaded if they are idle for some period of time. This lets the system conserve resources. In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time. If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.

**Managed Pipeline Version**. Sets the IIS [pipeline mode]. Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.

**HTTP Version**. Set to **2.0** to enable support for [HTTPS/2](https://wikipedia.org/wiki/HTTP/2) protocol. 

> [!NOTE]
> Most modern browsers support HTTP/2 protocol over TLS only, while non-encrypted traffic continues to use HTTP/1.1. To ensure that client browsers connect to your app with HTTP/2, either [buy an App Service Certificate](web-sites-purchase-ssl-web-site.md) for your app's custom domain or [bind a third party certificate](app-service-web-tutorial-custom-ssl.md).

**ARR Affinity**. In an app that's scaled out to multiple VM instances, ARR Affinity cookies guarantee that the client is routed to the same instance for the life of the session. To improve the performance of stateless applications, set this option to **Off**.   

**Auto Swap**. If you enable Auto Swap for a deployment slot, App Service will automatically swap the app into production when you push an update to that slot. For more information, see [Deploy to staging slots for apps in Azure App Service](deploy-staging-slots.md).

### Debugging
**Remote Debugging**. Enables remote debugging. When enabled, you can use the remote debugger in Visual Studio to connect directly to your app. Remote debugging will remain enabled for 48 hours. 

### App settings
This section contains name/value pairs that your app will load on start up. 

* For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings. 
* For App Service on Linux or Web App for Containers, if you have nested json key structure in your name like `ApplicationInsights:InstrumentationKey` you will need to have `ApplicationInsights__InstrumentationKey` as key name. So notice that any `:` should be replaced by `__` (i.e. double underscore).
* PHP, Python, Java and Node applications can access these settings as environment variables at runtime. For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_. Both contain the same value.

App settings are always encrypted when stored (encrypted-at-rest).

App settings can be resolved from Key Vault using [Key Vault references](app-service-key-vault-references.md).

### Connection strings
Connection strings for linked resources. 

For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name. 

For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type. The environment variable prefixes are as follows: 

* SQL Server: `SQLCONNSTR_`
* MySQL: `MYSQLCONNSTR_`
* SQL Database: `SQLAZURECONNSTR_`
* Custom: `CUSTOMCONNSTR_`

For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.

Connection strings are always encrypted when stored (encrypted-at-rest).

Connection strings can be resolved from Key Vault using [Key Vault references](app-service-key-vault-references.md).

### Default documents
The default document is the web page that is displayed at the root URL for a website.  The first matching file in the list is used. 

Apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.    

### Handler mappings
Use this area to add custom script processors to handle requests for specific file extensions. 

* **Extension**. The file extension to be handled, such as *.php or handler.fcgi. 
* **Script Processor Path**. The absolute path of the script processor. Requests to files that match the file extension will be processed by the script processor. Use the path `D:\home\site\wwwroot` to refer to your app's root directory.
* **Additional Arguments**. Optional command-line arguments for the script processor 

### Virtual applications and directories
To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root. Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.

## Enabling diagnostic logs
To enable diagnostic logs:

1. In the blade for your app, click **All settings**.
2. Click **Diagnostic logs**. 

Options for writing diagnostic logs from a web application that supports logging: 

* **Application Logging**. Writes application logs to the file system. Logging lasts for a period of 12 hours. 

**Level**. When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).

**Web server logging**. Logs are saved in the W3C extended log file format. 

**Detailed error messages**. Saves detailed error messages .htm files. The files are saved under /LogFiles/DetailedErrors. 

**Failed request tracing**. Logs failed requests to XML files. The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier. This folder contains an XSL file and one or more XML files. Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.

To view the log files, you must create FTP credentials, as follows:

1. In the blade for your app, click **All settings**.
2. Click **Deployment credentials**.
3. Enter a user name and password.
4. Click **Save**.

![Set deployment credentials][configure03]

The full FTP user name is “app\username” where *app* is the name of your app. The username is listed in the app blade, under **Essentials**.

![FTP deployment credentials][configure02]

## Other configuration tasks
### SSL
In Basic or Standard mode, you can upload SSL certificates for a custom domain. For more information, see [Enable HTTPS for an app](app-service-web-tutorial-custom-ssl.md). 

To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.

### Domain names
Add custom domain names for your app. For more information, see [Configure a custom domain name for an app in Azure App Service](app-service-web-tutorial-custom-domain.md).

To view your domain names, click **All Settings** > **Custom domains and SSL**.

### Deployments
* Set up continuous deployment. See [Using Git to deploy apps in Azure App Service](deploy-local-git.md).
* Deployment slots. See [Deploy to Staging Environments for Azure App Service].

To view your deployment slots, click **All Settings** > **Deployment slots**.

### Monitoring
In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations. A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds. An endpoint is considered available if the monitoring tests succeed from all the specified locations. 

For more information, see [How to: Monitor web endpoint status].

## Next steps
* [Configure a custom domain name in Azure App Service]
* [Enable HTTPS for an app in Azure App Service]
* [Scale an app in Azure App Service]
* [Monitoring basics in Azure App Service]
* [Change applicationHost.config settings with applicationHost.xdt](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)

<!-- URL List -->

[ASP.NET SignalR]: https://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[Deploy to Staging Environments for Azure App Service]: ./deploy-staging-slots.md
[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[How to: Monitor web endpoint status]: https://go.microsoft.com/fwLink/?LinkID=279906
[Monitoring basics in Azure App Service]: ./web-sites-monitor.md
[pipeline mode]: https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Scale an app in Azure App Service]: ./web-sites-scale.md

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
