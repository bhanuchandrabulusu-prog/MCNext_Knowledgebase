# Limits for Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_basics_limits.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Limits for Salesforce Personalization

Learn about Salesforce Personalization limits.

PERSONALIZATION FUNCTION	CATEGORY	FEATURE	VALUE
Recommenders	Resources	Recommenders per Salesforce org (across all data spaces). To discuss increasing this limit, contact Salesforce Customer Support.	

10

1 objective-based recommender with the Salesforce Personalization Card.


Full recommender data refresh frequency	Daily
Maximum number of recommendation requests per minute per tenant	60000
Recommendations	Maximum number of recommendations to return	24
Maximum number of recommender objectives you can configure per org	10
Filters	Maximum number of filter conditions for an include or exclude filter	10
Maximum number of item data graph calculated insight values (dimensions + measures) considered for recommendation	Top 100 values
Maximum number of filter values from the profile data graph considered per filter condition	100
Maximum number of values considered from a DMO when performing filter comparisons	100
Maximum number of direct related objects to the root DMO per item data graph	20
Engagement	Engagement Signals	Maximum number of engagement signals used for model training per objective-based recommender	25
Maximum number of engagement signals per org	100
Maximum number of engagement signals per data space	100
Maximum number of engagement signal filters per engagement signal	10
Maximum number of related DMOs per engagement signal	1
Number of referenced field levels allowed when referencing an engagement signal in a data graph	

3

For example, DMO (unified individual) > field level 1 (individual) > field level 2 (product browse engagement) > field level 3 (sales order product engagement)


Engagement Signal Metrics and Compound Metrics	Maximum number of engagement signal metrics per org	100
Maximum number of engagement signal compound metrics per org	100
Maximum number of engagement signal metrics per data space	100
Maximum number of engagement signal compound metrics per data space	100
Maximum number of engagement signal metrics per engagement signal	10
Attributions	Resources	Maximum number of attribution models per org (across all data spaces; including active and inactive models)	20
Maximum number of attribution models per data space	10
Stages	Maximum number of stages per attribution configuration	4
Engagement Signals and Metrics	Number of engagement signals per attribution stage	1
Maximum number of engagement signal metrics per attribution configuration	5
Batch Personalizations	Resources	Maximum number of active batch personalization jobs per Salesforce org	20
Personalization Points	Personalization Decisions	Maximum number of decisions per personalization point	25
Maximum number of targeting conditions per decision or experiment	50
Maximum number of merge fields across personalization attribute fields per decision	10
