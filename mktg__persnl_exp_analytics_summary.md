# Experiment Summary

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_analytics_summary.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Experiment Summary

The second section of the experiment dashboard shows the experiment summary metrics. These metrics provide participant totals for the control cohort and all variant cohorts. When compared against the control or against other variations (when no control is used), individual activity totals and lift values for each variant are provided as percent differences.

COLUMN	DESCRIPTION
Cohorts	The names of each experiment cohort.
Personalizer	The name of the recommender tested for this cohort. If a recommender isn’t used for a cohort, the Personalizer table cell is left blank.
Number of Individuals	Total number of individuals selected to participate in this cohort.
User-Defined Metric	This column name varies depending on the metric defined for the experiment. For example, this column can report revenue or recommendation click-through rate.
Lift	Percent difference of the tested metric when compared to the control or across all variation cohorts.
Chance to Beat Control	Probability that a cohort’s content is better than the control, based on the observed data. Multiple variation cohorts can beat the control. This column applies only to the primary metric.
Chance to Beat All	Probability that a cohort’s content is better than every other content in the experiment, based on the observed data. Only one variation cohort can beat all. This column appears only when no control is configured for the experiment.
SEE ALSO
Using Experiment Analytics
Experiment Status and Controls
Primary Metric Results
Secondary Metric Results
Troubleshooting Experiment Analytics
