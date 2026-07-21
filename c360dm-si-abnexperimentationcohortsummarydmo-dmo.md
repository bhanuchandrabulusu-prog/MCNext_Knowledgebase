# Abn Experimentation Cohort Summary DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-abnexperimentationcohortsummarydmo-dmo.html

---

An output DMO for collecting experimentation cohort summary data. The purpose is to collect experimentation data per cohort

Object API Name: std__AbnExperimentationCohortSummaryDmo__dlm
Category: cdp-udd
Availability: Available in 258 and later versions
Primary Key Field: Id

AbnExperimentId has a FOREIGNKEY relationship with the Abn Experiment DMO Id field.
AbnExperimentCohortId has a FOREIGNKEY relationship with the Abn Experiment Cohort DMO Id field.
AbnExperimentCohortId
AbnExperimentId
AssignedParticipantsCount
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
ExperimentAnalysisStatusTxt
Id
InternalOrganizationId
LastUpdatedDateTime
ProbabilityToBeatAllPercent
ProbabilityToBeatControlPercent
ScoreType
Field API Name: std__AbnExperimentCohortId__c
Data Type: TEXT
Description: The Experiment Cohort Id
Field API Name: std__AbnExperimentId__c
Data Type: TEXT
Description: The Experiment Id
Field API Name: std__AssignedParticipantsCount__c
Data Type: DOUBLE
Description: Number of assigned participants
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExperimentAnalysisStatusTxt__c
Data Type: TEXT
Description: The status of the experimentation data analysis (how trustworthy the experimentation data is)
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LastUpdatedDateTime__c
Data Type: DATETIME
Description: The Last Updated Date Time
Field API Name: std__ProbabilityToBeatAllPercent__c
Data Type: DOUBLE
Description: The Probability To Beat All (Percent)
Field API Name: std__ProbabilityToBeatControlPercent__c
Data Type: DOUBLE
Description: The Probability To Beat Control (Percent)
Field API Name: std__ScoreType__c
Data Type: TEXT
Description: The Score Type: OEC or SINGLE_PRIMARY
