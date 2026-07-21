# Personalization Content View Attribution DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-content-view-attribution-dmo.html

---

The Personalization Content First Touch View-Based Attribution Data Model Object (DMO) captures first-touch engagement data attributed to viewing personalized content. The data is aggregated by content.

PersnlContentFirstTouchViewAttr__dlm

Personalization Attribution Primary Key (PersonalizationAttrPk__c)

Field Name	Field API Name	Description	Data Type
Internal Organization	InternalOrganization__c	Reference ID to the business unit or other internal organization that owns the business account.	text
Data Source	DataSource__c	Reference ID for the logical name for a system that is the source of records identified by an external record ID.	text
Data Source Object	DataSourceObject__c	Reference ID for the logical name of the object where this record came from.	text
Attribution Date	AttributionDate__c	Date of the first engagement that led to the attribution.	dateTime
Data Space	DataSpace__c	The data space associated with this DMO	text
Personalization Point	PersonalizationPoint__c	Personalization point where data was gathered.	text
Personalization Decision	PersonalizationDecision__c	Personalization Decision assigned to the personalization point.	text
Personalizer	Personalizer__c	Personalizer used for the personalized response.	text
Content Object Record ID	ContentObjectRecordId	Record ID associated with this DMO.	text
Unique Profile Count	UniqueProfileCount__c	Total number of unique Personalization profiles (visitors) that viewed the personalized content.	number
Personalization Request Count	PersonalizationRequestCount__c	Total number of Personalization requests associated with the personalized content.	number
Attributed Clicks	AttributedClickCount__c	Number of clicks attributed to a particular stage in the defined personalization process.	number
Attributed Orders	AttributedOrderCount__c	Number of orders attributed to a particular stage in the defined personalization process.	number
Attributed Carts	AttributedCartsCount__c	Number of carts containing items at a particular stage in the defined personalization process.	number
Attributed Views	AttributedViewsCount__c	Number of content views attributed to a particular stage in the defined personalization process.	number
Attributed Revenue	AttributedRevenue__c	Revenue attributed to the personalization point.	number
Attributed Orders Placed	AttributedOrdersPlaced__c	Number of placed orders attributed to a particular stage in the defined personalization process.	number
