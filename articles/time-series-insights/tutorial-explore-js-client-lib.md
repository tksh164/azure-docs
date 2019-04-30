---
title: 'Tutorial: Explore the Azure Time Series Insights JavaScript client library | Microsoft Docs'
description: Learn about the Azure Time Series Insights JavaScript client library and the related programming model.
author: ashannon7
manager: cshankar
ms.service: time-series-insights
services: time-series-insights
ms.topic: tutorial
ms.date: 04/23/2019
ms.author: anshan
ms.custom: seodec18
# Customer intent: As a developer, I want to learn about the TSI JavaScript client library, so I can use the APIs in my own applications.
---

# Tutorial: Explore the Azure Time Series Insights JavaScript client library

To help web developers query and visualize data stored in Time Series Insights (TSI), the JavaScript D3-based TSI Client library was developed. This tutorial will guide you through the TSI Client library and programming model using a hosted sample app.

The tutorial details how to work with the library, how to access TSI data, and use chart controls to render and visualize data. You'll also learn how to experiment with different kinds of graphs to visualize data. At the conclusion of the tutorial, you'll be able to use the client library to incorporate TSI features into your own web app.

Specifically, you'll learn about:

> [!div class="checklist"]
> * The TSI sample application.
> * The TSI JavaScript client library.
> * How the sample application uses the library to visualize TSI data.

> [!NOTE]
> * The Tutorial uses a free, hosted, [Time Series Insights web demo](https://insights.timeseries.azure.com/clientsample).
> * The Time Series Insights sample app source files are provided in the [GitHub sample repository](https://github.com/Microsoft/tsiclient/tree/tutorial/pages/tutorial).

## Video

### In this video, we introduce the open source Time Series Insights JavaScript SDK.</br>

> [!VIDEO https://www.youtube.com/embed/X8sSm7Pl9aA]

## Prerequisites

This tutorial uses your browser's **Developer Tools** feature. Modern web browsers ([Microsoft Edge](/microsoft-edge/devtools-guide), [Chrome](https://developers.google.com/web/tools/chrome-devtools/), [FireFox](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools), [Safari](https://developer.apple.com/safari/tools/), and others)
typically provide access to the **Web Inspector View** through the `F12` hotkey. Otherwise, it can be accessed by right-clicking on a webpage and selecting **Inspect Element**.

## Time Series Insights sample application

Throughout this tutorial, a free, hosted, Time Series Insights sample app is used to explore the source code behind the application and the TSI JavaScript client library. Through it, you'll learn how to interact with TSI in JavaScript and visualize data through charts and graphs.

1. Navigate to the [Time Series Insights sample application](https://insights.timeseries.azure.com/clientsample). The following sign in prompt will appear:

   [![TSI Client sample sign-in prompt](media/tutorial-explore-js-client-lib/tcs-sign-in.png)](media/tutorial-explore-js-client-lib/tcs-sign-in.png#lightbox)

1. Select **Log in** to enter or select your credentials. Use either an enterprise organization account (Azure Active Directory) or a personal account (Microsoft Account or MSA).

   [![TSI Client sample credentials prompt](media/tutorial-explore-js-client-lib/tcs-sign-in-enter-account.png)](media/tutorial-explore-js-client-lib/tcs-sign-in-enter-account.png#lightbox)

1. After signing-in, you'll see a page with several kinds of charts populated with TSI data. Your user account and the **Log out** option are visible in the upper right corner:

   [![TSI Client sample main page after sign-in](media/tutorial-explore-js-client-lib/tcs-main-after-signin.png)](media/tutorial-explore-js-client-lib/tcs-main-after-signin.png#lightbox)

### Page source and structure

<div id="page-source-and-structure"></div>

First, let's view the [HTML and JavaScript source code](https://github.com/Microsoft/tsiclient/blob/tutorial/pages/tutorial/index.html) of the rendered web paged:

1. Open **Developer Tools** in your browser. Inspect the HTML elements that make up the current page (also known as the HTML or DOM tree).

1. Expand the `<head>` and `<body>` elements and observe the following sections:

   * Under the `<head>` element, you'll find page meta-data and dependencies that enable the app to run:
     * A `<script>` element that's used for referencing the Azure Active Directory Authentication Library **adal.min.js** (also known as ADAL). ADAL is a JavaScript library that provides OAuth 2.0 authentication (sign-in) and token acquisition for accessing APIs.
     * Multiple `<link>` elements for style sheets (also known as CSS) like **sampleStyles.css** and **tsiclient.css**. The style sheets are used to control visual page styling details, such as colors, fonts, spacing, and so on.
     * A `<script>` element that's used for referencing the TSI Client JavaScript library **tsiclient.js**. The library is used by the page to call TSI service APIs and render chart controls on the page.

     >[!NOTE]
     > * The source code for the ADAL JavaScript library is available from the [azure-activedirectory-library-for-js repository](https://github.com/AzureAD/azure-activedirectory-library-for-js).
     > * The source code for the TSI Client JavaScript library is available from the [tsiclient repository](https://github.com/Microsoft/tsiclient/tree/tutorial/pages/tutorial).

   * Under the `<body>` element, you'll find `<div>` elements, which help define the layout of items on the page, and another `<script>` element:
     * The first `<div>` element specifies the **Log in** dialog (`id="loginModal"`).
     * The second `<div>` element acts as a parent for:
       * A header `<div>` element that's used for status messages and sign-in information near the top of the page (`class="header"`).
       * A `<div>` element for the remainder of the page body elements, including all of the charts (`class="chartsWrapper"`).
       * A `<script>` section that contains all of the JavaScript that's used to control the page.

   [![TSI Client sample with Developer Tools](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-head-body.png)](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-head-body.png#lightbox)

1. Expand the `<div class="chartsWrapper">` element and you'll find more child `<div>` elements. These elements are used to position each chart control example. Notice that there are several pairs of `<div>` elements, one for each chart example:

   * The first (`class="rowOfCardsTitle"`) element contains a descriptive title to summarize what the chart(s) illustrate. For example: `Static Line Charts With Full-Size Legends.`
   * The second (`class="rowOfCards"`) element is a parent that contains additional child `<div>` elements that position the actual chart control(s) within a row.

   [![Body div elements](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-body-divs.png)](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-body-divs.png#lightbox)

1. Now, expand the `<script type="text/javascript">` element that's directly below the `<div class="chartsWrapper">` element. Notice the beginning of the page-level JavaScript section that's used to handle all of the page logic (authentication, calling TSI service APIs, rendering the chart controls, and more):

   [![Body script](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-body-script.png)](media/tutorial-explore-js-client-lib/tcs-devtools-callouts-body-script.png#lightbox)

## TSI JavaScript client library concepts

The TSI Client library (**tsclient.js**) provides abstractions for two important JavaScript functionalities:

* **Wrapper methods for calling the TSI Query APIs**: REST APIs that allow you to query for TSI data by using aggregate expressions. The methods are organized under the `TsiClient.Server` namespace of the library.

* **Methods for creating and populating several types of charting controls**: Methods that are used for rendering the TSI aggregate data in a web page. The methods are organized under the `TsiClient.UX` namespace of the library.

Through these simplifications, developers can build UI graph and chart components that are powered with TSI data more easily.

### Authentication

The [Time Series Insights sample application](https://insights.timeseries.azure.com/clientsample) is a single-page app with ADAL OAuth 2.0 user authentication support:

1. When using ADAL for authentication, the client app must be registered in Azure Active Directory. In fact, the single-page app is registered to use the [OAuth 2.0 implicit grant flow](https://docs.microsoft.com/azure/active-directory/develop/v1-oauth2-implicit-grant-flow).
1. As such, the application must specify some of the registration properties at runtime. These include the client GUID (`clientId`) and redirect URI (`postLogoutRedirectUri`).
1. Later, the app requests an **access token** from Azure Active Directory. The access token is issued for a finite set of permissions for a specific service/API identifier (`https://api.timeseries.azure.com`). The token permissions are issued on behalf of the signed-in user. The identifier for the service/API is another property that's contained in the app's Azure Active Directory registration.
1. After ADAL returns the access token to the app, it's passed as a **bearer token** when accessing the TSI service APIs.

   [!code-javascript[head-sample](~/samples-javascript/pages/tutorial/index.html?range=147-204&highlight=3-7,34-37)]

### Control identification

In the provided example, `<div>` elements are arranged in the parent `<body>` element to provide a sensible layout for all of the chart controls rendered on the page.

Each `<div>` element specifies properties for the placement and visual attributes of chart controls. HTML element `id` properties serve as unique identifiers to bind to specific controls for rendering and updating visualized data.

### Aggregate expressions

The TSI Client library APIs use aggregate expressions:

* An aggregate expression provides the ability to construct one or more **search terms**.

* The Client APIs are designed to provide similar functionality to another provide demo app (the [Time Series Insights explorer](https://insights.timeseries.azure.com/demo)), which uses search span, where predicate, measures, and split-by value.

* Most of the Client library APIs take an array of aggregate expressions that are used by the service to build a TSI data query.

### Call pattern

Populating and rendering chart controls follows a general pattern. This general pattern can be observed throughout the sample app and will assist you when using the Client library:

1. Declare an `array` to hold one or more TSI aggregate expressions:

   ```javascript
   var aes =  [];
   ```

1. Build *1* to *n* aggregate expression objects. Then, add them to the aggregate expression array:

   ```javascript
   var ae = new tsiClient.ux.aggregateExpression(predicateObject, measureObject, measureTypes, searchSpan, splitByObject, color, alias, contextMenuActions);
   aes.push(ae);
   ```

   **aggregateExpression parameters**

   | Parameter | Description | Example |
   | --------- | ----------- | ------- |
   | `predicateObject` | The data filtering expression. |`{predicateString: "Factory = 'Factory3'"}` |
   | `measureObject`   | The property name of the measure that's used. | `{property: 'Temperature', type: "Double"}` |
   | `measureTypes`    | The desired aggregations of the measure property. | `['avg', 'min']` |
   | `searchSpan`      | The duration and interval size of the aggregate expression. | `{from: startDate, to: endDate, bucketSize: '2m'}` |
   | `splitByObject`   | The string property that you wish to split by (optional – can be null). | `{property: 'Station', type: 'String'}` |
   | `color`         | The color of the objects that you wish to render. | `'pink'` |
   | `alias`           | A friendly name for the aggregate expression. | `'Factory3Temperature'` |
   | `contextMenuActions` | An array of actions to be bound to the time series objects in a visualization (optional). | For more information, see the section [Pop-up context menus](#contextMenu) |

1. Call a TSI query by using the `TsiClient.Server` APIs to request the aggregate data:

   ```javascript
   tsiClient.server.getAggregates(token, envFQDN, aeTsxArray);
   ```

   **getAggregates parameters**

   | Parameter | Description | Example |
   | --------- | ----------- | ------- |
   | `token`     | The access token for the TSI API. |	`authContext.getTsiToken()` For more information, see [authentication section.](#authentication) |
   | `envFQDN`	 | The fully qualified domain name (FQDN) for the TSI environment. | From the Azure portal, for example: `10000000-0000-0000-0000-100000000108.env.timeseries.azure.com`. |
   | `aeTsxArray` | An array of TSI query expressions. | Use the `aes` variable as described previously: `aes.map(function(ae){return ae.toTsx()}`. |

1. Transform the compressed result that's returned from the TSI query into JSON for visualization:

   ```javascript
   var transformedResult = tsiClient.ux.transformAggregatesForVisualization(result, aes);
   ```

1. Create a chart control by using the `TsiClient.UX` APIs, and bind it to one of the `<div>` elements on the page:

   ```javascript
   var barChart = new tsiClient.ux.BarChart(document.getElementById('chart3'));
   ```

1. Populate the chart control with the transformed JSON data object(s) and render the control on the page:

   ```javascript
   barChart.render(transformedResult, {grid: true, legend: 'compact', theme: 'light'}, aes);
   ```

## Rendering controls

The TSI Client library provides eight unique, out-of-the-box, analytics controls:

* **line chart**
* **pie chart**
* **bar chart**
* **heatmap**
* **hierarchy controls**
* **accessible grid**
* **discrete event timelines**
* **state transition timelines**

### Line, bar, pie chart examples

Look at the demo code used to render some of the standard chart control. Notice the programming model and patterns for creating those controls. Specifically, examine the section of HTML under the `// Example 3/4/5` comment, which renders controls with the HTML `id` values `chart3`, `chart4`, and `chart5`.

Recall from **step 3** of the [Page source and structure section](#page-source-and-structure) that chart controls are arranged in rows on the page each of which has a descriptive title row. In this example, the three charts are populated under the title `"Multiple Chart Types From the Same Data"` `<div>` element, and are bound to the three `<div>` elements that are beneath the title:

[!code-html[code-sample1-line-bar-pie](~/samples-javascript/pages/tutorial/index.html?range=59-73&highlight=1,5,9,13)]

The following section of JavaScript code uses patterns that were outlined earlier: build TSI aggregate expressions, use them to query for TSI data, and render the three charts. Notice the three types that are used from the `tsiClient.ux` namespace: `LineChart`, `BarChart`, and `PieChart`, to create and render the respective charts. Also note that all three charts are able to use the same aggregate expression data `transformedResult`:

[!code-javascript[code-sample2-line-bar-pie](~/samples-javascript/pages/tutorial/index.html?range=241-262&highlight=13-14,16-17,19-20)]

The three charts appear as follows when rendered:

[![Multiple chart types from the same data](media/tutorial-explore-js-client-lib/tcs-multiple-chart-types-from-the-same-data.png)](media/tutorial-explore-js-client-lib/tcs-multiple-chart-types-from-the-same-data.png#lightbox)

## Advanced features

The TSI Client library has several additional features you can use to implement data visualizations creatively.

### States and events

One advanced functionality is the ability to add state transitions and discrete events to charts. This feature is useful for highlighting incidents, alerting, and creating state switches (on/off switches for example).

Look at the code surrounding the `// Example 10` comment. The code renders a line control under the title `"Line Charts with Multiple Series Types"`, and binds it to the `<div>` element with the HTML `id` value `chart10`.

1. First, a structure named `events4` is defined to hold the state-change elements to track. The structure contains:

   * A string key named `Component States`.
   * An array of value objects that represent the states. Each object includes:
     * A string key that contains a JavaScript ISO timestamp.
     * An array that contains the characteristics of the state: a color and a description.

2. Next, the `events5` structure is defined for `Incidents`, which holds an array of the event elements to track. The array structure is the same shape as the structure that's outlined for `events4`.

3. Finally, the line chart is rendered, passing in the two structures with the chart options parameters: `events:` and `states:`. Notice the other option parameters for specifying a `tooltip:`, `theme:`, or `grid:`.

[!code-javascript[code-sample-states-events](~/samples-javascript/pages/tutorial/index.html?range=337-389&highlight=5,26,51)]

Visually, the diamond markers/pop-up windows that are used to indicate incidents, and the colored bars/pop-up windows along the time scale, indicate state changes:

[![Line Charts with Multiple Series Types](media/tutorial-explore-js-client-lib/tcs-line-charts-with-multiple-series-types.png)](media/tutorial-explore-js-client-lib/tcs-line-charts-with-multiple-series-types.png#lightbox)

### Pop-up context menus

<div id="contextMenu"></div>

Another advanced functionality is the ability to create custom context menus (right-click pop-up menus). Custom context menus are useful for enabling actions and logical next steps within the scope of your application.

Look code around the `// Example 13/14/15` comment. This code initially renders a line chart under the title `"Line Chart with Context Menu to Create Pie/Bar Chart"` and the chart is bound to the `<div>` element with the HTML `id` value `chart13`.

By using context menus, the line chart provides the capability to dynamically create a pie and bar chart that are bound to `<div>` elements with the IDs `chart14` and `chart15`. In addition, both the pie and bar charts also use context menus to enable their own features: the ability to copy data from the pie to bar chart, and print the bar chart data to the browser console window, respectively.

1. First a series of custom actions are defined. Each action contains an array with one or more elements. Each element defines a single context menu item:

   * `barChartActions`: This action defines the context menu for the pie chart, which contains one element to define a single item:
     * `name`: The text that's used for the menu item: "Print parameters to console."
     * `action`: The action that's associated with the menu item. The action is always an anonymous function that takes three arguments that are based on the aggregate expression that's used to create the chart. In this case, the arguments are written to the browser console window:
       * `ae`: The aggregate expression array.
       * `splitBy`: The `splitBy` value.
       * `timestamp`: The timestamp.

   * `pieChartActions`: This action defines the context menu for the bar chart, which contains one element to define a single item. The shape and schema is the same as the previous `barChartActions` element, but notice that the `action` function is dramatically different: it instantiates and renders the bar chart. Also note that the `ae` argument is used to specify the aggregate expression array that's passed at runtime when the menu item opens. The function also sets the `ae.contextMenu` property with the `barChartActions` context menu.
   * `contextMenuActions`: This action defines the context menu for the line chart, which contains three elements to define three menu items. The shape and schema for each element is the same as the previous elements that were described. Just like the `barChartActions` element, the first item writes the three function arguments to the browser console window. Similar to the `pieChartActions` element, the second two items instantiate and render the pie and bar charts, respectively. The second two items also set their `ae.contextMenu` properties with the `pieChartActions` and `barChartActions` context menus, respectively.

2. Next, two aggregate expressions are pushed onto the `aes` aggregate expression array and specify the `contextMenuActions` array for each item. These expressions are used with the line chart control.

3. Finally, only the line chart is initially rendered, from which both the pie and bar chart can be rendered at runtime.

[!code-javascript[code-sample-context-menus](~/samples-javascript/pages/tutorial/index.html?range=461-540&highlight=7,16,29,61-64,78)]

The screenshot shows the charts with their respective pop-up context menus. The pie and bar charts were created dynamically by using the line chart context menu options.

[![Line Chart with Context Menu to Create Pie/Bar Chart](media/tutorial-explore-js-client-lib/tcs-line-chart-with-context-menu-to-create-pie-bar-chart.png)](media/tutorial-explore-js-client-lib/tcs-line-chart-with-context-menu-to-create-pie-bar-chart.png#lightbox)

### Brushes

Brushes are used to scope a time range to define actions like zoom and explore.

The code that's used to illustrate brushes is shown in the previous "Line Chart with Context Menu to Create Pie/Bar Chart" example that describes Pop-up context menus.

1. Brush actions are similar to a context menu in that they define a series of custom actions for the brush. Each action contains an array with one or more elements. Each element defines a single context menu item:
   * `name`: The text that's used for the menu item: "Print parameters to console."
   * `action`: The action that's associated with the menu item, which is always an anonymous function that takes two arguments. In this case, the arguments are written to the browser console window:
      * `fromTime`: The `from` timestamp of the brush selection.
      * `toTime`: The `to` timestamp of the brush selection.

2. Brush actions are added as another chart option property. Notice the `brushContextMenuActions: brushActions` property that's passed to the `linechart.Render` call.

[!code-javascript[code-sample-brushes](~/samples-javascript/pages/tutorial/index.html?range=526-540&highlight=1,13)]

[![Line chart with context menu to create pie/bar chart with brushes](media/tutorial-explore-js-client-lib/tcs-line-chart-with-context-menu-to-create-pie-bar-chart-brushes.png)](media/tutorial-explore-js-client-lib/tcs-line-chart-with-context-menu-to-create-pie-bar-chart-brushes.png#lightbox)

## Next steps

In this tutorial, you learned how to:

> [!div class="checklist"]
> * Sign in and explore the TSI sample application and its source.
> * Use APIs in the TSI JavaScript client library.
> * Use JavaScript to create and populate chart controls with TSI data.

As seen, the TSI sample application uses a demo data set. To learn how you can create your own TSI environment and data set, advance to the following article:

> [!div class="nextstepaction"]
> [Tutorial: Create an Azure Time Series Insights environment](tutorial-create-populate-tsi-environment.md)

Or view the TSI sample application source files:

> [!div class="nextstepaction"]
> [TSI sample app repository](https://github.com/Microsoft/tsiclient/tree/tutorial/pages/tutorial)
