# Ai Agent Session DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentsessiondmo-dmo.html

---

Description: Required. A unique, system-generated identifier for the AiAgentSession record. Maximum size is 15 characters.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: The ID of the Individual record for the session owner participant. This field is populated only if the type of the Session Owner Object is Individual.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__OwnerUserId__c
Data Type: TEXT
Description: Reference to the User record that represents the participant. Populated only if the participant record’s DMO type is User.
Field API Name: std__PreviousSessionId__c
Data Type: TEXT
Description: The ID of the previous AI agent session in a multi-agent scenario.
Field API Name: std__RelatedMessagingSessionId__c
Data Type: TEXT
Description: An ID that links the AI agent session to the messaging session from which it was initiated.
Field API Name: std__RelatedVoiceCallId__c
Data Type: TEXT
Description: An ID that links the session to the voice call from which it was initiated.
Field API Name: std__SessionOwnerId__c
Data Type: TEXT
Description: The ID of the record of the participant who initiated the session.
Field API Name: std__SessionOwnerObject__c
Data Type: TEXT
Description: The name of the Data Model Object (DMO) the Session Owner record belongs to, for example, Individual.
Field API Name: std__StartTimestamp__c
Data Type: DATETIME
Description: The timestamp when the session was initiated.
Field API Name: std__VariableText__c
Data Type: TEXT
Description: JSON key-value pairs for contextual session data used by agents during interactions.
