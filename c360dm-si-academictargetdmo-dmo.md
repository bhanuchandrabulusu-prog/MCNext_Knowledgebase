# Academic Target DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-academictargetdmo-dmo.html

---

The Academic Target represents a target for admissions, enrollment, or registration for a specific academic term. The target is anchored to an Academic Term and may be scoped to a Learning program to support overall term level or program specific target tracking

Object API Name: std__AcademicTargetDmo__dlm
Category: Unassigned
Availability: Available in 262 and later versions
Primary Key Field: Id

AcademicTermId has a FOREIGNKEY relationship with the Academic Term DMO Id field.
LearningProgramId has a FOREIGNKEY relationship with the Learning Program DMO Id field.
AcademicTargetName
AcademicTermId
AtRiskDate
AtRiskNumber
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Id
InternalOrganizationId
LearningProgramId
TargetNumber
TargetScopeType
TargetType
Field API Name: std__AcademicTargetName__c
Data Type: TEXT
Description: The name of the academic target
Field API Name: std__AcademicTermId__c
Data Type: TEXT
Description: The academic term that’s associated with the academic target.
Field API Name: std__AtRiskDate__c
Data Type: DATEONLY
Description: The date on which the academic target is considered at risk if the at-risk threshold hasn’t been reached.
Field API Name: std__AtRiskNumber__c
Data Type: DOUBLE
Description: The number below which the academic target is considered at risk.
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
Field API Name: std__LearningProgramId__c
Data Type: TEXT
Description: The learning program that’s associated with the academic target.
Field API Name: std__TargetNumber__c
Data Type: DOUBLE
Description: The numeric goal for the academic target.
Field API Name: std__TargetScopeType__c
Data Type: TEXT
Description: The scope of the academic target. Possible values include Overall and Program.
Field API Name: std__TargetType__c
Data Type: TEXT
Description: The type of recruiting target for the academic target. Possible values include Prospects, Applicants, Admits, Accepts, Enrollees, and Registered.
