---
title: Create Java web app - Azure App Service
description: Learn how to run web apps in App Service by deploying a basic Java app. 
services: app-service\web
documentationcenter: ''
author: rmcmurray
manager: routlaw
editor: ''

ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 04/23/2019
ms.author: cephalin;robmcm
ms.custom: mvc, devcenter
ms.custom: seodec18

---
# Create your first Java web app in Azure

Azure App Service provides a highly scalable, self-patching web hosting service. This quickstart shows how to deploy a Java web app to App Service by using the Eclipse IDE for Java EE Developers.

> [!IMPORTANT]
> Azure App Service on Linux is also an option to host Java web apps natively on Linux using managed Tomcat, Java SE, and WildFly offerings. If you're interested in getting started with App Service on Linux, see [Quickstart: Create a Java app in App Service on Linux](containers/quickstart-java.md).

When you have completed this quickstart, your application will look similar to the following illustration when you view it in a web browser:

!["Hello Azure!" example web app](./media/app-service-web-get-started-java/browse-web-app-1.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

> [!NOTE]
>
> The steps in this quickstart show how to use the Eclipse IDE to publish a Java web app to App Service, but you can use the IntelliJ IDEA Ultimate Edition or Community Edition. For more information, see [Create a Hello World web app for Azure using IntelliJ](/java/azure/intellij/azure-toolkit-for-intellij-create-hello-world-web-app).
>

## Prerequisites

To complete this quickstart, install:

* The free <a href="https://www.eclipse.org/downloads/" target="_blank">Eclipse IDE for Java EE Developers</a>. This quickstart uses Eclipse Neon.
* The <a href="/java/azure/eclipse/azure-toolkit-for-eclipse-installation" target="_blank">Azure Toolkit for Eclipse</a>.

> [!NOTE]
>
> You will need to sign into your Azure account using the Azure Toolkit for Eclipse to complete the steps in this quickstart. To do so, see [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).
>

## Create a dynamic web project in Eclipse

In Eclipse, select **File** > **New** > **Dynamic Web Project**.

In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.
   
![New Dynamic Web Project dialog box](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### Add a JSP page

If Project Explorer is not displayed, restore it.

![Java EE workspace for Eclipse](./media/app-service-web-get-started-java/pe.png)

In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.
Right-click **WebContent**, and then select **New** > **JSP File**.

![Menu for a new JSP file in Project Explorer](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

In the **New JSP File** dialog box:

* Name the file **index.jsp**.
* Select **Finish**.

  ![New JSP File dialog box](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

In the index.jsp file, replace the `<body></body>` element with the following markup:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Save the changes.

> [!NOTE]
>
> If you see an error on line 1 that refers to a missing Java Servlet class, you can ignore it.
> 
> ![Benign Java servlet error](./media/app-service-web-get-started-java/java-servlet-benign-error.png)
>

## Publish the web app to Azure

In Project Explorer, right-click your project, and then select **Azure** > **Publish as Azure Web App**.

![Publish as Azure Web App context menu](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

If you are prompted with the **Azure Sign In** dialog box, you will need to follow the steps in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article to enter your credentials.

### Deploy Web App dialog box

After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.

Select **Create**.

![Deploy Web App dialog box](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### Create App Service dialog box

The **Create App Service** dialog box appears with default values. The number **170602185241** shown in the following image is different in your dialog box.

![Create App Service dialog box](./media/app-service-web-get-started-java/cas1.png)

In the **Create App Service** dialog box:

* Enter a unique name for your web app, or keep the generated name. This name must be unique across Azure. The name is part of the URL address for the web app. For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.
* For this quickstart, keep the default web container.
* Select an Azure subscription.
* On the **App service plan** tab:

  * **Create new**: Keep the default, which is the name of the App Service plan.
  * **Location**: Select **West Europe** or a location near you.
  * **Pricing tier**: Select the free option. For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).

    ![Create App Service dialog box](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### Resource group tab

Select the **Resource group** tab. Keep the default generated value for the resource group.

![Resource group tab](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Select **Create**.

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

The Azure Toolkit creates the web app and displays a progress dialog box.

![Create App Service Progress dialog box](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### Deploy Web App dialog box

In the **Deploy Web App** dialog box, select **Deploy to root**. If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Deploy Web App dialog box](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

The dialog box shows the Azure, JDK, and web container selections.

Select **Deploy** to publish the web app to Azure.

When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.

![Azure Activity Log dialog box](./media/app-service-web-get-started-java/aal.png)

Congratulations! You have successfully deployed your web app to Azure. 

!["Hello Azure!" example web app](./media/app-service-web-get-started-java/browse-web-app-1.png)

## Update the web app

Change the sample JSP code to a different message.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Save the changes.

In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.

The **Deploy Web App** dialog box appears and shows the app service that you previously created. 

> [!NOTE] 
> Select **Deploy to root** each time you publish. 
> 

Select the web app and select **Deploy**, which publishes the changes.

When the **Publishing** link appears, select it to browse to the web app and see the changes.

## Manage the web app

Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.

From the left menu, select **Resource Groups**.

![Portal navigation to resource groups](media/app-service-web-get-started-java/rg.png)

Select the resource group. The page shows the resources that you created in this quickstart.

![Resource group](media/app-service-web-get-started-java/rg2.png)

Select the web app (**webapp-170602193915** in the preceding image).

The **Overview** page appears. This page gives you a view of how the app is doing. Here, you can  perform basic management tasks like browse, stop, start, restart, and delete. The tabs on the left side of the page show the different configurations that you can open. 

![App Service page in Azure portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## Next steps

> [!div class="nextstepaction"]
> [Map custom domain](app-service-web-tutorial-custom-domain.md)
