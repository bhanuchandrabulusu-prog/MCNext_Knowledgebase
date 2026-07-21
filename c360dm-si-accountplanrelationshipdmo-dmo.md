# Account Plan Relationship DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanrelationshipdmo-dmo.html

---

Account Plan Relationship DMO

Represents the relationship between multiple account plans for key account management.

Object API Name: std__AccountPlanRelationshipDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
AccountPlanId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
RelatedAccountPlanId
Field API Name: std__AccountPlanId__c
Data Type: TEXT
Description: The primary account plan associated with a particular account plan.
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
Field API Name: std__RelatedAccountPlanId__c
Data Type: TEXT
Description: The related account plan associated with an account plan.
