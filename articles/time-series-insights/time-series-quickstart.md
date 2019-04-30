---
title: 'Quickstart: Azure Time Series Insights explorer | Microsoft Docs'
description: This quickstart shows you how to get started with Azure Time Series Insights explorer in your web browser to visualize large volumes of IoT data. Tour the key features in a demo environment. 
ms.service: time-series-insights 
services: time-series-insights
author: ashannon7
ms.author: anshan
manager: cshankar
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.topic: quickstart
ms.workload: big-data
ms.custom: mvc seodec18
ms.date: 04/22/2019
---

# Quickstart: Explore Azure Time Series Insights

A quickstart explorer is provided to get started with Azure Time Series Insights in a free demonstration environment. Through it, you'll learn how to use your web browser to visualize large volumes of IoT data and tour key features presently in general availability.

Azure Time Series Insights is a fully managed analytics, storage, and visualization service that simplifies how to explore and analyze billions of IoT events simultaneously. It gives you a global view of your data, letting you quickly validate your IoT solution, and avoid costly downtime to mission-critical devices. Through Azure Time Series Insights, you can discover hidden trends, spot anomalies, and conduct root-cause analyses in near real time.

For additional flexibility, Azure Time Series Insights can be added to a pre-existing application through its powerful [REST APIs](./time-series-insights-update-tsq.md) and [client SDK](./tutorial-create-tsi-sample-spa.md). The APIs allow you to store, query time series data, and consume time series data in a client application of your choice. You may also choose to use the client SDK to add UI components to your existing application.

The Time Series Insights explorer is a guided tour of features presently in general availability.

## Prepare the demo environment

1. Create a [free Azure account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) if one hasn't been created.

1. In your browser, navigate to the [general availability demo](https://insights.timeseries.azure.com/demo).

1. If prompted, sign in to the Time Series Insights explorer using your Azure account credentials.

1. The Time Series Insights quick tour page is displayed. Click **Next** to begin the quick tour.

   [![Click Next](media/quickstart/quickstart1.png)](media/quickstart/quickstart1.png#lightbox)

## Explore the demo environment

1. The **Time selection panel** is displayed. Use this panel to select a time frame to visualize.

   [![Time selection panel](media/quickstart/quickstart2.png)](media/quickstart/quickstart2.png#lightbox)

1. Click and drag in the region, then click the **Search** button.

   [![Select a time frame](media/quickstart/quickstart3.png)](media/quickstart/quickstart3.png#lightbox)

   Time Series Insights displays a chart visualization for the time frame you specified. You can do various actions within with the line chart, such as filtering, pinning, sorting, and stacking.

   To return to the **Time selection panel**, click the down arrow as shown:

   [![Chart](media/quickstart/quickstart4.png)](media/quickstart/quickstart4.png#lightbox)

1. Click **Add** in the **Terms panel** to add a new search term.

   [![Add item](media/quickstart/quickstart5.png)](media/quickstart/quickstart5.png#lightbox)

1. In the chart, you can select a region, right-click the region, and select **Explore Events**.

   [![Explore Events](media/quickstart/quickstart6.png)](media/quickstart/quickstart6.png#lightbox)

   A grid of your raw data is displayed from the region you are exploring:

   [![Grid view](media/quickstart/quickstart7.png)](media/quickstart/quickstart7.png#lightbox)

## Select and filter data

1. Edit your terms to change the values in the chart, and add another term to cross-correlate different types of values:

   [![Add a term](media/quickstart/quickstart8.png)](media/quickstart/quickstart8.png#lightbox)

1. Enter a filter term in the **Filter series...** box for improvised series filtering. For the quickstart, enter **Station5** to cross-correlate temperature and pressure for that station.

   [![Filter series](media/quickstart/quickstart9.png)](media/quickstart/quickstart9.png#lightbox)

After you finish the quickstart, you can experiment with the sample data set to create different visualizations.

## Next steps

You are ready to create your own Time Series Insights environment:
> [!div class="nextstepaction"]
> [Plan your Time Series Insights environment](time-series-insights-environment-planning.md)
