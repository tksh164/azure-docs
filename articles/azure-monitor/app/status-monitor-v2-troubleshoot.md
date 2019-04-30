---
title: Azure Status Monitor v2 troubleshooting and known issues | Microsoft Docs
description: The known issues of Status Monitor v2 and troubleshooting examples. Monitor website performance without redeploying the website. Works with ASP.NET web apps hosted on-premises, in VMs or on Azure.
services: application-insights
documentationcenter: .net
author: MS-TimothyMothra
manager: alexklim
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 04/23/2019
ms.author: tilee
---
# Troubleshooting Status Monitor v2

When you enable monitoring, you may experience issues that prevent data collection. 
This document lists all the known issues and troubleshooting examples.
If you come across an issue not listed here, you may contact us [here](https://github.com/Microsoft/ApplicationInsights-Home/issues).


> [!IMPORTANT]
> Status Monitor v2 is currently in public preview.
> This preview version is provided without a service level agreement, and it's not recommended for production workloads. Certain features might not be supported or might have constrained capabilities.
> For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)

## Known issues

### Conflicting DLLs in an application's bin directory

If any of these DLLs are present in the bin directory, monitoring may fail.

- Microsoft.ApplicationInsights.dll
- Microsoft.AspNet.TelemetryCorrelation.dll
- System.Diagnostics.DiagnosticSource.dll

Some of these DLLs are included in Visual Studio's default application templates, even if your application doesn't use them.
Symptomatic behavior can be seen using troubleshooting tools:

- PerfView:
	```
	ThreadID="7,500" 
	ProcessorNumber="0" 
	msg="Found 'System.Diagnostics.DiagnosticSource, Version=4.0.2.1, Culture=neutral, PublicKeyToken=cc7b13ffcd2ddd51' assembly, skipping attaching redfield binaries" 
	ExtVer="2.8.13.5972" 
	SubscriptionId="" 
	AppName="" 
	FormattedMessage="Found 'System.Diagnostics.DiagnosticSource, Version=4.0.2.1, Culture=neutral, PublicKeyToken=cc7b13ffcd2ddd51' assembly, skipping attaching redfield binaries" 
	```

- iisreset + app load (NO TELEMETRY). Investigate with Sysinternals (Handle.exe and ListDLLs.exe)
	```
	.\handle64.exe -p w3wp | findstr /I "InstrumentationEngine AI. ApplicationInsights"
	E54: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.ApplicationInsights.RedfieldIISModule.dll

	.\Listdlls64.exe w3wp | findstr /I "InstrumentationEngine AI ApplicationInsights"
	0x0000000009be0000  0x127000  C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\MicrosoftInstrumentationEngine_x64.dll
	0x0000000009b90000  0x4f000   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\Microsoft.ApplicationInsights.ExtensionsHost_x64.dll
	0x0000000004d20000  0xb2000   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\Microsoft.ApplicationInsights.Extensions.Base_x64.dll
	```

### Conflict with IIS shared configuration

If you have a cluster of web servers, you might be using a [Shared Configuration](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/shared-configuration_211). 
We can't automatically inject our HttpModule into this shared config.
Each web server must first run the Enable command to install our DLL into its GAC.

After you run the Enable command, 
1. browse to your Shared Configuration directory and find your `applicationHost.config` file.
2. Add this line to your configuration in the modules section:
	```
	<modules>
	    <!-- Registered global managed http module handler. The 'Microsoft.AppInsights.IIS.ManagedHttpModuleHelper.dll' must be installed in the GAC before this config is applied. -->
	    <add name="ManagedHttpModuleHelper" type="Microsoft.AppInsights.IIS.ManagedHttpModuleHelper.ManagedHttpModuleHelper, Microsoft.AppInsights.IIS.ManagedHttpModuleHelper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" preCondition="managedHandler,runtimeVersionv4.0" />
	</modules>
	```
	


## Troubleshooting
	
### Troubleshooting PowerShell

#### How to inspect what modules are available?
You can audit installed Modules using the command: `Get-Module -ListAvailable`

#### How to import a module into the current session?
If the Module hasn't been loaded into a PowerShell session, can manually load using the command: `Import-Module <path to psd1>`


### Troubleshooting the Status Monitor v2 module

#### How to review what commands are available in the Status Monitor v2 module?
- Run the command: `Get-Command -Module Az.ApplicationMonitor` to get the available commands:

	```
	CommandType     Name                                               Version    Source
	-----------     ----                                               -------    ------
	Cmdlet          Disable-ApplicationInsightsMonitoring              0.2.1      Az.ApplicationMonitor
	Cmdlet          Disable-InstrumentationEngine                      0.2.1      Az.ApplicationMonitor
	Cmdlet          Enable-ApplicationInsightsMonitoring               0.2.1      Az.ApplicationMonitor
	Cmdlet          Enable-InstrumentationEngine                       0.2.1      Az.ApplicationMonitor
	Cmdlet          Get-ApplicationInsightsMonitoringConfig            0.2.1      Az.ApplicationMonitor
	Cmdlet          Get-ApplicationInsightsMonitoringStatus            0.2.1      Az.ApplicationMonitor
	Cmdlet          Set-ApplicationInsightsMonitoringConfig            0.2.1      Az.ApplicationMonitor
	```

#### What is the current version of the Status Monitor v2 module?
- Run the command: `Get-ApplicationInsightsMonitoringStatus` to get an output of information about this module:

	```
	PowerShell Module version:
	0.2.1-alpha

	Application Insights SDK version:
	2.9.0.3872

	Executing PowerShell Module Assembly:
	Microsoft.ApplicationInsights.Redfield.Configurator.PowerShell, Version=2.8.14.9129, Culture=neutral, PublicKeyToken=31bf3856ad364e35

	PowerShell Module Directory:
	C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\PowerShell

	Runtime Paths:
	ParentDirectory: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content Exists: True
	ConfigurationPath: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\applicationInsights.ikey.config Exists: False
	ManagedHttpModuleHelperPath: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Runtime\Microsoft.AppInsights.IIS.ManagedHttpModuleHelper.dll Exists: True
	RedfieldIISModulePath: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Runtime\Microsoft.ApplicationInsights.RedfieldIISModule.dll Exists: True
	InstrumentationEngine86Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation32\MicrosoftInstrumentationEngine_x86.dll Exists: True
	InstrumentationEngine64Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation64\MicrosoftInstrumentationEngine_x64.dll Exists: True
	InstrumentationEngineExtensionHost86Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation32\Microsoft.ApplicationInsights.ExtensionsHost_x86.dll Exists: True
	InstrumentationEngineExtensionHost64Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation64\Microsoft.ApplicationInsights.ExtensionsHost_x64.dll Exists: True
	InstrumentationEngineExtensionConfig86Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation32\Microsoft.InstrumentationEngine.Extensions.config Exists: True
	InstrumentationEngineExtensionConfig64Path: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Instrumentation64\Microsoft.InstrumentationEngine.Extensions.config Exists: True
	ApplicationInsightsSdkPath: C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\0.2.1\content\Runtime\Microsoft.ApplicationInsights.dll Exists: True
	```




### Troubleshooting running processes

You can inspect the process on the instrumented machine to see if all DLLs are loaded.
If monitoring is working, at least 12 DLLS should be loaded.

- Cmd: `Get-ApplicationInsightsMonitoringStatus -InspectProcess`

	```
	iisreset.exe /status
	Status for IIS Admin Service ( IISADMIN ) : Running
	Status for Windows Process Activation Service ( WAS ) : Running
	Status for Net.Msmq Listener Adapter ( NetMsmqActivator ) : Running
	Status for Net.Pipe Listener Adapter ( NetPipeActivator ) : Running
	Status for Net.Tcp Listener Adapter ( NetTcpActivator ) : Running
	Status for World Wide Web Publishing Service ( W3SVC ) : Running

	handle64.exe -accepteula -p w3wp
	  BF0: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.ServerTelemetryChannel.dll
	  C58: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.AzureAppServices.dll
	  C68: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.DependencyCollector.dll
	  C78: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.WindowsServer.dll
	  C98: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.Web.dll
	  CBC: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.PerfCounterCollector.dll
	  DB0: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.AI.Agent.Intercept.dll
	  B98: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.ApplicationInsights.RedfieldIISModule.dll
	  BB4: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.ApplicationInsights.RedfieldIISModule.Contracts.dll
	  BCC: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.ApplicationInsights.Redfield.Lightup.dll
	  BE0: File  (R-D)   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Runtime\Microsoft.ApplicationInsights.dll

	listdlls64.exe -accepteula w3wp
	0x0000000019ac0000  0x127000  C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\MicrosoftInstrumentationEngine_x64.dll
	0x00000000198b0000  0x4f000   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\Microsoft.ApplicationInsights.ExtensionsHost_x64.dll
	0x000000000c460000  0xb2000   C:\Program Files\WindowsPowerShell\Modules\Az.ApplicationMonitor\content\Instrumentation64\Microsoft.ApplicationInsights.Extensions.Base_x64.dll
	0x000000000ad60000  0x108000  C:\Windows\TEMP\2.4.0.0.Microsoft.ApplicationInsights.Extensions.Intercept_x64.dll
	```

### Collect ETW logs with PerfView

#### Setup

1. Download PerfView.exe and PerfView64.exe from https://github.com/Microsoft/perfview/releases
2. Launch PerfView64.exe
3. Expand "Advanced Options"
4. Uncheck:
	- Zip
	- Merge
	- .NET Symbol Collection
5. Set Additional Providers: `61f6ca3b-4b5f-5602-fa60-759a2a2d1fbd,323adc25-e39b-5c87-8658-2c1af1a92dc5,925fa42b-9ef6-5fa7-10b8-56449d7a2040,f7d60e07-e910-5aca-bdd2-9de45b46c560,7c739bb9-7861-412e-ba50-bf30d95eae36,61f6ca3b-4b5f-5602-fa60-759a2a2d1fbd,323adc25-e39b-5c87-8658-2c1af1a92dc5,252e28f4-43f9-5771-197a-e8c7e750a984`


#### Collecting logs

1. In a cmd console with admin privileges, execute `iisreset /stop` To turn off IIS and all web apps.
2. In PerfView, click "Start Collection"
3. In a cmd console with admin privileges, execute `iisreset /start` To start IIS.
4. Try to browse to your app.
5. After your app finishes loading, return to PerfView and click "Stop Collection"

