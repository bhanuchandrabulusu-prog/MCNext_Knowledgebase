# View Personalization Pipeline Metrics by Date

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_view_pipeline_metrics_by_date.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
View Personalization Pipeline Metrics by Date

This query shows various pipeline metrics grouped by date, personalization point, and personalization decision over the selected date range.

The displayed metrics include:

Number of personalization requests
Number of unique individuals
Total response time
Number of contents returned within a personalized response
Number of personalized responses provided to each individual
SELECT 
CAST(PersonalizationLog__dlm.RequestStartDateTime__c AS DATE) as RequestDate,PersonalizationPoint__dlm.Name__c as PersonalizationPoint,
PersonalizationDecision__dlm.Name__c as PersonalizationDecision,
approx_distinct(PersonalizationLog__dlm.PersonalizationId__c) as NumRequests,approx_distinct(PersonalizationLog__dlm.IndividualId__c) as UniqueIndividuals, SUM(PersonalizationLog__dlm.ResponseTimeMillis__c/COALESCE(NULLIF(PersonalizationLog__dlm.NumContentItems__c,0),1)) as TotalResponseTime,
SUM(PersonalizationLog__dlm.NumContentItems__c/COALESCE(NULLIF(PersonalizationLog__dlm.NumContentItems__c,0),1)) as NumContentItems
FROM PersonalizationLog__dlm 
 LEFT JOIN PersonalizationPoint__dlm   
 ON(PersonalizationLog__dlm.PersonalizationPointId__c = 
 PersonalizationPoint__dlm.Id__c) 
 LEFT JOIN PersonalizationDecision__dlm 
 ON(PersonalizationLog__dlm.PersonalizationDecisionId__c =  
 PersonalizationDecision__dlm.Id__c) 

GROUP BY 1,2,3
ORDER BY 1 DESC
