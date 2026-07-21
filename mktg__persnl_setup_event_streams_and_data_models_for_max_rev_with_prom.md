# Configure Event Streams and Data Models for Maximize Revenue with Promotions Recommenders

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_event_streams_and_data_models_for_max_rev_with_prom.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Event Streams and Data Models for Maximize Revenue with Promotions Recommenders

Set up the required event streams and data models to enable the Maximize Revenue with Promotion recommender to surface high-impact offers based on real-time engagement and purchase patterns.

To ingest promotion content into Data 360, create a data stream.
If your promotion content is stored in Salesforce, install the Loyalty Management data bundle or Global Promotions data bundle.
If your promotion content is stored outside the Promotions object in Salesforce, Configure and Map Data Streams from the source and map the resulting data to the Promotion DMO in Data Cloud.
From the SDK event stream, data streams from offline purchases, or both, record the use of promotions tied to product orders and other engagements.
For promotions based on the overall order details, store Promotion ID in the ProductOrderEngagement DMO.
For promotions tied to a line item on the order, store PromotionID in the SalesOrderProductEngagement DMO.
To prioritize promotions with indirect relationship to products, store product interactions, such as browsing or adding to cart, as engagements in Product Browse and Shopping Cart Engagement DMOs.
For engagements where an individual interacts with a promotion directly, such as clicking to add a promotion, store promotion engagements in the Website Engagement DMO. Even if promotion data is not ingested for this purpose, we’ll need this DMO for configuration.
Ingest the following events from the SDK or through another data stream.
DMO	PURPOSE
ProductBrowseEngagement	To record product browse events
ProductOrderEngagement	To record purchase orders and promotions that are used in the orders
SalesOrderProductEngagement	To record purchase order line items and, if applicable, promotions that are tied directly to a line item
ShoppingCartEngagement	To record addition and removal events on the shopping cart. Product ID can be recorded here to include line item details of an order, or you can capture the ProductId in ShoppingCartProductEngagement.
ShoppingCartProductEngagement	(Optional) To record items that are added or removed from a shopping cart. You can use this DMO or ShoppingCartEngagement to record the item details. However, if you are planning to consider cases that require an engagement-aware cart, such as an abandoned cart, we recommend using ShoppingCartProductEngagement.
Website Engagement	To record website engagement events, such as page browse, views, and clicks. If users can engage with promotions directly, for instance clicking to add a promotion, then we record such activities.
Offer Product Order Engagement	To record the relationship between an order and promotions or offers applied to the order
Offer Sales Order Product Engagement	To record the relationship between an order line items and promotions or offers applied to the order line items
Map the promotion and engagement DMOs based on the table and your business needs.
For ProductOrderEngagement and SalesOrderProductEngagement, map Offer Product Order Engagement DMO and Offer Sales Order Product Engagement DMO, respectively. This creates a one to many relationship between the order and order line items.
Map Offer Product Order Engagement DMO and Offer Sales Order Product Engagement DMO to the Promotion DMO.
For ProductBrowseEngagement, ShoppingCartEngagement, and Website Engagement DMOs, record the promotion ID directly on the engagement record as it will maintain a one to one relationship. The promotionID on these DMOs must then map to the Promotion DMO directly.
DMO	FIELD	CARDINALITY	RELATED DMO	RELATED FIELD
Product Order Engagement	Individual ID	ManyToOne	Individual	Individual.Id
Offer Product Order Engagement	Product Order Engagement ID	ManyToOne	ProductOrderEngagement	Product Order Engagement ID
Promotion ID	ManyToOne	Promotion	Promotion ID
Offer Sales Order Product Engagement	Sales Order Product Engagement ID	ManyToOne	Sales Order Product Engagement	Sales Order Product Engagement ID
Promotion ID	ManyToOne	Promotion	Promotion ID
Sales Order Product Engagement	Product Order Engagement	ManyToOne	Product Order Engagement	Product Order Engagement.Id
Product	ManyToOne	Product	Product ID
Individual ID	ManyToOne	Individual	Individual ID
Product Browse Engagement	Product SKU	ManyToOne	Product	Product ID
Shopping Cart Engagement	Product	ManyToOne	Product	Product ID
Shopping Cart Product Engagement (optional)	Individual ID	ManyToOne	Individual	Individual ID
Product	ManyToOne	Product	Product SKU
ShoppingCartEngagementEventId	ManyToOne	Shopping Cart Engagement	ShoppingCartEngagementId
Website Engagement	Individual ID	ManyToOne	Individual	Individual ID
Product	ManyToOne	Product	Product ID
Promotion	ManyToOne	Promotion	Promotion ID
SEE ALSO
Promotion DMO
Product Order Engagement DMO
Sales Order Product DMO
Shopping Cart Engagement DMO
Shopping Cart Product Engagement DMO
Product Browse Engagement DMO
Website Engagement DMO
Offer Product Order Engagement DMO
Offer Sales Order Product Engagement DMO
