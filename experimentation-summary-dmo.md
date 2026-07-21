# Experimentation Summary DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-summary-dmo.html

---

Is Primary	IsPrimary__c	Indicates if the metric is a primary metric that’s used to determine the winner of the experiment.	boolean
Last Updated Date Time	LastUpdatedDateTime__c	The date and time when the experiment summary was last updated.	dateTime
Assigned Participants Count	AssignedParticipantsCount__c	The number of participants assigned to the cohort that’s assigned to the experiment.	number
Metric Value	MetricValueNumber__c	The metric value measured as part of the experiment.	number
Min Metric Value	MinMetricValueNumber__c	The lowest value of the metric recorded during the experiment.	number
Max Metric Value	MaxMetricValueNumber__c	The highest value of the metric recorded during the experiment.	number
Mean Metric Value	MeanMetricValueNumber__c	The average metric value recorded during the experiment.	number
Variance	VarianceNumber__c	The statistical spread of metric values, calculated by taking the average of squared deviations from the mean.	number
Credible Interval Lower	CredibleIntervalLowerNumber__c	The lower value of the Bayesian credible interval. The credible interval is the range of the posterior distribution that contains the configured percentage of probable values.	number
Credible Interval Upper	CredibleIntervalUpperNumber__c	The upper value of the Bayesian credible interval.	number
Probability To Beat Control	ProbabilityToBeatControlPercent__c	The probability of the cohort for the measured metric to win against the control.	number
Probability To Beat All	ProbabilityToBeatAllPercent__c	The probability of the cohort for the measured metric to win against all the other cohorts.	number
Signal Numerator Value	SignalNumeratorValueNumber__c	The numerator of MetricValueNumber if ExperimentSummaryMetricType is either RATE or AVG.	number
Signal Denominator Value	SignalDenominatorValueNumber__c	The denominator of MetricValueNumber if ExperimentSummaryMetricType is either RATE or AVG.	number
