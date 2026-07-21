# Academic Interest DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-academicinterestdmo-dmo.html

---

Academic Interest DMO

Represents an academic interest of a person.

Object API Name: std__AcademicInterestDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

AcademicTermId has a FOREIGNKEY relationship with the Academic Term DMO Id field.
AccountId has a FOREIGNKEY relationship with the Account DMO Id field.
ContactId has a FOREIGNKEY relationship with the Individual DMO Id field.
ContactRequestId has a FOREIGNKEY relationship with the Contact Request DMO Id field.
EducationalInfoRequestId has a FOREIGNKEY relationship with the Educational Info Request DMO Id field.
IndividualApplicationId has a FOREIGNKEY relationship with the Application DMO Id field.
LeadId has a FOREIGNKEY relationship with the Individual DMO Id field.
LearningProgramId has a FOREIGNKEY relationship with the Learning Program DMO Id field.
OpportunityId has a FOREIGNKEY relationship with the Opportunity DMO Id field.
AcademicInterestName
AcademicTermId
AccountId
cdp_sys_record_currency
ContactId
ContactRequestId
DataSourceId
DataSourceObjectId
EducationalInfoRequestId
Id
IndividualApplicationId
InternalOrganizationId
LeadId
LearningProgramId
OpportunityId
ReceivedDate
Source
Status
SubscriptionText
Field API Name: std__AcademicInterestName__c
Data Type: TEXT
Description: An auto-generated string or number assigned to the academic interest.
Field API Name: std__AcademicTermId__c
Data Type: TEXT
Description: The Academic Term associated with the Academic Interest.
Field API Name: std__AccountId__c
Data Type: TEXT
Description: The Account associated with the Academic Interest.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContactId__c
Data Type: TEXT
Description: The Contact associated with the Academic Interest.
Field API Name: std__ContactRequestId__c
Data Type: TEXT
Description: The Contact Request associated with the Academic Interest.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__EducationalInfoRequestId__c
Data Type: TEXT
Description: The Educational Info Request associated with the Academic Interest.
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__IndividualApplicationId__c
Data Type: TEXT
Description: The Individual Application associated with the Academic Interest.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LeadId__c
Data Type: TEXT
Description: The lead for the person who expressed the Academic Interest.
Field API Name: std__LearningProgramId__c
Data Type: TEXT
Description: The Learning Program associated with the Academic Interest.
Field API Name: std__OpportunityId__c
Data Type: TEXT
Description: The Opportunity associated with the Academic Interest.
Field API Name: std__ReceivedDate__c
Data Type: DATEONLY
Description: The date when the interest from the person was received.
Field API Name: std__Source__c
Data Type: TEXT
Description: Specifies the Academic Interest Source
Field API Name: std__Status__c
Data Type: TEXT
Description: Specifies the Academic Interest Status
Field API Name: std__SubscriptionText__c
Data Type: TEXT
Description: The subscription that the person is requesting.
