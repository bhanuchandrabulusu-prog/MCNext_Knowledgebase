# Example Engagement Signal Metrics

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_metrics_examples.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example Engagement Signal Metrics

Use these examples to create engagement signal metrics. You can use count metrics to define compound engagement signal rate metrics.

NOTE The count metrics in this table are created automatically if you configure the engagement signals described in Example Engagement Signals.
ENGAGEMENT SIGNAL	ENGAGEMENT SIGNAL METRIC NAME	AGGREGATION FUNCTION	FIELD SELECTION
Product View	Count ProductView	Count	Product Browse Engagement > Product Browse Engagement Id
Product View	Count ProductClick	Count	Product Browse Engagement > Product Browse Engagement Id
Add to Cart	Add to Cart Count	Count	Shopping Cart Product Engagement > Shopping Cart Product Engagement Id
Product Order	Revenue	Sum	Product Order Engagement > Adjusted Total Product Order Amount
Article Click	Click Count	Count	Knowledge Article Engagement > Knowledge Article Engagement Id
SEE ALSO
Configure an Engagement Signal Metric
Configure an Engagement Signal Compound Metric
