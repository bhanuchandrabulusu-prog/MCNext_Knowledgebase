# Configure a Personalization Content Schema

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_content_schema_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Personalization Content Schema

To ensure that the requesting application consistently renders your personalization output the same way, you use a personalization content schema (formerly called a response template) to define the shape of the personalization data.

Personalization content schemas are required when configuring personalization points and personalization decisions. A content schema defines the configuration options available to marketers when they’re building a personalization decision. The content schema also ensures that all decision responses for a given personalization point return data in the same format.

From the App Launcher, search for and select Personalization Content Schema.
Click New.
Select the data space that you want the personalization content schema to use.
Select a personalization type for the content schema.
PERSONALIZATION TYPE	DESCRIPTION
Recommendations	Content schemas with a recommendations personalization type are available for use on personalization points configured using a recommendations personalization type.
Dynamic Content	Content schemas with a dynamic content personalization type are available for use on personalization points configured using a dynamic content personalization type.
Enter a name for the personalization content schema and an optional description.
The API name is auto-generated.
Click Next.
Add any personalization attributes.
Each personalization attribute specifies a text entry field that appears when configuring associated personalization decisions. Using the text entry field, a marketer or business user can provide additional information that they want to return to whomever qualifies for the decision. For example, you can add an attribute for providing header text to a set of recommendations, call to action text, and a URL when providing dynamic content.
When configuring a content schema for dynamic content, click Save.
When configuring a content schema for recommendations, click Next and define the information that you want to return in a decision response.
Select the data model object (DMO) to use as a data source.
An item data graph is required to configure a recommender. When configuring a content schema for recommendations personalization types, only DMOs that are used as the root object of an item data graph are provided for selection. After you select a DMO, you can define what information about that DMO you want to return in a decision response.

By default, the primary key of the DMO is selected. Using only the primary key provides the option of rendering recommendation results using a third-party system. For example, when configuring a product recommendations strategy, you can use the primary key to return only item product IDs in a response for rendering by the receiving system.

(Optional) Select DMO fields that you want the recommender to use when providing recommendations.
You select fields by moving them from the Available DMO Fields list to the Selected DMO Fields list. All available DMO fields appear as selection options. You can use the up and down arrows to the right of the selected fields list to change the order in which fields are returned in the decision response.
Save your work.
SEE ALSO
Content Schemas
Using Content Schemas
Configure a Personalization Point
Create a Personalization Campaign
