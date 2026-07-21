# Prerequisites for the Personalization Campaign Guided Configuration

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_campaign_prereq.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Prerequisites for the Personalization Campaign Guided Configuration

Before using the guided campaign configuration, we recommend that you verify certain required components are in place. Having these components defined can make for a more efficient and streamlined configuration experience.

Contact your Salesforce admin to verify that these components are configured before you begin.

COMPONENT	DOCUMENTATION	NOTES
Data Space	About Data Spaces	All Salesforce orgs running Data 360 have a default data space.
Profile Data Graph	Create Required Data Graphs	You can choose from only profile data graphs that are configured in the data space you select.
Data 360 Web Connector	Configure a Data 360 Web Connector	Only web marketing channel deployment is currently supported. When configuring the Data 360 Web Connector, make sure to define the optional base URL setting. Personalization uses the URL when launching the Web Personalization Manager (WPM) to test and deploy the campaign.
Personalization Content Schema (formerly called Response Templates)	Configure a Personalization Content Schema	Only content schemas configured using the dynamic content personalization type are currently supported.
Experience Templates	Experience Templates	Experience templates provide structural layout for how personalized content, such as a hero banner or product carousel, appears to customers. A template transforms raw data from personalization into specific variables, such as a product name or image URL, with the help of a guided interface.
SEE ALSO
Using the Personalization Campaign Guided Configuration
Create a Personalization Campaign
Map a Campaign Using Web Personalization Manager
