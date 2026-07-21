# Query Personalization Attribution by Personalization Point

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_query_personalization_attribution_by_personalization_point.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Query Personalization Attribution by Personalization Point

This query shows attribution by personalization point over a specified date range. It includes the number of unique profiles, total number of clicks and attributed orders, and attributed revenue by date.

SELECT 
AttributionDate__c,
PersonalizationDecision__c,
PersonalizationPoint__c,
Personalizer__c,
SUM(PersonalizationRequestCount__c) as personalization_requests,
SUM (UniqueProfileCount__c) as unique_individuals,
SUM (AttributedViewsCount__c) as views,
SUM (AttributedClicksCount__c) as clicks,
SUM (AttributedCartsCount__c) as carts,
SUM (AttributedOrdersCount__c) as orders,
SUM(AttributedOrdersCount__c) / NULLIF(SUM(AttributedViewsCount__c), 0)*100 as orderConversionRate,
SUM (AttributedRevenue__c) as revenue
FROM scm_PersonalizationPointViewAttribution__dlm
WHERE  AttributionDate__c >= date('2024-01-01') AND AttributionDate__c <= date('2024-04-01')
GROUP BY 1,2,3,4
ORDER BY AttributionDate__c ASC;
