# Integrate the Salesforce Interactions SDK | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/integrate-salesforce-interactions-sdk.html

---

You can connect Personalization to any data space, including the default data space that’s provided when you install Data Cloud. Until you create additional data spaces, all Data Cloud objects are mapped to the default data space.

To segregate your brand, region, or department data and services, create additional data spaces. To create more data spaces, you need the Data Spaces add-on license.

To create a data space, perform these steps.

Go to Data Cloud Setup.

Under Data Management, click Data Spaces.

Click New, and give the data space a unique name.

Enter a unique data space prefix, starting with a letter and including up to three alphanumeric characters.

After you save the data space, you can’t change its prefix because it becomes part of the API name used to differentiate objects that exist in multiple data spaces.

Add an optional description about the purpose of the data space.

Click Save.

See Also

Salesforce Help: Manage Data Spaces
Salesforce Help: Create a Data Space

To capture website data and control the scope of data ingestion, connect your website to Data Cloud by creating a website connector.

Go to Data Cloud Setup.
Under CONFIGURATION, click Websites & Mobile Apps.
Click New.
Provide a Connector Name.
From the Connector Type dropdown, select Website and click Save.

With Interactions SDK, you can track various types of interactions on your website, with each interaction capturing a specific set of data. When setting up a website connector to send this data to Data Cloud, you must upload a schema file in JSON format that outlines the structure of the event data you’re tracking.

The SDK provides a recommended schema file that covers common events such as adding items to a cart or viewing an item in a product catalog. This recommended schema includes mappings for:

Engagement Events
Cart Interaction Mapping
Catalog Interaction Mapping
Order Interaction Mapping
Consent Event Mapping
Profile Events
Contact Point Email Mapping
Contact Point Phone Mapping
Identity Mapping
Party Identification Mapping

To use the power of the unified event model, we suggest using the recommended schema. Alternatively, you can upload your own custom schema. Once uploaded, each interaction type appears as an object with corresponding attributes.

Download the recommended schema file or use your own custom schema file.
To upload the schema file, click Upload Schema under the Schema block.
Confirm that all events and their associated fields are populated correctly.
Click Save.

After you upload the schema, examine it for accuracy.

To change your schema at any point, click Update Schema.

You can only add new events and fields. The schema must retain all previous events and fields.

To update your schema, click Yes, Update.

To view the full schema you uploaded, click View Full Schema.

See Also

Download: Recommended Web Connector Schema (JSON)

After you’ve created a connector for your website and configured your event schema, you can install the Interactions SDK on your website.

Scroll down to the Integration Guide section of the website connector setup page.
Copy the Content Delivery Network (CDN) URL.
Add the script to the <head> section of your website’s code using a <script> tag.
Initialize the SDK using the SalesforceInteractions.init method, as described in the Initialization section of the Salesforce Interactions SDK documentation.

See Also

Capture Web Interactions
Initialization
Consent

The Web SDK sitemap is a JavaScript file that outlines the data capture logic across different pages of your website, based on which the SDK captures user interactions from your website during site navigation.

To create and upload a sitemap, perform these steps.

Install the Salesforce Interactions SDK Launcher Chrome extension.
Enable and access the Sitemap Editor on your website through the extension.
Use the Sitemap Editor to instrument your website’s sitemap.
Create a JavaScript file named sitemap.js.
Copy the sitemap code you created and paste it into this file.
Navigate to the Sitemap section of the website connector setup page.
Click Upload and upload the sitemap.js file you created.
Review the sitemap for errors, and click Save.

For more information about Interactions SDK sitemaps, see the Sitemap documentation.

Now that you’ve set up your website connector and installed and initialized the SDK on your website, create a new data stream for your website connector.

In Data Cloud, navigate to the Data Streams tab and click New.

Under Connected Sources, click Website and then click Next.

From the Website dropdown, select the website connector you configured.

Select the events that you’d like to capture from your website and click Next.

A single data stream with the category Engagement consolidates all engagement events, while each profile event is individually categorized into its own data stream with the category Profile.

Review and verify the events you selected and their associated fields.

Click Next.

If you have more than one data space, select the data space you’d like to use with this data stream from the Data Space dropdown.

For every profile event you’re capturing, use the Refresh Mode dropdown to select the data refresh mode as either Incremental or Partial.

Click Deploy.

Data ingested by all data streams is written to data lake objects (DLOs). After creating your data streams, associate your DLOs to data model objects (DMOs).

To start data mapping, access the Data Stream detail page for your newly created data stream and click Start Data Mapping. Doing so takes you to the field mapping canvas that displays your DLOs and target DMOs. To map one to another, click the name of a DLO and connect it to the desired DMO.

For your website data stream, map behavioral events and data as described in these sections.

Behavioral Events Data Mapping

Map fields in your website connector’s behavioral events DLO to the DMO.

Contact Point Address Data Mapping

Make sure that no fields are mapped in your website connector’s contact point address DLO to the DMO.

Contact Point Email Data Mapping

Map fields in your website connector’s contact point email DLO to the DMO.

Contact Point Phone Data Mapping

Map fields in your website connector’s contact point phone DLO to the DMO.

Identity Data Mapping

Map fields in your website connector’s identity DLO to the DMO.

Party Identification Data Mapping

Map fields in your website connector’s party identification DLO to the DMO.

Map fields in your website connector’s behavioral events DLO to the DMO. Behavioral event data is divided into several subsections in the mapping canvas.

Section	DLO Field	Map to DMO	DMO Field
All Event Data	dateTime	Product Browse Engagement	Created Date
		Product Browse Engagement	Engagement Date Time
		Shopping Cart Engagement	Created Date
		Shopping Cart Engagement	Engagement Date Time
		Shopping Cart Product Engagement	Created Date
		Product Order Engagement	Created Date
		Product Order Engagement	Engagement Date Time
	deviceId	Product Browse Engagement	Individual
		Shopping Cart Engagement	Individual
		Shopping Cart Product Engagement	Individual
		Product Order Engagement	Individual
	eventId (primary key)	Product Browse Engagement	Product Browse Engagement ID (primary key)
		Shopping Cart Engagement	Shopping Cart Engagement ID (primary key)
		Shopping Cart Product Engagement	Shopping Cart Engagement ID (primary key)
		Product Order Engagement	Product Order Engagement ID (primary key)
Cart	eventType	Shopping Cart Engagement	Engagement Type
	interactionName	Shopping Cart Engagement	Engagement Channel Action
Cart Item	catalogObjectId	Shopping Cart Product Engagement	Product
	catalogObjectType	Shopping Cart Product Engagement	Product Category
	currency	Shopping Cart Product Engagement	Currency
	price	Shopping Cart Product Engagement	Product Price
	quantity	Shopping Cart Product Engagement	Product Quantity
	eventType	Shopping Cart Product Engagement	Engagement Type
Catalog	id	Product Browse Engagement	Product
	interactionName	Product Browse Engagement	Engagement Channel Action
	productSku	Product Browse Engagement	Product SKU
	personalizationId	Product Browse Engagement	Personalization
	personalizationContentId	Product Browse Engagement	Personalization Content
	eventType	Product Browse Engagement	Engagement Type
Order	eventType	Product Order Engagement	Engagement Type
	interactionName	Product Order Engagement	Engagement Channel Action
	orderId	Product Order Engagement	Correlation ID
	orderTotalValue	Product Order Engagement	Adjusted Total Product Amount
	orderTotalValue	Product Order Engagement	Total Product Amount
Consent Log	Not mapped	Not mapped	Not mapped
Order Item	Not mapped	Not mapped	Not mapped

Don’t map fields in your website connector’s contact point address DLO to the DMO.

contactPointAddress DLO Field	Contact Point Address DMO Field
Not mapped	

Map these fields in your website connector’s contact point email DLO to the DMO.

contactPointEmail DLO Field	Contact Point Email DMO Field
dateTime	Created Date
deviceId (primary key)	
Contact Point Email ID (primary key)
Party

email	Email Address

Map these fields in your website connector’s contact point phone DLO to the DMO.

contactPointPhone DLO	Contact Point Phone DMO Field
dateTime	Created Date
deviceId (primary key)	
Contact Point Phone ID (primary key)
Party

phoneNumber	Telephone Number

Map these fields in your website connector’s identity DLO to the DMO.

identity DLO Field	Individual DMO Field
dateTime	Created Date
deviceId (primary key)	Individual ID (primary key)
firstName	First Name
isAnonymous	Is Anonymous
lastName	Last Name
userName	External Record ID

Map these fields in your website connector’s party identification DLO to the DMO.

partyIdentification DLO Field	Party Identification DMO Field
dateTime	Created Date
deviceId (primary key)	
Party
Party Identification ID (primary key)

IDName	Identification Name
IDType	Party Identification Type
userId	Identification Number

For more information about data mapping in Data Cloud, see Data Mapping.
