# Ai Gateway Req Obj Rec DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aigatewayreqobjrecdmo-dmo.html

---

Ai Gateway Req Obj Rec DMO

Represents record-level references from a Gateway Request or Feedback.

Object API Name: std__AiGatewayReqObjRecDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

AiApplicationFeatureName
AiFeedbackId
AiGatewayRequestId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
ExternalRecordId
ExternalSourceId
Id
InternalOrganizationId
RecordId
RecordLabelName
RecordLinkText
RecordTypeName
ReqMetadataText
Field API Name: std__AiApplicationFeatureName__c
Data Type: TEXT
Description: Represents the AI application’s specific Feature for which this gateway generation call was made.
Field API Name: std__AiFeedbackId__c
Data Type: TEXT
Description: Reference to the AI Feedback Record.
Field API Name: std__AiGatewayRequestId__c
Data Type: TEXT
Description: Reference to the AI Gateway Request.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalRecordId__c
Data Type: TEXT
Description: The corresponding record Id from an external data source system
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: Corresponding record Id from external data source system
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__RecordId__c
Data Type: TEXT
Description: Record Identifier for the Related Object.
Field API Name: std__RecordLabelName__c
Data Type: TEXT
Description: Name of the Record (e.g. Case Lable, Knowledge Article Title/Label)
Field API Name: std__RecordLinkText__c
Data Type: TEXT
Description: Links to Salesforce Objects or URLs to web pages.
Field API Name: std__RecordTypeName__c
Data Type: TEXT
Description: Type of the Object (e.g. Case, Knowledge Article etc.)
Field API Name: std__ReqMetadataText__c
Data Type: TEXT
Description: Additional Metadata around the record linking.
