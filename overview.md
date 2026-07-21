# Overview

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/overview.html

---

Personalization is a Customer 360 application that works with Data Cloud to provide personalized experiences across Salesforce clouds. It uses product recommendations and goal-based and rule-based content targeting to deliver personalized recommendations or custom content to users.

Personalization uses Data Cloud to isolate, organize, and prepare data for use as personalized content. Data Cloud data spaces provide logical partitions to organize the data for profile unification, calculated insights, and marketing.

A data space contains data graphs that use data model objects (DMOs) to build precalculated views of your data. Personalization uses these data graphs to more quickly and efficiently obtain and deliver personalized content to users or site visitors. Personalization uses its own DMOs when making decisions about which individuals are eligible to receive a personalization, and when determining what personalized content to provide.

Personalization is delivered in the following ways.

A Customer 360 Personalization application that centralizes connected and personalized experiences across clouds.
Personalization as a Service, providing real-time, Data Cloud-based, personalization functionality to Salesforce customers across channels.

To generate and present unique, personalized content experiences, Personalization uses Data Cloud profile and item data graphs, calculated insights, segments, and real-time behavioral data.

User interaction data is ingested using Salesforce Interactions SDK. Data is simultaneously ingested into two processing layers - the real-time layer for immediate processing, and the standard data layer for regular processing along with other ingested data.
Data Cloud identity resolution performs real-time matching to identify a user profile. If the user is unknown, a new profile is created.
The known or anonymous profile in the real-time data graph is updated with ingested engagement and profile event data.
Real-time insights and segments are calculated. The real-time profile data graph is updated with metrics and segmentation results.
When a personalization decision is required, Personalization.. calls the Data Cloud profile API to obtain the updated individual profile from the real-time profile data graph.
Salesforce Help: Personalization
Salesforce Help: Personalization and Data Cloud Setup
Salesforce Help: About Salesforce Data Cloud
Salesforce Help: Manage Data Spaces
Salesforce Help: Data Graphs
Salesforce Help: Create and Activate Segments
Salesforce Help: Enhance Data with Insights
