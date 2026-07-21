# Personalizer DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalizer-dmo.html

---

The Personalizer Data Model Object (DMO) defines what additional service is used to provide a complete decision response. For example, to provide a recommendations response, the personalizer uses the recommendation service to provide targeted, personalized results to visitors.

Personalizer__dlm

Personalizer (Id__c)

Field Name	Field API Name	Description	Data Type
Name	Name__c	Name applied to the Personalizer.	text
Developer Name	DeveloperName__c	Name of the Personalizer in a code-friendly format.	text
Master Label	MasterLabel__c	Primary setup object name.	text
Description	Description__c	Optional description for the Personalizer.	text
Content Object Id	ContentObjectId__c	The logical name of the object where the personalized content originated.	text
Catalog Data Graph Id	CatalogDataGraphId__c	Identifier for the data graph containing precomputed catalog data for use by the Personalizer.	text
Profile Data Graph Id	ProfileDataGraphId__c	Data graph containing precomputed profile data for use by the Personalizer.	text
Strategy	Strategy__c	Recommendation strategy selected for this personalization. For example, Top Sellers or Maximize Revenue.	text
Last Modified Date	LastModifiedDate__c	The date when a user last modified the record.	dateTime
Created Date	CreatedDate__c	The date a record was created.	dateTime
