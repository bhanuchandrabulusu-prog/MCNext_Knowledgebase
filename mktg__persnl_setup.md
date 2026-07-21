# Salesforce Personalization and Data 360 Setup

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Salesforce Personalization and Data 360 Setup

Salesforce Personalization in Marketing Cloud Next is a Customer 360 application that connects and provides personalized experiences across clouds. To use Salesforce Personalization, define the appropriate permissions, and install and configure Data 360 to work with Personalization data model objects.

Salesforce Personalization and Data 360
To generate and present unique, personalized content experiences, Salesforce Personalization in Marketing Cloud Next uses profile and item data graphs, calculated insights, segments, and real-time behavioral data from Data 360.
Salesforce Personalization Permissions
Configure the right permissions for creating and managing personalization, and empower your users to leverage Web Personalization Manager and the Personalization Intelligence app.
Data 360 Prerequisites
Salesforce Personalization requires Data 360. Set up Personalization to work with Data 360.
Add the Web SDK with the Personalization Module to Your Site
Salesforce Personalization requires the Salesforce Interactions SDK with the Personalization module.
Install Salesforce Personalization Data and Personalization Intelligence
Before you can use Salesforce Personalization, you must deploy required foundational data elements to the Data 360 data space that you want Personalization to use. You can also install a personalization pipeline intelligence dashboard or deploy optional attribution intelligence data.
Add Custom Fields to the Goods Product Data Model Object
If you want to use the Salesforce Personalization Maximize Revenue recommender for a retail configuration, add these fields to the Goods Product data model object.
Real-Time Identity Resolution for Personalization
Real-time identity resolution matches information about active users to a unified profile object, consolidating profile data from different sources. Each unified profile contains all unique contact point values from all sources, providing a comprehensive view of each individual. Combining real-time identity resolution and Salesforce Personalization, you can deliver personalized content to individuals using your app or website within milliseconds.
Using Data Graphs With Personalization
Salesforce Personalization requires the Data 360 profile data graph and item data graph. The profile data graph provides real-time data to determine personalization eligibility. The item data graph provides data to the Personalization recommenders that are used to generate recommendations.
Assign a Default Data Graph to a Data Space
You can assign default profile data graphs to specific data spaces, providing selection guidance for Salesforce Personalization configurations. After the data graph is assigned, it is automatically populated as the default data graph whenever you select its associated data space in a Salesforce Personalization configuration.
Creating and Deploying a Preconfigured Personalization Use Case
Using preconfigured templates and data kits, you can more quickly and easily create a recommender-based Personalization use case for one-time deployment to a data space that doesn't have a profile data graph.
Define Segments for Salesforce Personalization
You can define real-time segments based on customer interactions to deliver immediate responses. For example, use segments to assess user engagement in real time to segment customers based on interests and preferences. You can also define standard segments to determine which products you want to recommend to individuals. For example, you can exclude products that users have purchased in the past 15 days from a recommendation list.
Configure Data 360 Insights for Personalization
You can configure Data 360 insights to define and calculate multidimensional metrics for use by Salesforce Personalization. Using insights, you can define specialized metrics to provide more in-depth views into customer activity, better understand site or app interaction, or gauge customer satisfaction.
Data Graph Configuration for Objective-Based Recommenders
Supplement your Data 360 data graph setup with the required fields to leverage the Maximize Revenue or Maximize Clicks objective-based recommenders. These recommenders require certain object and field configurations in both their profile and item data graphs.
Configure Event Streams and Data Models for Maximize Revenue with Promotions Recommenders
Set up the required event streams and data models to enable the Maximize Revenue with Promotion recommender to surface high-impact offers based on real-time engagement and purchase patterns.
Localize Recommendations for Salesforce Personalization
Deliver recommendations in your customers' preferred languages. By mapping locale-related fields to Data Model Objects (DMOs), you ensure the system returns translated content and appropriate fallback attributes automatically.
