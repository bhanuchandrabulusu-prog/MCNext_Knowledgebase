# Personalization Decision DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-decision-dmo.html

---

The Personalization Decision Data Model Object (DMO) defines all object properties required to make personalized decisions for a Personalization point. Properties include eligibility criteria (targeting rules), priority settings, and so on.

PersonalizationDecision__dlm

Personalization Decision (Id__c)

Field Name	Field API Name	Description	Data Type
Developer Name	DeveloperName__c	Name of the personalization decision in a code-friendly format.	text
Name	Name__c	Name applied to the Personalization Decision.	text
Description	Description__c	Optional description for the Personalization Decision.	text
Personalization Point	PersonalizationPointId__c	Personalization point using the decision.	text
Personalizer	PersonalizerId__c	Name applied to the associated Personalizer.	text
Priority	PersonalizationDecisionPriority__c	Priority value assigned to the decision at the Personalization Point.	number
Criteria	Criteria__c	Targeting rules associated with the personalization decision.	text
Last Modified Date	LastModifiedDate__c	The date when a user last modified the record.	dateTime
Created Date	CreatedDate__c	The date a record was created.	dateTime
