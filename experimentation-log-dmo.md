# Experimentation Log DMO | Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-log-dmo.html

---

Personalization Id	PersonalizationId__c	The identifier for the personalized response sent to a specific personalization point.	text
Request id	Requestid__c	The identifier for the experimentation request sent to the experimentation pipeline.	text
Request DateTime	RequestDateTime__c	The date and time the experimentation request was made.	dateTime
Individual	Individualid__c	The identifier for the individual DMO.	text
Unified Individual	UnifiedIndividualId__c	The identifier for the unified individual.	text
Experiment	AbnExperimentId__c	The identifier for the experiment.	text
Experiment Cohort	AbnExperimentCohortId__c	The identifier for the cohort assigned to the experiment.	text
Treatment Value	TreatmentValueText__c	The dynamic value populated based on the personalization type and experiment source.	text
Pool Assignment	PoolAssignmentNumber__c	The pool a user is assigned to. A user is assigned to a cohort and a pool within the cohort when the user makes an experimentation request.	number
Tracking Key	TrackingKeyText__c	The Global Unique Identifier (GUID) for tracking engagement events across Personalization API calls.	text
