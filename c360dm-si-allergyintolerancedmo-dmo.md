# Allergy Intolerance DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-allergyintolerancedmo-dmo.html

---

Description: Categories of Allergy Intolerance. The categories are based on the HL7 Allergy Intolerance Category. Valid values include Food, Medication, and Biologic.
Field API Name: std__AllergyIntoleranceSeverity__c
Data Type: TEXT
Description: The criticality of a patient’s allergy intolerance. Values: low, high, unable-to-assess.
Field API Name: std__AllergyIntoleranceType__c
Data Type: TEXT
Description: The type of Allergy Intolerance. The type is based on the HL7 Allergy Intolerance Type. Valid values include 785009 for ‘Dextranase’ and 860009 for ‘Immunoglobulin, aggregated’.
Field API Name: std__AllergyIntoleranceVerificationStatus__c
Data Type: TEXT
Description: The criticality of a patient’s Allergy Intolerance. Valid values include low, high, and unable-to-assess.
Field API Name: std__AssertionSourceId__c
Data Type: TEXT
Description: The ID of the person or healthcare provider that asserted the patient’s condition.
Field API Name: std__AssertionSourceObject__c
Data Type: TEXT
Description: The name of the object that the Assertion Source record belongs to.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ClinicalEncounterId__c
Data Type: TEXT
Description: The ID of a Clinical Encounter. An encounter is an interaction between a patient and one or more healthcare providers for the purpose of providing healthcare services or assessing the health status of the patient.
Field API Name: std__CodeId__c
Data Type: TEXT
Description: The ID of the code that identifies the Allergy Intolerance based on the HL7 condition code. Valid values include 109006 for ‘Anxiety’ and and 253005 for ‘Sycosis’.
Field API Name: std__CodeSetBundleId__c
Data Type: TEXT
Description: The ID of the code that identifies the Allergy Intolerance based on the HL7 condition code. Valid values include 109006 for ‘Anxiety’ and 253005 for ‘Sycosis’.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AllergyIntolerance record. Maximum size is 36 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LastOccurrenceDateTime__c
Data Type: DATETIME
Description: Date and time when the allergy symptoms most recently occurred.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__OnsetEndDateTime__c
Data Type: DATETIME
Description: The estimated or actual date and time when the Allergy Intolerance was first observed.
Field API Name: std__OnsetStartDateTime__c
Data Type: DATETIME
Description: The date and time when the symptoms of the Allergy Inrolerance ended.
Field API Name: std__PatientId__c
Data Type: TEXT
Description: The ID of the person who received or registered to receive medical treatment for the Allergy Intolerance
Field API Name: std__RecordCreationDateTime__c
Data Type: DATETIME
Description: The original date and time when the Allergy Intolerance record was created. The value is provided only if the intolerance was recorded in another system.
Field API Name: std__RecorderId__c
Data Type: TEXT
Description: The ID of the patient, patient relative, or healthcare provider who recorded or observed the Allergy Intolerance.
Field API Name: std__RecordObject__c
Data Type: TEXT
Description: The object name of the recorder ID field record.
Field API Name: std__SourceSystem__c
Data Type: TEXT
Description: The name of the system the request was sourced from.
Field API Name: std__SourceSystemIdentifier__c
Data Type: TEXT
Description: The ID of the system the request was sourced from.
Field API Name: std__SourceSystemModified__c
Data Type: DATETIME
Description: The timestamp of the most recent update from the source system.
Field API Name: std__Status__c
Data Type: TEXT
Description: The clinical status of the Allergy Intolerance.
