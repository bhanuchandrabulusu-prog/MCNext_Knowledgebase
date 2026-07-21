# Personalization Point Click Attribution DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-point-click-attribution-dmo.html

---

The Personalization Point Last Touch View-Based Attribution Data Model Object (DMO) captures last-touch engagement data attributed to viewing personalized content. The data is aggregated by personalization point.

PersnlPointLastTouchViewAttr__dmo

Personalization Attribution Primary Key (PersonalizationAttrPk__c)

Field Name	Field API Name	Description	Data Type
Internal Organization	InternalOrganization__c	Reference ID to the business unit or other internal organization that owns the business account.	text
Data Source	DataSource__c	Reference ID for the logical name for a system that is the source of records identified by an external record ID.	text
Data Source Object	DataSourceObject__c	Reference ID for the logical name of the object where this record came from.	text
Attribution Date	AttributionDate__c	Date of the first engagement that led to the attribution.	dateTime
Data Space	DataSpace__c	The data space associated with this DMO	text
Personalization Point	PersonalizationPoint__c	Personalization point where the attribution occurred.	text
Personalization Decision	PersonalizationDecision__c	Personalization Decision associated with the Personalization point.	text
Personalizer	Personalizer__c	Personalizer used for the personalized response.	text
Unique Profile Count	UniqueProfileCount__c	Total number of unique Personalization profiles (visitors) that interacted with the Personalization Point.	number
Personalization Request Count	PersonalizationRequestCount__c	Total number of Personalization requests launched from the Personalization Point.	number
Attributed Clicks	AttributedClicksCount__c	Number of clicks on personalized content.	number
Attributed Carts	AttributedCartsCount__c	Number of add to cart actions attributed to personalization clicks.	number
Attributed Revenue	AttributedRevenue__c	Revenue attributed to the personalization point.	number
Attributed Orders Placed	AttributedOrdersPlaced__c	Number of orders attributed to clicks on personalized content.	number
