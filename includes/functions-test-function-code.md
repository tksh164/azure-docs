---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/04/2018
ms.author: glenga
---
## <a name="test"></a>Test the function

Use cURL to test the deployed function on a Mac or Linux computer or using Powershell on Windows. Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app. Append the query string `&name=<yourname>` to the URL.

```powershell
Invoke-WebRequest -Uri "https://<app_name>.azurewebsites.net/api/MyHttpTrigger?name=<yourname>"
```

```bash
curl https://<app_name>.azurewebsites.net/api/MyHttpTrigger?name=<yourname>
```  

![Function response shown in a browser.](./media/functions-test-function-code/functions-azure-cli-function-test-curl.png)  

If you don't have `cURL`or `Invoke-WebRequest` available in your command line, enter the same URL in the address of your web browser. Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.

    https://<app_name>.azurewebsites.net/api/MyHttpTrigger?name=<yourname>
   
![Function response shown in a browser.](./media/functions-test-function-code/functions-azure-cli-function-test-browser.png)  
