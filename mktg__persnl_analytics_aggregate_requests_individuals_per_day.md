# Aggregate the Requests Served to Individuals per Day

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_aggregate_requests_individuals_per_day.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Aggregate the Requests Served to Individuals per Day

This query gets the number of requests served and how many individuals received those requests on a daily basis.

SELECT
DATE_TRUNC('day',RequestDateTime__c) as Day,
COUNT(DISTINCT PersonalizationRequestId__c) as NumRequests,
COUNT(DISTINCT IndividualId__c) as UniqueIndividuals
FROM
PersonalizationLog__dlm
GROUP BY
1
ORDER BY
1
