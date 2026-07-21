# Ai Agent Interaction DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentinteractiondmo-dmo.html

---

Description: Required. A unique, system-generated identifier for the AiAgentInteraction record. Maximum size is 15 characters.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: The ID of an Individual record that represents the session owner participant. This field is populated only if the SessionOwnerObject is Individual.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__PrevInteractionId__c
Data Type: TEXT
Description: The ID of the previous interaction. The ID enables sequencing or chaining of interactions.
Field API Name: std__SessionOwnerId__c
Data Type: TEXT
Description: The ID of the record for the participant who initiated (owned) the session.
Field API Name: std__SessionOwnerObject__c
Data Type: TEXT
Description: The name of the Data Model Object (DMO) the Session Owner record belongs to, for example, Individual.
Field API Name: std__StartTimestamp__c
Data Type: DATETIME
Description: The timestamp when the interaction began.
Field API Name: std__TelemetryTraceId__c
Data Type: TEXT
Description: An ID used for distributed tracing. The ID allows tracking of interactions across system components.
Field API Name: std__TelemetryTraceSpanId__c
Data Type: TEXT
Description: The span ID for tracing this specific interaction within a larger distributed tracing context.
Field API Name: std__TopicApiName__c
Data Type: TEXT
Description: The API name of the topic that was classified for the interaction.
