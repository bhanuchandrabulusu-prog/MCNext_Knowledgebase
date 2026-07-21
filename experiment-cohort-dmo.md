# Experiment Cohort DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experiment-cohort-dmo.html

---

IsControl	IsControl__c	Indicates if the cohort is a control cohort. An experiment can have only one controlling cohort.	boolean
Allocation Weight	AllocationWeight__c	The weight of the cohort in an experiment. The total weight for all cohorts in an experiment must equal 100.	number
Personalizer	PersonalizerId__c	Identifier for the personalization recommender.	text
Last Modified Date	LastModifiedDate__c	The date when the experiment was last modified.	date
Created Date	CreatedDate__c	The date when the experiment was created.	date
