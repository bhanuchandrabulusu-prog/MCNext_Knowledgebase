# Configure a Personalization Content Schema

**Source:** https://help.salesforce.com/s/articleView?id=mktg.mc_persnl_personalization_schema_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Personalization Content Schema

Personalization content schemas are required when configuring personalization points and personalization decisions. A personalization content schema defines the configuration options available to marketers when they’re building a personalization decision. The content schema also ensures that all decision responses for a given personalization point return data in the same format.

Using the personalization content schema (previously called a response template) to define the shape of the personalization data, the requesting application can consistently render the personalization output for display.

From the App Launcher, search for and select Personalization Content Schema.
Click New.
Choose how you want to get started.
To create the personalization content schema from scratch, select Manual Setup and click Next.
To import a personalization content schema from an installed data kit, select Use a Data Kit and click Next.
For the Manual Setup configuration method:
Select the data space that you want the personalization content schema to use.
Select a personalization type for the content schema.
PERSONALIZATION TYPE	DESCRIPTION
Recommendations	Content schemas with a recommendations personalization type are available for use on personalization points configured using a recommendations personalization type.
Dynamic Content	Content schemas with a dynamic content personalization type are available for use on personalization points configured using a dynamic content personalization type.
Enter a name for the personalization content schema and an optional description.
The API name is auto-generated.
Click Next.
For the Use a Data Kit configuration method:
Select a data space.
Search for or select a data kit to view its contents.
Select the personalization content schema to import.
Click Next.
(Optional) Change the name and description.
Click Next.
NOTE Only unmanaged data kits are available for this configuration method. If no unmanaged data kits contain the object, create it manually.
Add any personalization attributes.
Each personalization attribute specifies a text entry field that appears when configuring associated personalization decisions. Using the text entry field, a marketer or business user can provide additional information that they want to return to whomever qualifies for the decision. For example, you can add an attribute for providing header text to a set of recommendations, call to action text, and a URL when providing dynamic content.
When configuring a content schema for dynamic content, click Save.
When configuring a content schema for recommendations, click Next and define the information that you want to return in a decision response.
Select the data model object (DMO) to use as a data source.
An item data graph is required to configure a recommender. When configuring a recommendations content schema, only DMOs that are used as the root object of an item data graph are provided for selection. After you select a DMO, you can define what information about that DMO you want to return in a decision response.

By default, the primary key of the DMO is selected. Using only the primary key provides the option of rendering recommendation results using a third-party system. For example, when configuring a product recommendations strategy, you can use the primary key to return only item product IDs in a response for rendering by the receiving system.

(Optional) Select DMO fields that you want the recommender to use when providing recommendations.
You select fields by moving them from the Available DMO Fields list to the Selected DMO Fields list. All available DMO fields appear as selection options. You can use the up and down arrows to the right of the selected fields list to change the order in which fields are returned in the decision response.
Save your work.
SEE ALSO
Configure a Personalization Point
Personalization Point Considerations
