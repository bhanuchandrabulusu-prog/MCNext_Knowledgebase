# Sample AMPscript Templates for Batch Personalization | Sample Templates

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/batch-persnl-sample-templates.html

---

After activating batch personalization decision data to Marketing Cloud Engagement (MCE), you can use AMPscript to pull decision data into MCE messages. For information about how to use AMPscript in MCE, see AMPscript for Marketing Cloud Engagement.

The data included in a batch personalization output depends on the response template linked to the personalization point that’s evaluated in a batch personalization.

You can extend the sample templates provided here to suit your data configuration. However, keep in mind that the API names of the item attributes differ depending on your data space or the naming convention if they’re custom fields.

The sample template is curated based on a personalization point with these configuration.

SAMPLE CONFIGURATION	
Type	Recommendations
Object being recommended	Knowledge Article Version
Items returned	4
Response template configuration:	
Personalization attributes	Recs_Header
Item attributes	ssot__Id__c ssot__Name__c ssot__ExternalURL__c ssot__URL__c

The sample template is curated based on a personalization point with these configuration.

SAMPLE CONFIGURATION	
Type	Recommendations
Object being recommended	Goods Product
Items returned	4
Response template configuration:	
Personalization attributes	Recs_Header
Item attributes	ssot__Id__c ssot__Name__c ImageURL__c URL__c UnitPrice__c Note: The attributes without the ssot prefix are custom attributes added to the Goods Product DMO. With proper mapping, you can add custom fields to any DMO and include them in decision responses.
