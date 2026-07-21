# Adverse Event DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-adverseeventdmo-dmo.html

---

Adverse Event DMO

Object API Name: std__AdverseEventDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

SubjectId has a FOREIGNKEY relationship with the Care Program Enrollee DMO Id field.
RelatedAdverseEventId has a FOREIGNKEY relationship with the Adverse Event DMO Id field.
EventCodeId has a FOREIGNKEY relationship with the Code Set DMO Id field.
SiteId has a FOREIGNKEY relationship with the Healthcare Facility DMO Id field.
EventCodeId has a FOREIGNKEY relationship with the Code Set Bundle DMO Id field.
ReportingContextId has a FOREIGNKEY relationship with the Research Study DMO Id field.
SubjectId has a FOREIGNKEY relationship with the Healthcare Provider DMO Id field.
SubjectId has a FOREIGNKEY relationship with the Account DMO Id field.
ClinicalEncounterId has a FOREIGNKEY relationship with the Clinical Encounter DMO Id field.
SiteId has a FOREIGNKEY relationship with the Care Program Site DMO Id field.
RecordedById has a FOREIGNKEY relationship with the Account DMO Id field.
Category
CauseEndDateTime
CauseStartDateTime
cdp_sys_record_currency
ClinicalEncounterId
DataSourceId
DataSourceObjectId
DetectedDateTime
EventCodeId
EventCodeObject
EventEndDateTime
EventStartDateTime
HasSubjectDiscontinuedStudy
Id
InternalOrganizationId
IsExpected
RecordedById
RecordedByObject
RecordedDateTime
RelatedAdverseEventId
ReportingContextId
ReportingContextObject
Severity
SiteId
SiteObject
Status
SubjectId
SubjectObject
Type
Field API Name: std__Category__c
Data Type: TEXT
Description: The category of the Adverse Event.
Field API Name: std__CauseEndDateTime__c
Data Type: DATETIME
Description: The end date of the cause for the Adverse Event.
Field API Name: std__CauseStartDateTime__c
Data Type: DATETIME
Description: The start date of the cause for the Adverse Event.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ClinicalEncounterId__c
Data Type: TEXT
Description: The ID of the clinical encounter associated with the Adverse Event.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DetectedDateTime__c
Data Type: DATETIME
Description: The date and time when the Adverse Event was detected.
Field API Name: std__EventCodeId__c
Data Type: TEXT
Description: The ID of the code for the Adverse Event.
Field API Name: std__EventCodeObject__c
Data Type: TEXT
Description: The object name of the Event Code field record for the Adverse Event.
Field API Name: std__EventEndDateTime__c
Data Type: DATETIME
Description: The end date and time of the Adverse Event.
Field API Name: std__EventStartDateTime__c
Data Type: DATETIME
Description: The start date and time of the Adverse Event.
Field API Name: std__HasSubjectDiscontinuedStudy__c
Data Type: BOOLEAN
Description: Whether the subject discontinued the research study due to the Adverse Event (true) or not (false).
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AdverseEvent record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsExpected__c
Data Type: BOOLEAN
Description: Whether the Adverse Event is expected for the research study (true) or not (false).
Field API Name: std__RecordedById__c
Data Type: TEXT
Description: The ID of the person who recorded the Adverse Event.
Field API Name: std__RecordedByObject__c
Data Type: TEXT
Description: The object name of the Recorded By field for the Adverse Event.
Field API Name: std__RecordedDateTime__c
Data Type: DATETIME
Description: The date and time when the Adverse Event was recorded.
Field API Name: std__RelatedAdverseEventId__c
Data Type: TEXT
Description: The ID of the Adverse Event entry that’s related to this record.
Field API Name: std__ReportingContextId__c
Data Type: TEXT
Description: The reporting context for the Adverse Event.
Field API Name: std__ReportingContextObject__c
Data Type: TEXT
Description: The object name of the Reporting Context field record for the Adverse Event.
Field API Name: std__Severity__c
Data Type: TEXT
Description: The severity of the Adverse Event.
Field API Name: std__SiteId__c
Data Type: TEXT
Description: The ID of the site where the Adverse Event occured.
Field API Name: std__SiteObject__c
Data Type: TEXT
Description: The object name of the Site field record for the Adverse Event.
Field API Name: std__Status__c
Data Type: TEXT
Description: The status of the Adverse Event.
Field API Name: std__SubjectId__c
Data Type: TEXT
Description: The ID of the subject for the Adverse Event.
Field API Name: std__SubjectObject__c
Data Type: TEXT
Description: The object name of the Subject field record for the Adverse Event.
Field API Name: std__Type__c
Data Type: TEXT
Description: The type of the Adverse Event.
