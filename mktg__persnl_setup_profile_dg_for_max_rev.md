# Configure Profile Data Graph for the Maximize Revenue Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_profile_dg_for_max_rev.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Profile Data Graph for the Maximize Revenue Recommender

To use the maximize revenue recommender with a profile data graph for a retail environment, you add certain objects and fields to the profile data graph.

Before configuring a profile data graph for use with the maximize revenue recommender:

Make sure to create and map these required fields to their respective data model objects (DMOs).
DMO	REQUIRED FIELD
SalesOrderProductEngagement	SalesOrderProductEngagement.ProductOrderEngagementId
ProductOrderEngagement	ProductOrderEngagement.Id
For the Sales Order Product Engagement object relationships, create a N:1 (ManyToOne) active relationship between its Product Order Engagement Id field and the Product Order Engagement Id field of the Product Order Engagement object.
OBJECT	FIELD	CARDINALITY	RELATED OBJECT	RELATED FIELD
Sales Order Product Engagement	Product Order Engagement	ManyToOne	Product Order Engagement	Product Order Engagement Id
(Optional) For the Shopping Cart Product Engagement object relationships, create an N:1 (ManyToOne) active relationship between its Shopping Cart Engagement field and the Shopping Cart Engagement Id field of the Shopping Cart Engagement object.
OBJECT	FIELD	CARDINALITY	RELATED OBJECT	RELATED FIELD
Shopping Cart Product Engagement	Shopping Cart Engagement	ManyToOne	Shopping Cart Engagement	Shopping Cart Engagement Id

Use the instructions in Create a Data Graph, but select the fields and objects listed here.

Select Unified Link Individual, and click + to add it.
Select Individual, and click + to add it
Add Product Browse Engagement, Product Order Engagement, and Shopping Cart Engagement to the data graph.
Next to Product Order Engagement, click + and then select Sales Order Product Engagement.
(Optional) Next to Shopping Cart Engagement, click + and then select Shopping Cart Product Engagement.
Select these related objects, and add the required fields.
NOTE Some fields are preselected for some objects. Leave those fields selected.
RELATED OBJECT	FIELD NAME	FIELD API NAME
Product Browse Engagement	Created Date	CreatedDate__c
Product Id	ProductId__c
Product Brand	ProductBrand__c
Product Category Name	ProductCategoryName__c
Engagement Channel Action	EngagementChannelAction__c
Product Order Engagement	Created Date	CreatedDate__c
Individual ID	IndividualId__c
Sales Order Product Engagement	Created Date	CreatedDate__c
Product	Product__c
Ordered Quantity	OrderedQuantity__c
Product Price Amount	ProductPriceAmount__c
Shopping Cart Engagement	Created Date	CreatedDate__c
Product	Product__c
Product Brand	ProductBrand__c
Product Category Name	ProductCategoryName__c
ShoppingCartProductEngagement	Individual Id	IndividualId__c
Created Date	CreatedDate__c
Product Id	ProductId__c
Add the direct or related attributes that you want to use for decision targeting or recommendation filters.
Add the Data 360 segments or insights that you want to use when making targeting decisions.
To review the structure of the JSON blob, click Preview.
Save and build the data graph.
