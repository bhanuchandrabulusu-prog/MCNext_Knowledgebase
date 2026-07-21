# Account Plan Stakeholder Product DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanstakeholderproductdmo-dmo.html

---

This entity represents the relationship between an Account Plan Stakeholder and the specific Products they can influence within that plan.

Object API Name: std__AccountPlanStakeholderProductDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

ProductRecordId has a FOREIGNKEY relationship with the Product DMO Id field.
ProductRecordId has a FOREIGNKEY relationship with the Life Science Marketable Product DMO Id field.
AccountPlanStakeholderId has a FOREIGNKEY relationship with the Account Plan Stakeholder DMO Id field.
AccountPlanStakeholderId
cdp_sys_record_currency
CommentText
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
ProductRecordId
ProductRecordObject
Field API Name: std__AccountPlanStakeholderId__c
Data Type: TEXT
Description: The account plan stakeholder associated with the account plan.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__CommentText__c
Data Type: TEXT
Description: The additional description about the relationship between the account plan, account plan stakeholder, and the associated products.
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
Field API Name: std__ProductRecordId__c
Data Type: TEXT
Description: The product associated with the account plan stakeholder.
Field API Name: std__ProductRecordObject__c
Data Type: TEXT
Description: Specifies the object name of the product record id.
