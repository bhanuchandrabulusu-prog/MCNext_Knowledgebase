# Account Plan Product DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanproductdmo-dmo.html

---

Account Plan Product DMO

Represents all the products associated with an account plan or its objectives.

Object API Name: std__AccountPlanProductDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
AccountPlanObjectiveId has a FOREIGNKEY relationship with the Account Plan Objective DMO Id field.
ProductRecordId has a FOREIGNKEY relationship with the Product DMO Id field.
ProductRecordId has a FOREIGNKEY relationship with the Life Science Marketable Product DMO Id field.
AccountPlanId
AccountPlanObjectiveId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
ProductObject
ProductRecordId
Field API Name: std__AccountPlanId__c
Data Type: TEXT
Description: The account plan associated with a product.
Field API Name: std__AccountPlanObjectiveId__c
Data Type: TEXT
Description: The account plan objective associated with a product.
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
Field API Name: std__ProductObject__c
Data Type: TEXT
Description: Specifies the object name of the product record id.
Field API Name: std__ProductRecordId__c
Data Type: TEXT
Description: The specific product associated with an account plan.
