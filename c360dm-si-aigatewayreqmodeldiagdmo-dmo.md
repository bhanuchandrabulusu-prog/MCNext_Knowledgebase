# Ai Gateway Req Model Diag DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aigatewayreqmodeldiagdmo-dmo.html

---

Ai Gateway Req Model Diag DMO

Represents the Diagnostic Data for each AI Model used in a single AI Gateway Request.

Object API Name: std__AiGatewayReqModelDiagDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

AiApplicationFeatureName
AiGatewayRequestId
AiModelName
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
EndpointName
ErrorText
ExternalRecordId
ExternalSourceId
Id
InternalOrganizationId
RegionName
ReqLatencyMsNumber
ReqMetadataText
ReqStatus
Field API Name: std__AiApplicationFeatureName__c
Data Type: TEXT
Description: Represents the AI application’s specific Feature for which this gateway generation call was made.
Field API Name: std__AiGatewayRequestId__c
Data Type: TEXT
Description: Reference to the AI Gateway Request.
Field API Name: std__AiModelName__c
Data Type: TEXT
Description: Name of the AI Model Used.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__EndpointName__c
Data Type: TEXT
Description: Endpoint Name used for the Request.
Field API Name: std__ErrorText__c
Data Type: TEXT
Description: Error captured as part of the Request.
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
Field API Name: std__RegionName__c
Data Type: TEXT
Description: Region used for the Request.
Field API Name: std__ReqLatencyMsNumber__c
Data Type: DOUBLE
Description: Request Latency in Millisecond.
Field API Name: std__ReqMetadataText__c
Data Type: TEXT
Description: Additional Metadata around the request.
Field API Name: std__ReqStatus__c
Data Type: TEXT
Description: Status of the Request to the AI Model.
