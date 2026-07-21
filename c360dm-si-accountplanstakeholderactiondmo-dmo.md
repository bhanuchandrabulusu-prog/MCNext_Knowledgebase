# Account Plan Stakeholder Action DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanstakeholderactiondmo-dmo.html

---

Represents all Actions being done as part of an Account Plan (e.g., Action Plans, Tasks) linked to a specific Stakeholder.

Object API Name: std__AccountPlanStakeholderActionDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

ActionRecordId has a FOREIGNKEY relationship with the Action Plan DMO Id field.
ActionRecordId has a FOREIGNKEY relationship with the Assessment Task DMO Id field.
AccountPlanStakeholderId has a FOREIGNKEY relationship with the Account Plan Stakeholder DMO Id field.
ActionRecordId has a FOREIGNKEY relationship with the Action Plan Item DMO Id field.
AccountPlanStakeholderId
ActionRecordId
ActionRecordObject
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
Field API Name: std__AccountPlanStakeholderId__c
Data Type: TEXT
Description: The account plan stakeholder for whom the action is performed.
Field API Name: std__ActionRecordId__c
Data Type: TEXT
Description: The action plan or action plan item referencing an action to be performed for the account plan stakeholder.
Field API Name: std__ActionRecordObject__c
Data Type: TEXT
Description: Specifies the object name of the action record id.
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
