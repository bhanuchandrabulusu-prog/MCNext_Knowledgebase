# Abn Experiment DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-abnexperimentdmo-dmo.html

---

Description: An enumerated type that specifies the builder or app this experiment was created in. Valid values are Created, Started, Stopped, and Archived.
Field API Name: std__ExperimentState__c
Data Type: TEXT
Description: The user-configurable state of the experiment. Valid values are Created, Running, Completed, and Archived.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for this AbnExperiment record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__PersonalizationSchemaId__c
Data Type: TEXT
Description: For a custom schema, the schema of the Experiment. In the Platform object, the ENUMORID is split into two mutually exclusive fields: id and enum.
Field API Name: std__PersonalizationSchemaType__c
Data Type: TEXT
Description: For a standard schema, the schema of the Experiment. Possible values include ExperienceVariation or Flow.
Field API Name: std__ProfileDataGraphId__c
Data Type: TEXT
Description: Optional. A data graph is required only if the Experiement has recommendation cohorts.
Field API Name: std__StartedDateTime__c
Data Type: DATETIME
Description: The date/time the Experiment was started. No value is provided if the Experiment was never started.
Field API Name: std__StoppedDateTime__c
Data Type: DATETIME
Description: The date/time the Experiment was stopped. No value is provided if the Experiment was never stopped.
