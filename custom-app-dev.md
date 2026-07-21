# Custom App Development | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/custom-app-dev.html

---

After you set up Data 360 with data, and use the Customer 360 model and identity resolution rules to create unified profiles, you can use APIs to access and manage profiles and calculated insights.

Check out this comparison table to understand the capabilities of each API available in Data 360. To learn more about each API, check out the section corresponding to each API.

API Name	When to Use & Features	REST Resources	Link to Section
Connect REST API	
Use Connect REST API to get and manipulate Data 360 data through ANSI SQL queries and REST calls to resources, and to get metadata.
Connect REST API provides access to Data 360 resources.
Connect REST API is integrated with the Salesforce Platform, so use it when building platform apps and using platform features.
	
Query
Calculated Insights
Profile
Identity Resolution Rulesets
Segments
Universal ID Lookup
Metadata of Data Cloud Resources
	Connect REST API
Connect API in Apex	
Use Connect API in Apex when using Apex to write a custom app in Salesforce.
Connect API in Apex provides access to a subset of Data 360 resources. It doesn’t provide access to profiles or universal ID lookups.
Use Connect API in Apex to get and manipulate Data 360 data through ANSI SQL queries and REST calls to resources, and to get metadata.
	
Query
Calculated Insights
Identity Resolution Rulesets
Segments
Metadata of Data Cloud Resources
	Connect API in Apex
Data 360 API (also known as Direct API)	
Use Connect REST API to get Data 360 data through ANSI SQL queries or through REST calls to resources, and to get metadata.
Data 360 API provides direct access to resources in the Data 360 tenant. As a result, it has optimized performance. Use Data 360 API if you don’t need to also access Salesforce Platform features and you want fast performance.
Data 360 API provides access to a subset of Data 360 resources. It doesn’t provide access to segments and identity resolution rulesets.
Authorization with OAuth is a two-step process that involves the exchange of the Salesforce access token with a Data 360 access token.
	
Query
Calculated Insights
Profile
Universal ID Lookup
Metadata of Data 360 Resources
	Data Cloud API (also known as Direct API)
SOQL Queries	
Use the REST API query call or Apex to execute SOQL queries against the Unified Profile, Data Source objects, or Data Model objects. SOQL is Salesforce’s query language that’s integrated with the Salesforce Platform. Use SOQL as an alternative to using query API calls with ANSI SQL in Connect API and Data 360 API.
	Query	SOQL Queries
Salesforce Metadata API	
Use the Salesforce Metadata API to retrieve or deploy metadata as part of developing your app.
	See the Metadata API section.	Metadata API

Use Connect REST API in your custom app to run queries, and access profiles, calculated insights, identity resolution rulesets, data source records, and metadata.

These are the actions you can perform on the Data 360 resources using Connect REST API.

Query Library: Query data across data model, lake, unified, and linked objects.
Calculated Insights: Get metadata for calculated insights. Metadata includes dimensions and measures. Create and manipulate calculated insights metadata. Query calculated insight objects. Trigger a run for a calculated insight.
Profile: Get metadata for data model objects in the profile category, including Individual, Contact Point Email, Unified Individual, and Contact Point Address objects. Metadata includes the objects, their fields, and category. Also, query a Profile data model object.
Identity Resolution Rulesets: Get, create, and manipulate identity resolution rulesets. Also, run an identity resolution ruleset job on demand.
Segments: Get, create, manipulate, and publish market segment definitions.
Universal ID Lookup: Look up objects by source ID.
Metadata: Get all metadata in your Data 360 instance, including profiles, calculated insights, segments, and other objects, as well as their relationships to other objects.

For more information, see Data Cloud Resources in the Data Cloud Connect REST API Guide.

Make calls and queries to the Connect REST API by using the Data 360 Connect API Postman Collection. The Postman collection provides a handy template of API calls with prefilled URIs. For more information, see Salesforce Data Cloud Connect APIs. To view a video that walks you through the steps of calling Data Cloud Connect REST APIs with Postman, see Data Cloud Connect APIs and Postman Quick Start Video.

Use Apex, Salesforce’s cloud-based programming language that runs on the Salesforce Platform, to query, create, and manipulate Data 360 components and to query components. The components you can access in Apex are a subset of the ones you can access with Connect REST API.

The Apex classes in the ConnectApi namespace enable you to access and manipulate Data 360 components.

ConnectApi.CdpQuery Class: Get Data 360 metadata and query data.
ConnectApi.CdpCalculatedInsight Class: Create, delete, get, run, and update Data 360 calculated insights.
ConnectApi.CdpIdentityResolution Class: Create, delete, get, run, and update Data 360 identity resolution rulesets.
ConnectApi.CdpSegment Class: Create, delete, get, publish, and update Data 360 segments. Get segment members.

For more information about Apex, see the Apex Developer Guide.

The Data 360 API provides similar capabilities as the Connect API but it is optimized for use when making calls only to the Data 360 tenant and when not accessing Salesforce Platform features. Use the Data 360 API in your app to query data, and to retrieve and manipulate profiles and calculated insights. If your app integrates with the Salesforce Platform features, we recommend you use the Connect REST API or Connect API in Apex.

For more information, see these resources in the Data Cloud Query Guide.

Query Data using Query API
Query Services Status Codes
Query Source Record IDs
Query Calculated Insights
Query Customer Profile Information with Profile API
Retrieve Metadata

Make calls and queries to the Data 360 API by using the Salesforce Data Cloud APIs Postman Collection. The Postman collection provides a handy template of API calls with prefilled URIs. For more information, see the Direct APIs. For Connect API, see Salesforce Data Cloud Connect APIs.

Because the Data 360 API is within a Data 360 tenant, the OAuth authorization to the Data 360 API involves a two-step process to exchange the Salesforce access token with a Data 360 access token.

To use the Data 360 API, an API user must first authenticate to Salesforce using OAuth, which returns an access token. The user can then post that token to an API endpoint, which is accessed via the Salesforce org’s MyDomain. The endpoint returns a Data 360 API access token as well as the tenant-specific endpoint. Next, the user can make Data 360 API calls from the tenant-specific endpoint. For more information about the steps to obtain the access tokens, see Getting Started in the Data Cloud Reference Guide.

In comparison, when using a Salesforce API, such as the Connect REST API, an API user can authenticate to Salesforce using OAuth, and then make API calls via the Salesforce org’s My Domain login URL.

Use the REST API query call or Apex to execute SOQL queries against the Unified Profile, Data Source objects, or Data Model objects. SOQL is Salesforce’s query language that’s integrated with the Salesforce Platform. Use SOQL as an alternative to using query API calls with ANSI SQL in Connect API and Data 360 API.

For more information about what SOQL keywords are supported for Data 360 queries, see Data Cloud Query Profile Parameters in the REST API Developer Guide.

Use the Salesforce Metadata API to migrate metadata, which are definitions of configurations and components of Data 360 from one Data 360 org to another. Metadata API currently provides partial support for Data 360 metadata.

Metadata API is used in these parts of Data 360:

AWS Data Streams
Ingestion API Data Streams
Mobile and Web Data Streams
Data Lake
Data Model

To get a list of all the metadata types available for Data 360, see Data 360 Metadata Types in the Metadata API Developer Guide. For more information, see Using the Metadata API in Data 360 in Salesforce Help.

A subset of Data 360 components can be packaged. To find out which components are available in packaging, see Metadata Components for Data 360 Cheat Sheet) in the Data 360 Partner Guide. Also, check out the Metadata Coverage Report.

As an alternative to Metadata API, you can use unmanaged packages to deploy metadata by installing the packaged components in another org. See Packages and Data Kits.

Use Consent API to opt in or opt out of data-related actions, such as exporting or processing of data, and storage of personally identifiable information.

For more information, see:

REST API Developer Guide: Use the Consent API with Data 360
Trailhead: Learn Privacy and Data Protection Law
Trailhead: Data 360 and the Ethical Use of Data

Send an alert or an event to a target based on streaming insights and engagement data to trigger an automation or data integration. The supported targets are Salesforce Platform Event, webhook, and Marketing Cloud.

When a data change occurs in Data 360 in Data Model Object (DMO) records or calculated insights, the data action sends the DataObjectDataChgEvent platform event. The platform event can be received by a subscriber, such as a flow, which performs an action based on this change. For more information, see Webhook Data Action Targets in Data 360 in the Data Cloud Reference Guide.

For more information about using a webhook as a data action target, see the Unleashing the Power of Data Actions Using a Webhook as a Target blog post in Salesforce Developers.

For more information about using actions with Flow, see the Integrating Data 360 Data Actions with Flow topic.

For more information about data actions in general, see Data Actions in Data 360 in Salesforce Help.
