# Configure an Engagement Signal Metric

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_metrics_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure an Engagement Signal Metric

Engagement signal metrics enable you to track and view user engagement with your personalized content. Use these metrics when creating custom objectives for objective-based recommenders and when creating attribution configurations.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure engagement signal metrics:	Engagement Signals

When creating engagement signal metrics, keep these considerations in mind.

For each engagement signal that you configure, a count-based engagement signal metric is created by default. You can use this metric like any other engagement signal metric that you add to the engagement signal.
For count metric aggregation, note that ingesting the same event from multiple data streams can result in duplicate events being counted in the DMO. If you expect duplication to occur in your engagement DMOs, we recommend using DISTINCT to avoid duplicate counting.
You can select how to quantify, or aggregate, metrics using various operators.
METRIC AGGREGATION	DESCRIPTION	EXAMPLE	SUPPORTED IN
COUNT	Counts all entries for a metric.	

The total number of times an email link is clicked.

In practice, this value is determined by counting the total number of engagement events (rows) that appear in the email engagement DMO.

	
Custom Objectives
Custom Attribution Configurations
Experimentation

SUM	Adds data values across all event occurrences.	Purchases greater than a specified value.	
Custom Attribution Configurations
Experimentation

AVG	Averages data values across all event occurrences.	Average sales less than a specified value.	
Custom Attribution Configurations
Experimentation

DISTINCT	Counts the number of unique values after eliminating duplicate entries.	

The number of unique products added to a cart.

In practice, this value is determined by counting distinct products added to a cart using the engagement asset ID from the shopping cart engagement DMO.

	
Custom Attribution Configurations
Experimentation

SELECT	Enables models to aggregate and consider the value of an attribute for training, not just it’s count.	Using the Net Order Amount field from the Shopping Cart Engagement DMO to maximize its value in a custom objective recommender.	
Custom Objectives
Custom Attribution Configurations (API only)
From the App Launcher, search for and select Engagement Signals.
Open an engagement signal that you want to add an engagement signal metric to.
In the engagement signal object Related tab, from the Engagement Signal Metrics list, click New.
Name the engagement signal metric and provide an optional description.
Select a metric aggregation from the Aggregate menu.
Select a DMO field that you want to track and view.
Save your work.
SEE ALSO
Example Engagement Signal Metrics
Configure an Engagement Signal Compound Metric
