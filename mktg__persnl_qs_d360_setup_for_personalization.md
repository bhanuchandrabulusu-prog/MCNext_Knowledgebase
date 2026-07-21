# Setup Guide: Data 360 for Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_qs_d360_setup_for_personalization.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Setup Guide: Data 360 for Salesforce Personalization

This guide covers the steps to set up Data 360 to support Salesforce Personalization for Marketing Cloud Next. It outlines basic recommendations, so that your team can get up and running. For in-depth information, special features, or customization options, we provide additional resources along the way.

REQUIRED EDITIONS
Available in: Salesforce Enterprise and Unlimited Editions with the Personalization Starter add-on.
Getting to Know Salesforce Personalization
Salesforce Personalization Marketing Cloud Next works with Data 360 to provide personalized experiences across Salesforce clouds. It uses objective-based (using ML), or rules-based content recommenders to deliver personalized experiences to customers across channels. For simple use cases, you can also configure rules to surface specific content assets.
Assigning Permissions to Admins and Users
To set up Salesforce Personalization, you work in Salesforce Setup, Data 360 Setup, and the Data 360 and Salesforce Personalization apps. Before you begin, make sure you and other admins on your team have the necessary roles and permissions.
Enable Data 360 and Deploy Personalization Data Kits
Turn on Data 360 and deploy data kits to provide the unified data and necessary infrastructure to power the core capabilities of Salesforce Personalization.
Schedule Required Calculated Insights
After the calculated insights from the data kit are available, you must schedule them to run periodically. This data is used to generate the metrics that measures and populates the personalization pipeline intelligence dashboard. A Data 360 Admin can complete this task in the Data 360 app.
Building a Data 360 Sitemap for Personalization
To assist with building a Data 360 sitemap for Personalization, you can use the Salesforce Data 360 Sitemap Builder. This tool is a low-code to no-code Chrome extension tool that helps to simplify the creation of Data 360 sitemaps and schemas. The purpose of this extension is to help decrease the need for JavaScript programming knowledge, and make personalization implementation more accessible to non-developers.
Configure a Website Connector
To allow data to move between interactions on your website and Salesforce Personalization, you must create a connector, create a sitemap, and install the SDK that sends interaction data back to Salesforce Personalization.
Upload an Event Schema
When you set up a website connector to send event data to Data 360, you must upload a schema file in JSON format that outlines the structure of the event data that you’re tracking.
Configure and Map Data Streams
Installing the data kits add the objects and fields that store marketing data. However, the data kits only deploy datastreams used for analytics and attribution. To bring external data and make it available to your marketing tools and processes, you must deploy data streams and map them to the Data 360 objects.
Configure Identity Resolution Rules
Identity resolution is a critical step to organizing and unifying your data. Usually, when your data originates from many systems, it’s modeled and labeled differently in each place. Identity resolution rulesets define the relationships among data model objects (DMOs) and their fields. After you configure these rules, Data 360 can organize related and duplicate data into unified individual records that marketers can use for cross-channel personalization.
Create Required Data Graphs
Instead of querying your entire database every time you want to serve personalized content, Data 360 and Salesforce Personalization use data graphs, which organize and store only relevant data. For Salesforce Personalization, you can use two data graphs: a real-time profile data graph for person details, and a standard item data graph for product and content information.
Create Calculated Insights for Targeting
Calculated Insights can streamline your personalization strategy for rules-based recommenders and recommendation filters. For example, add a calculated insight to your item data graph to identify most viewed or most purchased products or to restrict products for certain recommendations.
