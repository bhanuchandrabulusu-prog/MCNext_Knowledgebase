# Ai Agent Interaction Step DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentinteractionstepdmo-dmo.html

---

Description: Required. A unique, system-generated identifier for the AiAgentInteractionStep record. Maximum size is 15 characters.
Field API Name: std__InputValueText__c
Data Type: TEXT
Description: The input data provided to the step.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__OutputValueText__c
Data Type: TEXT
Description: The output data of the step’s execution.
Field API Name: std__ParticipantIndividualId__c
Data Type: TEXT
Description: Reference to the Individual record that represents the participant. Populated only if the participant record’s DMO type is Individual.
Field API Name: std__ParticipantUserId__c
Data Type: TEXT
Description: Reference to the User record that represents the participant. Populated only if the participant record’s DMO type is User.
Field API Name: std__PostStepVariableText__c
Data Type: TEXT
Description: The state of relavant variables after step execution finishes.
Field API Name: std__PreStepVariableText__c
Data Type: TEXT
Description: The state of relevant variables before step execution begins.
Field API Name: std__PrevStepId__c
Data Type: TEXT
Description: The ID of the previous step. The ID enables sequencing or chaining of steps.
Field API Name: std__SessionId__c
Data Type: TEXT
Description: Reference to the specific AiAgentSession in which this step is involved.
Field API Name: std__StartTimestamp__c
Data Type: DATETIME
Description: The timestamp when execution of the the step started.
Field API Name: std__SubType__c
Data Type: TEXT
Description: The subtype of the step that provides additional classification within the step type.
Field API Name: std__TelemetryTraceSpanId__c
Data Type: TEXT
Description: The ID used for distributed tracing to place the step within a broader tracing context.
