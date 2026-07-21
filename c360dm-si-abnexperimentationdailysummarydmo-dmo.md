# Abn Experimentation Daily Summary DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-abnexperimentationdailysummarydmo-dmo.html

---

Abn Experimentation Daily Summary DMO

Object API Name: std__AbnExperimentationDailySummaryDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AbnExperimentCohortId has a FOREIGNKEY relationship with the Abn Experiment Cohort DMO Id field.
AbnExperimentId has a FOREIGNKEY relationship with the Abn Experiment DMO Id field.
AbnExperimentCohortId
AbnExperimentId
AssignedParticipantsCount
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
ExperimentSummaryMetricType
ForDate
Id
InternalOrganizationId
IsPrimary
LastUpdatedDateTime
MetricId
MetricName
MetricValueNumber
SignalDenominatorValueNumber
SignalNumeratorValueNumber
Field API Name: std__AbnExperimentCohortId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__AbnExperimentId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__AssignedParticipantsCount__c
Data Type: DOUBLE
Description: The number of assigned participants for this record.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExperimentSummaryMetricType__c
Data Type: TEXT
Description: Alphanumeric string representing the experiment summary metric type.
Field API Name: std__ForDate__c
Data Type: DATEONLY
Description: Calendar date representing the for date in the YYYY-MM-DD format.
Field API Name: std__Id__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsPrimary__c
Data Type: BOOLEAN
Description: Indicates whether this record is primary (true) or not (false).
Field API Name: std__LastUpdatedDateTime__c
Data Type: DATETIME
Description: The date and time of the last updated date time.
Field API Name: std__MetricId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__MetricName__c
Data Type: TEXT
Description: Alphanumeric string representing the metric name.
Field API Name: std__MetricValueNumber__c
Data Type: DOUBLE
Description: Numeric value representing the metric value number. Do not include currency symbols or commas.
Field API Name: std__SignalDenominatorValueNumber__c
Data Type: DOUBLE
Description: Numeric value representing the signal denominator value number. Do not include currency symbols or commas.
Field API Name: std__SignalNumeratorValueNumber__c
Data Type: DOUBLE
Description: Numeric value representing the signal numerator value number. Do not include currency symbols or commas.
