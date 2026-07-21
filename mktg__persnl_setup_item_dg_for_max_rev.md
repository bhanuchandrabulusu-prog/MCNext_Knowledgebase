# Configure Item Data Graph for the Maximize Revenue Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_item_dg_for_max_rev.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Item Data Graph for the Maximize Revenue Recommender

When configuring an item data graph for use with the Maximize Revenue recommender, make sure to include these related objects and fields. The Maximize Revenue recommender uses the Product Sales calculated insight. Configure the insight before creating the item data graph.

Use the instructions in the Create a Data Graph Data 360 documentation to create a near real-time item data graph.

Configure the Product Sales calculated insight.
The Maximize Revenue recommender uses the SQL code included in the calculated insight. See Configure the Top Sellers Standard Insight for Rule-Based Recommenders.
Create the data graph using these related objects and fields.

Unit Price and Image URL are custom fields. If you don’t see them, add them. See Add Custom Fields to the Goods Product Data Model Object.

RELATED OBJECT	FIELD NAME	FIELD API NAME
Goods Product	Product SKU	ProductSKU__c
Primary Product Category	PrimaryProductCategory__c
Name	Name__c
Description	Description__c
Is Sellable	IsSellable__c
Unit Price	UnitPrice__c
Image URL	ImageUrl__c
Add the calculated insight containing the required SQL code to the item data graph.
Add the SalesOrderProductEngagement related object and TotalSoldUnits field to the data graph.
To view the JSON blob structure, click Preview.
Click Save and Build.
