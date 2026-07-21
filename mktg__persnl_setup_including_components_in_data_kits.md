# Including Personalization Components in Data Kits

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_including_components_in_data_kits.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Including Personalization Components in Data Kits

To streamline installations and deploy more complete solutions for Salesforce Personalization, add packageable personalization components to a Data 360 data kit. You can publish the data kit using Package Manager, and then deploy your customized solution in Data 360.

Packageable Personalization components include:

Personalization Recommenders
Engagement Signals
Personalization Objectives

When you add personalization components to a package, keep these considerations in mind:

All required objects that are related with configuring the component are automatically added. For example, when you add an objective-based recommender to a package, the underlying objective, engagement signals, mapped DMOs, and data graph relationships are also added.
Even though data graph relationships are included when you add a personalization component, specific related and mapped objects aren’t included with the data graph. Always add any mapped objects to the data kit you’re creating, or confirm that the objects already exist in the org where you plan to install the data kit.
Packages don’t currently support adding filters.

For more details, see Data Kits in Data 360 Help.

SEE ALSO
Salesforce Help: Create a Data Kit
Salesforce Help: Publish a Data Kit
Salesforce Help: Deploy Data Kit Components in Data 360
