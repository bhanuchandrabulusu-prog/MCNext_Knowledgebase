# Configure a Website Connector

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_qs_configure_website_connector.htm&language=en_US&type=5#persnl_qs_configure_website_connector

---

SALESFORCE PERSONALIZATION
Configure a Website Connector

To allow data to move between interactions on your website and Salesforce Personalization, you must create a connector, create a sitemap, and install the SDK that sends interaction data back to Salesforce Personalization.

Create a Connector

To send data from your website to Salesforce, you must configure a connector.

From Data Cloud Setup, search Configuration, and then click Websites & Mobile Apps.
Click New.
Enter a connector name.
From the Connector Type dropdown, select Website, and then click Save.
Create a Sitemap

A sitemap is a JavaScript file that defines the logic to capture data across different pages of your website. It's used by the SDK to collect interaction data and share it with Data 360.

In Data Cloud Setup under Configuration, click Websites & Mobile Apps.
To open the website record page, click the website.
In Sitemap, upload the file. If you change the sitemap later, to upload the new one, click Upload | Replace Sitemap.
Navigate to the location of the sitemap that you saved.
Select the file and then click Open.
Review the sitemap for errors, and save your sitemap.

For more information about Interactions SDK sitemaps, see Sitemap or review this example sitemap in Salesforce Developer Documentation.

Verify Your Data Space in SDK

A data space relates to the data streams and data graphs that are used for personalization. Out of the box, Salesforce Personalization works with the default data space. To use a different data space, you must define it via an API call.

This example shows an API call to define your data space:

SalesforceInteractions.init({
  consents: [],
  personalization: {
    dataspace: "personalizationDemo",
  },
});
SEE ALSO
Create and Upload a Sitemap
Example Sitemap
Upload a Website Sitemap to Data 360
Request Personalization Through the Sitemap
