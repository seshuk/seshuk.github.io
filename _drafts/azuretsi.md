
---
layout: post
title: "Azure Time Series Insights"
subtitle: "Azure service to process Time series data"
categories: ['Azure']
tags:
 - Azure
 - C#
 - IoT
---

*- What is Azure Time Series Insights:*
    o    Azure Time Series Insights is a fully managed analytics, storage, and visualization service that makes it simple to explore and analyse billions of events simultaneously.
    o    It is designed to work with Time Series data (typically huge amount of data that change over time, ex: State changes etc)
    o    With a few simple configuration settings, it can start capturing events from one or more Event Hubs.
    o    All the events/data is stored in TSI data storage and can be queried for analysis and visualization.
    o    It’s very fast.
    o    TSI has an In-built UI that can be configured to create out of the box charts and dashboards. 
    o   They also provide JavaScript API to adding charts directly to SPAs for creating reports.

*Use cases*
    - Main use cases for this service are the scenarios where there is a need to analyse huge amounts of data and detect patterns from the same. In IoT scenarios where events could be generated every few seconds to milliseconds, it could potentially generate megabytes of data in a few minutes.

    Azure TS Insights helps in the case it provides ways to collect and store that data in real time and query later for analysis. From my experience, the queries ran pretty fast.
* High-level Architecture:*

*Query API*
   [Query API Reference](https://docs.microsoft.com/en-us/rest/api/time-series-insights/time-series-insights-reference-queryapi)

   [Syntax](https://docs.microsoft.com/en-us/rest/api/time-series-insights/time-series-insights-reference-query-syntax)

*Further Reading:*
    https://blogs.technet.microsoft.com/uktechnet/2018/04/26/use-the-query-apis-to-unlock-the-power-of-azure-time-series-insights/


