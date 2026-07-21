# Personalization Point View Attribution DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-point-view-attribution-dmo.html

---

The Personalization Point First Touch View-Based Attribution Data Model Object (DMO) captures first-touch engagement data attributed to viewing personalized content. The data is aggregated by personalization point.

PersnlPointFirstTouchViewAttr__dlm

Personalization Attribution Primary Key (PersonalizationAttrPk__c)

Field Name	Field API Name	Description	Data Type
Internal Organization	InternalOrganization__c	Reference ID to the business unit or other internal organization that owns the business account.	text
Data Source	DataSource__c	Reference ID for the logical name for a system that is the source of records identified by an external record ID.	text
Data Source Object	DataSourceObject__c	Reference ID for the logical name of the object where this record came from.	text
Attribution Date	AttributionDate__c	Date of the first engagement that led to the attribution.	dateTime
Data Space	DataSpace__c	Data space used as the personalization content source.	text
Root Personalization Point	RootPersonalizationPoint__c	Personalization point where data was gathered.	text
Personalization Decision	PersonalizationDecision__c	Personalization decision assigned to the Personalization point.	text
Personalizer	Personalizer__c	Personalizer used for the personalized response.	text
Unique Profile Count	UniqueProfileCount__c	Total number of unique personalization profiles (visitors) that interacted with the personalization point.	number
Personalization Request Count	PersonalizationRequestCount__c	Total number of Personalization requests launched from the personalization point.	number
Attributed Clicks	AttributedClickCount__c	Number of content clicks attributed to personalization views.	number
Attributed Orders	AttributedOrderCount__c	Number of orders attributed to personalization views.	number
Attributed Carts	AttributedCartsCount__c	Number of add to cart actions attributed to personalization views.	number
Attributed Views	AttributedViewsCount__c	Number of orders attributed to personalization views.	number
Attributed Revenue	AttributedRevenue__c	Revenue attributed to the personalization point.	number
Attributed Orders Placed	AttributedOrdersPlaced__c	Number of placed orders attributed to the personalization point.	number
