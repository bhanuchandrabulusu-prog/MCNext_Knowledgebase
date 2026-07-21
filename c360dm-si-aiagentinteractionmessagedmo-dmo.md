# Ai Agent Interaction Message DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentinteractionmessagedmo-dmo.html

---

Description: A description of the format or type of the message content. Possible values include text/plain, application/json, and audio/wav.
Field API Name: std__AiAgentSessionId__c
Data Type: TEXT
Description: The ID of the session this message belongs to.
Field API Name: std__AiAgentSessionParticipantId__c
Data Type: TEXT
Description: The ID of the participant who sent the message.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContentText__c
Data Type: TEXT
Description: Direct textual content if the message is text-based.
Field API Name: std__ConversationId__c
Data Type: TEXT
Description: Optional foreign-key relationship with the Conversation Entity.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AiAgentInteractionMessage record. Maximum size is 15 characters.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: The ID of an Individual record that represents the session owner participant. This field is populated only if the SessionOwnerObject is Individual.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__MessageEndTimestamp__c
Data Type: DATETIME
Description: The exact time the message was ended.
Field API Name: std__MessageSentTimestamp__c
Data Type: DATETIME
Description: The exact time the message was sent.
Field API Name: std__MessageStartTimestamp__c
Data Type: DATETIME
Description: The exact time the message was started.
Field API Name: std__Modality__c
Data Type: TEXT
Description: The message is in voice or text mode.
Field API Name: std__ParentMessageId__c
Data Type: TEXT
Description: The ID of another message if this message is a reply or continuation.
Field API Name: std__ParticipantUserId__c
Data Type: TEXT
Description: Reference to the User record that represents the participant. Populated only if the participant record’s DMO type is User.
Field API Name: std__SessionOwnerId__c
Data Type: TEXT
Description: The ID of the record of the participant who initiated the session.
Field API Name: std__SessionOwnerObject__c
Data Type: TEXT
Description: The name of the Data Model Object (DMO) the Session Owner record belongs to, for example, Individual.
