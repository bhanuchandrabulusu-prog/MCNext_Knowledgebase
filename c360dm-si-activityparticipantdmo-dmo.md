# Activity Participant DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-activityparticipantdmo-dmo.html

---

Description: The unique identifier for an instance of an Activity subtype to which the Activity Topic is related, for example, a Task, EmailMessage or VoiceCall. This is a relationship field. Maximum size is 15 characters.
Field API Name: std__ActivityObject__c
Data Type: TEXT
Description: The domain object name of the Activity. Possible values include Task, VoiceCall, and Messaging Session.
Field API Name: std__ActivityParticipantRole__c
Data Type: TEXT
Description: The way the person is participating in the Activity. Possible values include To, From, CC, Attendee, and Organizer.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContactPointId__c
Data Type: TEXT
Description: The identifier of an instance of a Contact Point subtype the Activity Participant is related to. The identifier can be a Contact Point Email, Contact Point Phone, or Contact Point OTT Service.
Field API Name: std__ContactPointObject__c
Data Type: TEXT
Description: The domain object name of the ContactPoint record.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the ActivityParticipant record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ParticipantId__c
Data Type: TEXT
Description: Required. The Salesforce ID of the user, lead, or contact record for this participant. The participant can be a person or a bot. This is a polymorphic relationship field. Maximum size is 15 characters.
Field API Name: std__ParticipantObject__c
Data Type: TEXT
Description: The name of the entity that the ParticipantID refers to. For example, if the ParticipantId exists on the Lead object, ParticipantObject=Lead.
