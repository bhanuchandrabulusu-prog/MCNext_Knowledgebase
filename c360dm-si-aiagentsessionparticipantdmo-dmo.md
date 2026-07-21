# Ai Agent Session Participant DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentsessionparticipantdmo-dmo.html

---

Description: Required. A unique, system-generated identifier for the AiAgentSessionParticipant record. Maximum size is 15 characters.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: The ID of an Individual record that represents the participant. This field is populated only if the type of the participant record’s Data Model Object (DMO) is Individual.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ParticipantAttributeText__c
Data Type: TEXT
Description: JSON key-value pairs for additional metadata or attributes of the participant specific to this session.
Field API Name: std__ParticipantId__c
Data Type: TEXT
Description: The ID of the record for the participant involved in the session.
Field API Name: std__ParticipantObject__c
Data Type: TEXT
Description: The name of the Data Model Object (DMO) the Participant record belongs to, for example, Individual.
Field API Name: std__ParticipantUserId__c
Data Type: TEXT
Description: Reference to the User record that represents the participant. Populated only if the participant record’s DMO type is User.
Field API Name: std__StartTimestamp__c
Data Type: DATETIME
Description: The timestamp when the participant joined the session.
