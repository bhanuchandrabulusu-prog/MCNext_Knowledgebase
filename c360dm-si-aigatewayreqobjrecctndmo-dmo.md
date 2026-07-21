# Ai Gateway Req Obj Rec Ctn DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aigatewayreqobjrecctndmo-dmo.html

---

Ai Gateway Req Obj Rec Ctn DMO

Represents citations that reference the Gateway Request Object Record.

Object API Name: std__AiGatewayReqObjRecCtnDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

AiGatewayReqObjRecId has a FOREIGNKEY relationship with the Ai Gateway Req Obj Rec DMO Id field.
AiApplicationFeatureName
AiGatewayReqObjRecId
cdp_sys_record_currency
CitationText
DataSourceId
DataSourceObjectId
ExternalRecordId
ExternalSourceId
Id
InternalOrganizationId
Field API Name: std__AiApplicationFeatureName__c
Data Type: TEXT
Description: Represents the AI application’s specific Feature for which this gateway generation call was made.
Field API Name: std__AiGatewayReqObjRecId__c
Data Type: TEXT
Description: Reference to the AI Gateway Request Object Record.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__CitationText__c
Data Type: TEXT
Description: Text that details the Citation for the record.
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
