# Configure Profile Data Graph for the Maximize Revenue with Promotion Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_profile_dg_for_max_rev_with_prom.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Profile Data Graph for the Maximize Revenue with Promotion Recommender

To use the Maximize Revenue with Promotions recommender, make sure that you include these related objects and fields to capture product and promotion engagement data.

To create a profile data graph, use the instructions in Create a Data Graph, but select the fields and objects listed here.

Select Unified Link Individual, and click + to add it.
Select Individual, and click +.
Add Product Browse Engagement, Product Order Engagement, Shopping Cart Engagement, and Website Engagement to the data graph.
(Optional) Next to Shopping Cart Engagement, click + and select Shopping Cart Product Engagement.
Next to Product Order Engagement, click + and select Sales Order Product Engagement and Offer Product Order Engagement.
Next to Sales Order Product Engagement, click + and select Offer Sales Order Product Engagement.
(Optional) To include segment membership in filter criteria, look for Unified Individual, click + and select Unified Individual - Latest.
Select these related objects, and add the required fields.
NOTE Some fields are preselected for some objects. Leave those fields selected.
RELATED OBJECT	FIELD NAME	FIELD API NAME
Product Browse Engagement	Created Date	ssot__CreatedDate__c
Product Id	ssot__ProductId__c
Individual ID	ssot__IndividualId__c
Product Order Engagement	Created Date	ssot__CreatedDate__c
Individual ID	ssot__IndividualId__c
Adjusted Total Product Amount	ssot__AdjustedTotalProductAmount__c
Sales Order Product Engagement	Created Date	ssot__CreatedDate__c
Product	ssot__ProductId__c
Shopping Cart Engagement	Created Date	CreatedDate__c
Product	Product__c
Individual ID	ssot__IndividualId__c
Offer Product Order Engagement	Promotion	PromotionId__c
OfferSalesOrderProductEngagement	Promotion	PromotionId__c
Website Engagement	Created Date	ssot__CreatedDate__c
Individual ID	ssot__IndividualId__c
Promotion ID	ssot__PromotionId__c

Here's a sample profile data graph:

In the profile data graph, add the direct or related attributes that you want to use for decision targeting or recommendation filters.
Add the Data 360 segments or insights that you want to use when making targeting decisions.
To review the structure of the JSON blob, click Preview.
Save and build the data graph.
