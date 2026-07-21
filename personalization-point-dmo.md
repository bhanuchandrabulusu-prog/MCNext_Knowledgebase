# Personalization Point DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-point-dmo.html

---

The Personalization Point Data Model Object (DMO) defines a specific personalization experience point, like a grid location in Experience Builder, that is eligible for a personalization decision.

PersonalizationPoint__dlm

Personalization Point (Id__c)

Field Name	Field API Name	Description	Data Type
Developer Name	DeveloperName__c	Name of the personalization point in a code-friendly format.	text
Name	Name__c	Name applied to the Personalization Point.	text
Description	Description__c	Optional description for the Personalization Point.	text
Personalization Schema	PersonalizationSchemaId__c	Personalization schema used by this point to define the shape of the personalized data returned by the selected decision.	text
Personalization Point Status	Status__c	Current status of the personalization point. For example, Active, Processing, or Deleting.	text
Profile Data Graph Id	ProfileDataGraphId__c	Data graph containing precomputed profile data for use by the Personalizer.	number
Source	Source__c	The Personalization source. For example, the Personalization App or Experience Builder	text
Last Modified Date	LastModifiedDate__c	The date when a user last modified the record.	dateTime
Created Date	CreatedDate__c	The date the record was created.	dateTime
