# Abn Experiment Log DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-abnexperimentlogdmo-dmo.html

---

Description: Required. A unique, system-generated identifier for this AbnExperimentLog record. Maximum size is 15 characters.
Field API Name: std__Individualid__c
Data Type: TEXT
Description: Required. A unique identifier for the individual. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__PersonalizationDecisionId__c
Data Type: TEXT
Description: The combination of a PersonalizationPoint and a Personalizer that’s associated with the user Engagement.
Field API Name: std__PersonalizationId__c
Data Type: TEXT
Description: A Personalization Id uniquely identifies a personalization request for a particular personalization point and individual that’s serviced by the personalization pipeline.
Field API Name: std__PersonalizationPointId__c
Data Type: TEXT
Description: Often a specific place in the UI the user engaged with. The Personalization Point collects a number of recommenders and personalizers, along with rules for when to execute them.
Field API Name: std__PoolAssignmentNumber__c
Data Type: DOUBLE
Description: An experiment has 10,000 pools split across multiple cohorts based on the traffic shaping rules. When a user calls experimentation, they are assigned to a cohort and a pool within that cohort.
Field API Name: std__RequestDatetime__c
Data Type: DATETIME
Description: When a request for an Experiment was sent to the service.
Field API Name: std__Requestid__c
Data Type: TEXT
Description: An identifier specific to a particular Experiment request.
Field API Name: std__TrackingKeyText__c
Data Type: TEXT
Description: A GUID provided by the consumer that’s used to track engagement events across Personalization Services Platform API calls.
Field API Name: std__TreatmentValueText__c
Data Type: TEXT
Description: Data that depends on the PersonalizationType and ExperimentSource. For a Personalizer, the field maps to the Personalizer Id; otherwise, it is a static string that’s used by the source application. For an Experiment created by the Flow Builder application, it maps to the Flow Path ID.
Field API Name: std__UnifiedIndividualId__c
Data Type: TEXT
Description: Represents a Unified Individual.
