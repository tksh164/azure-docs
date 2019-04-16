---
title: 'Visualize data in the Azure Time Series Insights Preview explorer | Microsoft Docs'
description: This article describes features and options available in the Azure Time Series Insights Preview explorer web app.
author: ashannon7
ms.author: anshan
ms.workload: big-data
manager: cshankar
ms.service: time-series-insights
services: time-series-insights
ms.topic: conceptual
ms.date: 12/03/2018
ms.custom: seodec18
---

# Visualize data in the explorer Preview

This article describes features and options available in the Azure Time Series Insights Preview [explorer web app](https://insights.timeseries.azure.com/preview/samples).

## Prerequisites

Before you use the Azure Time Series Insights Preview explorer, you must:

* Have a Time Series Insights environment set up. For more information, see [Tutorial: Azure Time Series Insights Preview](./time-series-insights-update-create-environment.md).
* Provide data access to the Time Series Insights environment that you created for the account. You can provide access to others as well as to yourself.
* Add an event source to the Time Series Insights environment to push data to the environment.

## Learn about the Azure Time Series Insights Preview explorer

  ![explorer-one][1]

The Azure Time Series Insights Preview explorer consists of the following elements:

* **Navigation bar**: Lets you switch between analytics and model pages.
* **Hierarchy tree**: Lets you select specific data elements to be charted.
* **Time series well**: Displays your currently selected data elements.
* **Chart panel**: Displays your current working chart.
* **Timeline**: Lets you modify your working time span.
* **App bar**: Contains your user management options, such as current tenant, and lets you change theme and language settings.

## Time Series Insights Preview environment panel

The environment panel displays all the Time Series Insights environments you have access to. The list includes pay-as-you-go environments Preview and S1/S2 environments (GA). Simply click the Time Series Insights environment you want to use.

  ![explorer-two][2]

## Time Series Insights Preview navigation menu

  ![explorer-three][3]

With the navigation menu, you can switch between the Time Series Insights apps:

* **Analyze**: Lets you chart and perform rich analytics on your modeled or unmodeled time series data.

* **Model**: Lets you push new Time Series Insights Preview types, hierarchies, and instances to your Time Series Insights model.

## Time Series Insights Preview model authoring

With this app, you can perform Create, Read, Update, and Delete (CRUD) operations on your Time Series Model.  

* **Time Series Model type**: Time Series Insights types enable defining variables or formulas for doing computations. They are associated with a given Time Series Insights instance. A type can have one or more variables.
* **Time Series Model hierarchy**: Hierarchies are systematic organizations of your data. Hierarchies depict the relationships between different entities in your Time Series Insights data.
* **Time Series Model instance**: Instances are the time series themselves. In most cases, they are the DeviceID or AssetID, which is the unique identifier of the asset in the environment.

To learn more about the Time Series Model, see [Times Series Models](./time-series-insights-update-tsm.md).

## Time Series Insights Preview model search panel

The model search panel lets you easily search and navigate your Time Series Model hierarchy to find the specific time series instances you want to display on your chart. When you select your instances, they are added to both the current chart and the data well.

  ![explorer-four][4]

## Time Series Insights Preview well

The well displays instance fields and other metadata associated with selected time series instances. The check boxes at the right side let you hide or display specific instances from the current chart. You can also remove specific data elements from your current data well by clicking the red x control to the right of the element.

  ![explorer-five][5]

You can also pop out the telemetry panel to get a better vertical view of the elements in your data well.

  ![explorer-six][6]

> [!NOTE]
> If you see the following message, the instance does not have any data during the time span selected. To resolve the issue, you can increase the time span or confirm that the instance is pushing data.
>
> ![explorer-seven][7]

## Time Series Insights Preview chart

With the chart, you can display time series instances as lines. You can collapse the environment panel, data model, and time span control panel by clicking the web controls to make the chart larger.

  ![explorer-eight][8]

1. **Selected Date range**: Controls which data elements are available for visualization.

1. **Inner Date range slider tool**: Use the two endpoint controls by dragging them over the desired time span.

1. **Time span collapse control**: Collapses and expands the time span panel editor.

1. **Y-axis format control**: Cycles through the available Y-axis view options:

    * `Default`: Each line has an individual Y-axis.
    * `Stacked`: Lets you stack multiple lines on the same Y-axis, with the Y-axis data changing based on the line selected.
    * `Shared`: All Y-axis data displayed together.

1. **Current data element**: The currently selected data element and its associated details.

You can further drill into a specific data slice by left-clicking a data point on the current graph and then dragging the selected area to the endpoint of your choice. Right-click the greyed, selected area, and click zoom as shown in this following image:

  ![explorer-nine][9]

After you perform the zoom action, you will see your selected dataset. Click the Y-axis format control to cycle through the three Y-axis representations of your Time Series Insights data.

  ![explorer-ten][10]

Here you can see an example of shared Y-axes:

  ![explorer-eleven][11]

## Time Series Insights Preview time editor panel

When you work with Time Series Insights Preview, you first select a time span. The selected time span controls the dataset that is available for manipulation with the Time Series Insights Preview widgets. The following web controls are available in Time Series Insights Preview for selecting your working time span.

  ![explorer-twelve][12]

1. **Inner-date range slider tool**: Use the two endpoint controls by dragging them over the desired time span. This inner-date range is constrained by the outer-date range slider control.

1. **Increase and decrease date range buttons**: Increase or decrease your time span by selecting either button for the interval you want.

1. **Time span collapse control**: This web control lets you hide all the controls except for the inner-date range slider tool.

1. **Outer-date range slider control**: Use the endpoint controls to select the outer-date range, which will be available for your inner-date range control.

1. **Quick times date range drop-down**: Lets you quickly switch between preset time span selections, such as the last 30 minutes, the last 12 hours, or a custom range. Changing this value also changes the available interval ranges discussed in the interval-size slider tool.

1. **Interval-size slider tool**: Lets you zoom in and out of intervals over the same time span. This action provides more precise control of movement between large slices of time. It displays smooth trends down to slices as small as a millisecond, allowing you to see granular, high-resolution cuts of your data. The slider’s default starting point is set as the most optimal view of the data from your selection, which balances resolution, query speed, and granularity.

1. **Date range to and from web control**: With this web control you can easily click and select your desired date and time ranges. You can also use the control to switch between different time zones. After you make the changes, to apply to your current workspace, select **Save**.

   ![explorer-thirteen][13]

## Time Series Insights Preview navigation panel

The Time Series Insights Preview navigation panel provides the following functionality:

  ![explorer-fourteen][14]

### Current session share link control

  ![explorer-fifteen][15]

Select the link web control (highlighted) to generate a URL to save or share your current Azure Time Series Insights working session, which includes:

* Currently selected time range
* Currently selected interval size
* Currently selected data well

### Tenant section

  ![explorer-sixteen][16]

* Displays your current Time Series Insights login account information.
* Lets you switch between the available Time Series Insights themes.

### Theme selection

Azure Time Series Insights Preview supports two themes:

* **Light Theme**: The default theme shown throughout this document.
* **Dark theme**:  Renders the explorer as shown here:

  ![explorer-seventeen][17]

Here you can also change between supported languages.

## S1/S2 environment controls

### Time Series Insights Preview terms panel

This section applies only to existing S1/S2 environments that attempt to use the explorer in the updated UI. You might want to use the GA product and Preview in combination. We’ve added some functionality from the existing UI to the updated explorer, but you can get the full UI experience for S1/S2 environment in the existing Time Series Insights explorer.  

In lieu of the hierarchy, you will see the Time Series Insights terms panel, where you define queries in your environment. It lets you filter your data based on a predicate.

  ![explorer-eighteen][18]

The Time Series Insights Preview terms editor panel takes the following parameters:

**Where**: The where clause lets you quickly filter your events by using the set of operands listed in the following table. If you conduct a search by selecting an operand, the predicate is automatically updated based on that search. Supported operand types include:

| Operation	| Supported types	| Notes |
| --- | --- | --- |
| `<`, `>`, `<=`, `>=` | Double, DateTime, TimeSpan | |
| `=`, `!=`, `<>` | String, Bool, Double, DateTime, TimeSpan, NULL |
| `IN` | String, Bool, Double, DateTime, TimeSpan, NULL | All operands should be of the same type or be NULL constant. |
| `HAS` | String | Only constant string literals are allowed at right-hand side. Empty string and NULL are not allowed. |

Learn more about supported query operations and data types by reading [Time Series Expression (TSX)](https://docs.microsoft.com/rest/api/time-series-insights/preview-tsx).

### Examples of Where clauses

  ![explorer-nineteen][19]

**Measure**: This drop-down displays all numeric columns (**Doubles**) that you can use as elements for your current chart.

**Split by**: This drop-down displays all the available categorical columns (Strings) in your model that you can group your data by. You can add up to five terms to view on the same X-axis. Enter your desired parameters, and then select **Add** to add a fresh term.

  ![explorer-twenty][20]

You can show and hide elements in the chart panel by selecting the visible icon as shown in the following image. You can completely remove queries by clicking the red **x**.

  ![explorer-twenty-one][21]

## Next steps

See the following articles:
* [Azure Time Series Insights Preview storage and ingress](./time-series-insights-update-storage-ingress.md)
* [Data modeling](./time-series-insights-update-tsm.md)
* [Diagnosing and troubleshooting](./time-series-insights-update-how-to-troubleshoot.md)

<!-- Images -->
[1]: media/v2-update-explorer/explorer-one.png
[2]: media/v2-update-explorer/explorer-two.png
[3]: media/v2-update-explorer/explorer-three.png
[4]: media/v2-update-explorer/explorer-four.png
[5]: media/v2-update-explorer/explorer-five.png
[6]: media/v2-update-explorer/explorer-six.png
[7]: media/v2-update-explorer/explorer-seven.png
[8]: media/v2-update-explorer/explorer-eight.png
[9]: media/v2-update-explorer/explorer-nine.png
[10]: media/v2-update-explorer/explorer-ten.png
[11]: media/v2-update-explorer/explorer-eleven.png
[12]: media/v2-update-explorer/explorer-twelve.png
[13]: media/v2-update-explorer/explorer-thirteen.png
[14]: media/v2-update-explorer/explorer-fourteen.png
[15]: media/v2-update-explorer/explorer-fifteen.png
[16]: media/v2-update-explorer/explorer-sixteen.png
[17]: media/v2-update-explorer/explorer-seventeen.png
[18]: media/v2-update-explorer/explorer-eighteen.png
[19]: media/v2-update-explorer/explorer-nineteen.png
[20]: media/v2-update-explorer/explorer-twenty.png
[21]: media/v2-update-explorer/explorer-twenty-one.png
