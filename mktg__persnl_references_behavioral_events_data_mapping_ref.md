# Behavioral Events Data Mappings

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_behavioral_events_data_mapping_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Behavioral Events Data Mappings

Map fields in your website connector’s behavioral events DLO to the DMO. Behavioral event data is divided into subsections on the mapping canvas.

SECTION	DLO FIELD	MAP TO DMO	DMO FIELD
All Event Data	dateTime	Product Browse Engagement	Created Date
Product Browse Engagement	Engagement Date Time
Shopping Cart Engagement	Created Date
Shopping Cart Engagement	Engagement Date Time
Shopping Cart Product Engagement	Created Date
Product Order Engagement	Created Date
Product Order Engagement	Engagement Date Time
All Event Data	deviceId	Product Browse Engagement	Individual
Shopping Cart Engagement	Individual
Shopping Cart Product Engagement	Individual
Product Order Engagement	Individual
All Event Data	eventId (primary key)	Product Browse Engagement	Product Browse Engagement ID (primary key)
Shopping Cart Engagement	Shopping Cart Engagement ID (primary key)
Shopping Cart Product Engagement	Shopping Cart Engagement ID (primary key)
Product Order Engagement	Product Order Engagement ID (primary key)
Cart	eventType	Shopping Cart Engagement	Engagement Type
interactionName	Shopping Cart Engagement	Engagement Channel Action
Cart Item	catalogObjectId	Shopping Cart Product Engagement	Product
catalogObjectType	Shopping Cart Product Engagement	Product Category
currency	Shopping Cart Product Engagement	Currency
price	Shopping Cart Product Engagement	Product Price
quantity	Shopping Cart Product Engagement	Product Quantity
eventType	Shopping Cart Product Engagement	Engagement Type
Catalog	id	Product Browse Engagement	Product
interactionName	Product Browse Engagement	Engagement Channel Action
productSku	Product Browse Engagement	Product SKU
personalizationId	Product Browse Engagement	Personalization
personalizationContentId	Product Browse Engagement	Personalization Content
eventType	Product Browse Engagement	Engagement Type
Order	eventType	Product Order Engagement	Engagement Type
interactionName	Product Order Engagement	Engagement Channel Action
orderId	Product Order Engagement	Correlation ID
orderTotalValue	Product Order Engagement	Adjusted Total Product Amount
orderTotalValue	Product Order Engagement	Total Product Amount
