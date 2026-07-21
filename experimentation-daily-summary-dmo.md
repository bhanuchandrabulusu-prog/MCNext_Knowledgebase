# Experimentation Daily Summary DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-daily-summary-dmo.html

---

Is Primary	IsPrimary__c	Indicates if the metric is a primary metric, which is used to determine the winner of the experiment.	boolean
For Date	ForDate__c	The date when the summary was created.	date
Last Updated Date Time	LastUpdatedDateTime__c	The date and time when the daily summary was last updated.	dateTime
Assigned Participants Count	AssignedParticipantsCount__c	The number of participants assigned to the cohort on the day the daily summary was created.	number
Metric Value	MetricValueNumber__c	The metric value measured as part of the experiment.	number
Signal Numerator Value	SignalNumeratorValueNumber__c	The numerator of MetricValueNumber if ExperimentSummaryMetricType is either RATE or AVG.	number
Signal Denominator Value	SignalDenominatorValueNumber__c	The denominator of MetricValueNumber if ExperimentSummaryMetricType is either RATE or AVG.	number
