# Ai Agent Tag DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagenttagdmo-dmo.html

---

Ai Agent Tag DMO

Object API Name: std__AiAgentTagDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AiAgentTagDefinitionId has a FOREIGNKEY relationship with the Ai Agent Tag Definition DMO Id field.
AiAgentTagDefinitionId
cdp_sys_record_currency
CreatedDate
DataSourceId
DataSourceObjectId
Description
ExternalSourceId
Id
InternalOrganizationId
IsActive
IsFallback
OrderNumber
Value
Field API Name: std__AiAgentTagDefinitionId__c
Data Type: TEXT
Description: The reference ID of an associated AI Agent Tag Definition.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__CreatedDate__c
Data Type: DATETIME
Description: The date when the record for the AI Agent Tag was created.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Description__c
Data Type: TEXT
Description: Additional information about the AI Agent Tag.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AiAgentTag record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsActive__c
Data Type: BOOLEAN
Description: Whether the tag is currently active (true) or not (false).
Field API Name: std__IsFallback__c
Data Type: BOOLEAN
Description: Indicates whether this record is fallback (true) or not (false).
Field API Name: std__OrderNumber__c
Data Type: DOUBLE
Description: Numeric value representing the order number. Do not include currency symbols or commas.
Field API Name: std__Value__c
Data Type: TEXT
Description: The value assigned to the AI Agent Tag.
