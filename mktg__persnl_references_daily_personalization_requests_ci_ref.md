# Daily Personalization Requests Calculated Insight

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_daily_personalization_requests_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Daily Personalization Requests Calculated Insight

Personalization Intelligence Analytics requires the daily personalization requests calculated insight.

Object Parameters
Required name: DailyPersonalizationRequests
Required API name: DailyPersonalizationRequests__cio
Insight Expression
SELECT
   DATE_ADD(ssot__PersonalizationLog__dlm.ssot__RequestDateTime__c, 0) as RequestDate__c,
   ssot__PersonalizationLog__dlm.ssot__PersonalizationPointId__c as PersonalizationPointId__c,
   ssot__PersonalizationPoint__dlm.ssot__Name__c as PersonalizationPointName__c,
   ssot__PersonalizationLog__dlm.ssot__PersonalizationType__c as PersonalizationType__c,
   ssot__PersonalizationLog__dlm.ssot__PersonalizationDecisionId__c as PersonalizationDecisionId__c,
   ssot__PersonalizationDecision__dlm.ssot__Name__c as PersonalizationDecisionName__c,
   ssot__PersonalizationLog__dlm.ssot__PersonalizerId__c as PersonalizerId__c,
   ssot__Personalizer__dlm.ssot__Name__c as PersonalizerName__c,
   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__PersonalizationRequestId__c) as NumRequests__c,   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__PersonalizationId__c) as NumPersonalizationRequests__c,
   SUM(ssot__PersonalizationLog__dlm.ssot__ResponseTimeMillisecond__c / IFNULL(NULLIF(ssot__PersonalizationLog__dlm.ssot__ContentItemsQuantity__c, 0), 1)) as TotalResponseTimeMilliseconds__c,
   SUM(ssot__PersonalizationLog__dlm.ssot__ContentItemsQuantity__c / IFNULL(NULLIF(ssot__PersonalizationLog__dlm.ssot__ContentItemsQuantity__c, 0), 1)) as NumContentItems__c,
   SUM(ssot__PersonalizationLog__dlm.ssot__ContentLengthBytesNumber__c) as TotalContentLength__c
FROM
   ssot__PersonalizationLog__dlm
LEFT JOIN
   ssot__PersonalizationPoint__dlm ON (ssot__PersonalizationLog__dlm.ssot__PersonalizationPointId__c = ssot__PersonalizationPoint__dlm.ssot__Id__c)
LEFT JOIN
   ssot__PersonalizationDecision__dlm ON (ssot__PersonalizationLog__dlm.ssot__PersonalizationDecisionId__c = ssot__PersonalizationDecision__dlm.ssot__Id__c)
LEFT JOIN
   ssot__Personalizer__dlm ON (ssot__PersonalizationLog__dlm.ssot__PersonalizerId__c = ssot__Personalizer__dlm.ssot__Id__c)
GROUP BY
   RequestDate__c,
   PersonalizationPointId__c,
   PersonalizationPointName__c,
   PersonalizationType__c,
   PersonalizationDecisionId__c,
   PersonalizationDecisionName__c,
   PersonalizerId__c,
   PersonalizerName__c
