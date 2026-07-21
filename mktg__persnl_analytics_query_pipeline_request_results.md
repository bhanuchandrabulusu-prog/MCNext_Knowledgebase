# Get Information About Personalization Pipeline Requests

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_query_pipeline_request_results.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Get Information About Personalization Pipeline Requests

This query retrieves who made the request and when, the response time, and which content was returned.

SELECT
substr(to_iso8601(RequestDateTime__c),1,19) as DateTime,
PersonalizationRequestId__c as PersonalizationRequestId,
IndividualId__c as IndividualId,
PersonalizationPointId__c as PersonalizationPoint,
ResponseTimeMillisecond__c as ResponseTime,
TargetObjectLabelText__c as TargetObjectLabel,
TargetObjectRecordId__c as TargetObjectRecordId
FROM
PersonalizationLog__dlm
WHERE
PersonalizationRequestId__c ='fcf77347-44c2-4e84-952f-10391a5a9df9'
