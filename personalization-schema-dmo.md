# Personalization Schema DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-schema-dmo.html

---

The Personalization Schema Data Model Object (DMO) defines how personalized results are presented to visitors. For example, the schema can present personalized results as a list of product recommendations, or present manually-defined information, like specific record data, a call to action banner, or an image.

PersonalizationSchema__dlm

Personalization Schema (Id__c)

Field Name	Field API Name	Description	Data Type
Name	Name__c	Name applied to the Personalization Schema.	text
Description	Description__c	Optional description for the Personalization Schema.	text
Personalization Type	PersonalizationType__c	The type of personalization presented to the visitor. For example, Recommendations or Manual Content.	text
Content Object	ContentObject__c	The logical name of the object where the personalized content originated.	text
Last Modified Date	LastModifiedDate__c	The date when a user last modified the record.	dateTime
Created Date	CreatedDate__c	The date a record was created.	dateTime
