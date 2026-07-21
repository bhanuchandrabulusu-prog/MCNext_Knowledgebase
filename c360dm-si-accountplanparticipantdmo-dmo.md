# Account Plan Participant DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanparticipantdmo-dmo.html

---

This entity represents the team members participating in the account plan. These members are responsible for executing tasks and tactics to achieve the plan’s defined objectives.

Object API Name: std__AccountPlanParticipantDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

ParticipantRecordId has a FOREIGNKEY relationship with the User Group DMO Id field.
ParticipantRecordId has a FOREIGNKEY relationship with the User DMO Id field.
AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
AccountPlanId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
ParticipantObject
ParticipantRecordId
ParticipantRoleText
Field API Name: std__AccountPlanId__c
Data Type: TEXT
Description: The account plan that the participant is working on.
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
Field API Name: std__ParticipantObject__c
Data Type: TEXT
Description: The specific object name of the participant record id.
Field API Name: std__ParticipantRecordId__c
Data Type: TEXT
Description: The specific team member participating in the account plan.
Field API Name: std__ParticipantRoleText__c
Data Type: TEXT
Description: The plan participant’s role in executing the account plan,

such as sales representative or collaborator.
