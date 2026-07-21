# Account Plan Ptcp Stakeholder DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanptcpstakeholderdmo-dmo.html

---

Stores information about the account plan participant who collaborates with the account plan stakeholder for performing account plan tasks.

Object API Name: std__AccountPlanPtcpStakeholderDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AccountPlanStakeholderId has a FOREIGNKEY relationship with the Account Plan Participant DMO Id field.
AccountPlanParticipantId has a FOREIGNKEY relationship with the Account Plan Participant DMO Id field.
AccountPlanParticipantId
AccountPlanStakeholderId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
ParticipantName
StakeholderName
Field API Name: std__AccountPlanParticipantId__c
Data Type: TEXT
Description: The acount plan stakeholder who collaborates with the account plan participant and influences the decisions of the account plan.
Field API Name: std__AccountPlanStakeholderId__c
Data Type: TEXT
Description: The account plan participant who collaborates with the account plan stakeholder for performing account plan tasks.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ParticipantName__c
Data Type: TEXT
Description: The identifier of the record in the source system.
Field API Name: std__StakeholderName__c
Data Type: TEXT
Description: The name of the system from which data is loaded into this object.
