# Daily Personalization Uniques Calculated Insight

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_daily_personalization_uniques_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Daily Personalization Uniques Calculated Insight

Personalization Intelligence Analytics requires the daily personalization uniques calculated insight.

Object Parameters
Required name: DailyPersonalizationUniques
Required API name: DailyPersonalizationUniques__cio
Insight Expression
SELECT 
   DATE_ADD(ssot__PersonalizationLog__dlm.ssot__RequestDateTime__c,0) as RequestDate__c, 
   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__IndividualId__c) as NumUniqueIndividuals__c,    APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__PersonalizationRequestId__c) as NumRequests__c,
   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__PersonalizationId__c) as NumPersonalizationRequests__c,
   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__ContentObjectAPIName__c) as NumUniqueRecordTypes__c,
   APPROX_COUNT_DISTINCT(ssot__PersonalizationLog__dlm.ssot__ContentObjectRecordId__c) as NumUniqueRecords__c
FROM
   ssot__PersonalizationLog__dlm
GROUP BY
   RequestDate__c
