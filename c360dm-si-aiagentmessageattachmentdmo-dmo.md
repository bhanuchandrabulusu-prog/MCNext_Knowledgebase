# Ai Agent Message Attachment DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentmessageattachmentdmo-dmo.html

---

Ai Agent Message Attachment DMO

Stores metadata and file paths for attachments linked to AI Agent Interaction Messages.

Object API Name: std__AiAgentMessageAttachmentDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

MessageId has a FOREIGNKEY relationship with the Ai Agent Interaction Message DMO Id field.
cdp_sys_record_currency
ContentDocumentVersionId
CreatedTimestamp
DataSourceId
DataSourceObjectId
ExternalSourceId
FilePathName
FileType
Id
InternalOrganizationId
MessageId
SourceName
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContentDocumentVersionId__c
Data Type: TEXT
Description: Content Document Version Id
Field API Name: std__CreatedTimestamp__c
Data Type: DATETIME
Description: Date and time when the attachment was recorded or created
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__FilePathName__c
Data Type: TEXT
Description: A file path pointing to where the attachment is stored in Data Cloud
Field API Name: std__FileType__c
Data Type: TEXT
Description: File type
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__MessageId__c
Data Type: TEXT
Description: AiAgentInteractionMessage Id
Field API Name: std__SourceName__c
Data Type: TEXT
Description: Thunderbird or Livekit
