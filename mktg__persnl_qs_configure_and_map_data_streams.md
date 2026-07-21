# Configure and Map Data Streams

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_qs_configure_and_map_data_streams.htm&language=en_US&type=5#persnl_qs_configure_and_map_data_streams

---

SALESFORCE PERSONALIZATION
Configure and Map Data Streams

Installing the data kits add the objects and fields that store marketing data. However, the data kits only deploy datastreams used for analytics and attribution. To bring external data and make it available to your marketing tools and processes, you must deploy data streams and map them to the Data 360 objects.

The data stream names and field values are predefined by the package and can’t be changed.

Configure Web Personalization Data Streams

Now that you’ve set up your website connector, and installed and set up the SDK on your website, you need to create a data stream that pushes interaction details to Data 360.

One data stream with the category Engagement consolidates every engagement event. Each profile event is individually categorized into its own data stream with the category Profile.

In Data Cloud, navigate to the Data Streams tab, and then click New.
Under Connected Sources, click Website and then click Next.
From the Website dropdown, select the website connector you configured.
Select the events that you’d like to capture from your website, and then click Next.
Review and verify the events you selected and their associated fields, and then click Next.
Select the data space that you want to use with this data stream.
For each profile event, find the Refresh Mode dropdown and select Partial.
During this process, you can select how often to refresh the data stream. We highly recommend selecting Partial, which inserts only updated data. The Incremental option overwrites rows, which can inadvertently delete field values in certain situations.
Click Deploy.
Map Data Streams

The data streams you just created move external data into DLOs (Data Lake Objects). However, Salesforce Personalization uses data from DMOs (Data Model Objects). As a result, you must map fields from the DLOs to fields in your DMOs.

Beyond the engagement events that indicate someone’s interaction with your site, Data 360 can also use profile data for more in-depth targeting.

The process to map fields from your site into Data 360 varies for each organization. These reference documents outline the available DLO fields and recommend possible DMO mappings.

NOTE The Party Identification DMO is used as a primary key, which is used for identity resolution. A Party ID can be any unique identifier, such as a SubscriberKey, IP address, or other alphanumeric value.
Behavioral Events
Contact Point Address
Contact Point Email
Contact Point Phone
Identity Data
Party Identification Mapping
