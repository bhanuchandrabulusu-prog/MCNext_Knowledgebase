# Configure an Engagement Signal Compound Metric

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_compound_metrics_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure an Engagement Signal Compound Metric

Engagement signal compound metrics are rate metrics. You create them by combining two single metrics, a numerator and a denominator, using a Divide By function to create a ratio.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure engagement signal compound metrics:	Engagement Signals

When creating engagement signal compound metrics, keep these considerations in mind.

Before creating a compound metric, make sure to have at least two single metrics configured for the engagement signal that you’re creating the compound metric on.
The single metric fields that you select to build a compound metric must logically function as a ratio for a rate-focused compound metric. For example, recommender clicks/recommender views to build a recommendations click-through rate compound metric.
From the App Launcher, search for and select Engagement Signals.
Open an engagement signal that you want to add an engagement signal compound metric to.
In the engagement signal object Related tab, from the Engagement Signal Compound Metrics list, click New.
Name the engagement signal compound metric and provide an optional description.
The Engagement Signal Compound Metric API Name is auto-generated.
From the first Engagement Signal Metric menu, select a metric that you want to use as the numerator for the compound metric.
Select the Divide By operator from the Operator menu.
From the last Engagement Signal Metric menu, select a metric that you want to use as the denominator for the compound metric.
Save your work.
SEE ALSO
Example Engagement Signal Compound Metrics
Configure an Engagement Signal Metric
