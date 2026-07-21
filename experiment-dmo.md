# Experiment DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experiment-dmo.html

---

Personalization Schema	PersonalizationSchemaId__c	The schema of the experiment if the experiment uses a custom schema.	text
Personalization Schema Type	PersonalizationSchemaType__c	The schema of the experiment if the experiment uses a standard schema.	text
External Source Id	ExternalSourceId__c	The link to the external data source system from where the record originated, if applicable.	text
Profile Data Graph	ProfileDataGraphId__c	The profile data graph. This value is required only if the experiment has recommendation cohorts.	text
Primary Metric	PrimaryMetric__c	The primary metric to evaluate the success of the experiment.	text
Experiment Source	ExperimentSource__c	The builder or application in which the experiment is created. For example, Personalization App, CMS Content, Experience Builder, or Flow Builder.	text
