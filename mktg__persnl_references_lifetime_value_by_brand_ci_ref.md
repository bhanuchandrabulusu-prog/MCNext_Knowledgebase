# Lifetime Value by Brand and Category Calculated Insight

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_lifetime_value_by_brand_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Lifetime Value by Brand and Category Calculated Insight

This insight calculates a sum of the lifetime value. You can filter the insight by brand or category.

When creating this insight, use the instructions in Create a Calculated Insight Using SQL in Data 360 documentation. You can then add the insight to the Salesforce Personalization near real-time item data graph.

SELECT
   UnifiedIndividual__dlm.ssot__Id__c as unifiedindividualid__c, ssot__GoodsProduct__dlm.ssot__BrandId__c as Brand__c, ssot__GoodsProduct__dlm.ssot__PrimaryProductCategory__c as Category__c, 
   SUM(ssot__ProductOrderEngagement__dlm.ssot__NetOrderAmount__c) as ltv__c 
FROM 
   UnifiedIndividual__dlm 
JOIN
   IndividualIdentityLink__dlm 
ON
   UnifiedIndividual__dlm.ssot__Id__c = IndividualIdentityLink__dlm.UnifiedRecordId__c 
JOIN
   ssot__ProductOrderEngagement__dlm 
ON
   IndividualIdentityLink__dlm.SourceRecordId__c = ssot__ProductOrderEngagement__dlm.ssot__IndividualId__c 
JOIN
   ssot__SalesOrderProductEngagement__dlm 
ON 
   ssot__ProductOrderEngagement__dlm.ssot__Id__c = ssot__SalesOrderProductEngagement__dlm.ssot__ProductOrderEngagementId__c 
JOIN
   ssot__GoodsProduct__dlm 
ON
   ssot__GoodsProduct__dlm.ssot__Id__c = ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c 
GROUP BY
   unifiedindividualid__c, ssot__GoodsProduct__dlm.ssot__BrandId__c, ssot__GoodsProduct__dlm.ssot__PrimaryProductCategory__c
