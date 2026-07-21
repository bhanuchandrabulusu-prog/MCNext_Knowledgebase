# Account Plan Objective DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanobjectivedmo-dmo.html

---

Represents all strategic objectives or initiatives that a relationship team aims to pursue with a customer, facilitating focused planning and execution to enhance customer engagement and satisfaction

Object API Name: std__AccountPlanObjectiveDmo__dlm
Category: Unassigned
Availability: Available in 252 and later versions
Primary Key Field: Id

ObjectiveOwnerId has a FOREIGNKEY relationship with the User DMO Id field.
GoalDefinitionId has a FOREIGNKEY relationship with the Goal Definition DMO Id field.
AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
AccountPlanId
ActionPlanCompletedPct
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Description
DueDate
EndDate
GoalDefinitionId
Id
InternalOrganizationId
ObjectiveOwnerId
StartDate
Status
Field API Name: std__AccountPlanId__c
Data Type: TEXT
Description: The account plan associated with the objective.
Field API Name: std__ActionPlanCompletedPct__c
Data Type: PERCENT
Description: The completed percentage of action plans associated

with the account plan objective.

Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Description__c
Data Type: TEXT
Description: The description of the account plan objective.
Field API Name: std__DueDate__c
Data Type: DATEONLY
Description: The date when the objective is due to be completed.
Field API Name: std__EndDate__c
Data Type: DATEONLY
Description: The end date of the account plan objective.
Field API Name: std__GoalDefinitionId__c
Data Type: TEXT
Description: The reference to the imported objective
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ObjectiveOwnerId__c
Data Type: TEXT
Description: The owner user associated with the objective.
Field API Name: std__StartDate__c
Data Type: DATEONLY
Description: The start date of the account plan objective.
Field API Name: std__Status__c
Data Type: TEXT
Description: Specifies the status of the account plan objective.
