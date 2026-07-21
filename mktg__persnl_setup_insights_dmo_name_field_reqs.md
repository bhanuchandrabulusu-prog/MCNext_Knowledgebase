# Calculated Insight DMO Name and Field Requirements

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_insights_dmo_name_field_reqs.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Calculated Insight DMO Name and Field Requirements

How you name calculated insight DMOs and their field references depends on the data space that you configure them in. If you configure an insight in the default data space, prepend all DMO names and DMO fields with ssot__. If you’re configuring an insight in a non-default data space, prepend all DMO names and DMO fields with {prefix}__.

In this example default data space, the Daily Personalization Uniques calculated insight has ssot__ prepended to all DMO names and fields.

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

In this example non-default data space, the Daily Personalization Uniques calculated insight has {prefix}__ prepended to all DMO names and DMO fields.

SELECT 
   DATE_ADD({prefix}_PersonalizationLog__dlm.RequestDateTime__c,0) as RequestDate__c, APPROX_COUNT_DISTINCT({prefix}_PersonalizationLog__dlm.IndividualId__c) as NumUniqueIndividuals__c, 
   APPROX_COUNT_DISTINCT({prefix}_PersonalizationLog__dlm.PersonalizationRequestId__c) as NumRequests__c,
   APPROX_COUNT_DISTINCT({prefix}_PersonalizationLog__dlm.PersonalizationId__c) as NumPersonalizationRequests__c,
   APPROX_COUNT_DISTINCT({prefix}_PersonalizationLog__dlm.ContentObjectAPIName__c) as NumUniqueRecordTypes__c,
   APPROX_COUNT_DISTINCT({prefix}_PersonalizationLog__dlm.ContentObjectRecordId__c) as NumUniqueRecords__c
FROM 
   {prefix}_PersonalizationLog__dlm
GROUP BY
   RequestDate__c
