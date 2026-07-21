# Account Contact DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountcontactdmo-dmo.html

---

Description: Required. ID of the account that’s the parent of this contact. We recommend that you update up to 50 contacts simultaneously when changing the accounts on contacts enabled for a Customer Portal or partner portal. We also recommend that you make this update after business hours. This is a relationship field. Maximum size is 36 characters.
Field API Name: std__AssistantName__c
Data Type: TEXT
Description: The name of the assistant for the account contact. Maximum size is 255 characters.
Field API Name: std__AssistantPhone__c
Data Type: TEXT
Description: The assistant’s phone number. Label is Asst. Phone. Maximum size is 255 characters.
Field API Name: std__BusinessPhoneId__c
Data Type: TEXT
Description: The telephone number for the contact.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContactEmailId__c
Data Type: TEXT
Description: The email address for the contact.
Field API Name: std__ContactNote__c
Data Type: TEXT
Description: A description of the contact.
Field API Name: std__CreatedDate__c
Data Type: DATETIME
Description: The date and time the record was originally created.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DeceasedDateTime__c
Data Type: DATETIME
Description: The date and time of the deceased date time.
Field API Name: std__DepartmentName__c
Data Type: TEXT
Description: The name of the department for the account contact. Maximum size is 255 characters.
Field API Name: std__EffectiveEndDate__c
Data Type: DATEONLY
Description: The end date of the Account Contact relation.
Field API Name: std__EffectiveStartDate__c
Data Type: DATEONLY
Description: The start date of the Account Contact relation.
Field API Name: std__ExternalRecordId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__FaxPhoneId__c
Data Type: TEXT
Description: The fax number for the contact.
Field API Name: std__FirstName__c
Data Type: TEXT
Description: Alphanumeric string representing the first name.
Field API Name: std__Gender__c
Data Type: TEXT
Description: Alphanumeric string representing the gender.
Field API Name: std__HomePhoneId__c
Data Type: TEXT
Description: The contact’s home phone number. Label is Home Phone. This is a One to One (1:1) relationship field. AccountContacts is the relationship name and Contact Point Phone is the referenced object. Maximum size is 36 characters.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for this AccountContact record. Maximum size is 36 characters.
Field API Name: std__IndirectRelationAccountContactId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: The person that’s the contact for the account.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsActive__c
Data Type: BOOLEAN
Description: Whether the relation is active.
Field API Name: std__IsDirect__c
Data Type: BOOLEAN
Description: Whether the individual is directly related to the account.
Field API Name: std__IsIncludedInGroup__c
Data Type: BOOLEAN
Description: Whether the member is included in the group (true) or not (false).
Field API Name: std__IsPrimaryGroup__c
Data Type: BOOLEAN
Description: Whether the group is a primary group for the member (yes) or not (no).
Field API Name: std__IsPrimaryMember__c
Data Type: BOOLEAN
Description: Whether the member is a primary contact of a group (true) or not (false).
Field API Name: std__LastActivityDate__c
Data Type: DATETIME
Description: The date and time of the last activity date.
Field API Name: std__LastModifiedDate__c
Data Type: DATETIME
Description: The date and time of the last modification to this record.
Field API Name: std__LastName__c
Data Type: TEXT
Description: Alphanumeric string representing the last name.
Field API Name: std__MailingAddressId__c
Data Type: TEXT
Description: The mailing address for the member.
Field API Name: std__MaritalStatus__c
Data Type: TEXT
Description: Alphanumeric string representing the marital status.
Field API Name: std__MiddleName__c
Data Type: TEXT
Description: Alphanumeric string representing the middle name.
Field API Name: std__MobilePhoneId__c
Data Type: TEXT
Description: Contact’s mobile phone number. Label is Mobile Phone. This is a One to One (1:1) relationship field. AccountContacts is the relationship name and Contact Point Phone is the referenced object. Maximum size is 36 characters.
Field API Name: std__OtherContactAddressId__c
Data Type: TEXT
Description: Reference to Other address.
Field API Name: std__OwnerId__c
Data Type: TEXT
Description: The unique identifier of the owner of the account associated with this contact. This is a person internal to the company who has an interest in or responsibility for the AccountContact; usually the person who created it. This is a relationship field. Maximum size is 15 characters.
Field API Name: std__PersonName__c
Data Type: TEXT
Description: Full name of the person associated with the lead.
Field API Name: std__ReportsToAccountContactId__c
Data Type: TEXT
Description: The unique identifier of the contact that this contact reports to. This is a One to One (1:1) relationship field. AccountContacts is the relationship name and Account Contact is the referenced object. Maximum size is 36 characters.
Field API Name: std__SequenceInMultipleBirthNumber__c
Data Type: DOUBLE
Description: Numeric value representing the sequence in multiple birth number. Do not include currency symbols or commas.
Field API Name: std__Title__c
Data Type: TEXT
Description: Title of the account contact, such as CEO or Vice President. Maximum size is 255 characters.
