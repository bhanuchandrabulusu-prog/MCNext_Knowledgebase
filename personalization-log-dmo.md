# Personalization Log DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalization-log-dmo.html

---

The Personalization Log Data Model Object (DMO) captures data from various data sources about engagement with Personalization.

PersonalizationLog__dlm

Personalization Log Id (Id__c)

Field Name	Field API Name	Description	Data Type
Personalization Content Id	PersonalizationContentId__c	Personalization content record ID for the content provided.	text
Personalization Id	PersonalizationId__c	Identifier for the personalized response sent to a specific personalization point.	text
Personalization Request Id	PersonalizationRequestId__c	Unique identifier for the Personalization request.	text
Request Start DateTime	RequestStartDateTime__c	Date and time the Personalization request was made.	dateTime
Augmenting Stage Time Millis	AugmentingStageTimeMillis__c	Amount of time, in milliseconds, it took to look up and augment a profile.	number
Qualifying Stage Time Millis	QualifyingStageTimeMillis__c	Amount of time, in milliseconds, it took to qualify a profile for a Personalization response.	number
Personalizing Stage Time Millis	PersonalizingStageTimeMillis__c	Amount of time, in milliseconds, it took to retrieve content for all personalization decisions.	number
Response Time Millis	ResponseTimeMillis__c	Amount of time, in milliseconds, it took to respond to the Personalization request.	number
Individual	IndividualId__c	Individual DMO ID.	text
Personalization Type	PersonalizationType__c	The type of personalization presented to the visitor. For example, Recommendations or Manual Content.	text
Personalization Point Id	PersonalizationPointId	The ID of the personalization point in the personalization request.	text
Personalization Decision Id	PersonalizationDecisionId	The ID of the personalization decision in the personalization request.	text
Personalizer Id	PersonalizerId	The ID of the personalizer used to call a personalization service, if required. The personalizer determines what service to use, gathers any other required data, and generates a personalized response.	text
Content	Content	Raw content returned by the personalization request. For example, a data element in the array.	text
Content Length	ContentLength	Length of the content field in abstract units for use in comparative analysis.	number
Number of Content Items	NumContentItems	Number of content items returned by the personalization request.	number
DMO Label	DmoLabel	Label assigned to the DMO. For example, Goods Product.	text
DMO API Name	DmoApiName	The DMO name in code-friendly format. For example, ssot_GoodsProduct_dlm.	text
DMO Record Id	DmoRecordId	The record ID of the DMO. For example, RedSoxBallCap.
