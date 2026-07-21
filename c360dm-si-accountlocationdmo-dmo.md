# Account Location DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountlocationdmo-dmo.html

---

Represents a link between an account and a location in Field Service. You can associate multiple accounts with one location. For example, a shopping center location may have multiple customer accounts.

Object API Name: std__AccountLocationDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

LocationId has a FOREIGNKEY relationship with the Location DMO Id field.
AccountId has a FOREIGNKEY relationship with the Account DMO Id field.
AccountId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
Description
EffectiveEndDateTime
EffectiveStartDateTime
Id
InternalOrganizationId
LocationId
LocationName
LocationSupplyType
Field API Name: std__AccountId__c
Data Type: TEXT
Description: The account with whom the location is associated.
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
Description: Description of the Account Location Record.
Field API Name: std__EffectiveEndDateTime__c
Data Type: DATETIME
Description: Date and time the account location is inactive.
Field API Name: std__EffectiveStartDateTime__c
Data Type: DATETIME
Description: Date and time the account location is active.
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LocationId__c
Data Type: TEXT
Description: The location associated with the account.
Field API Name: std__LocationName__c
Data Type: TEXT
Description: Name of the Account Location
Field API Name: std__LocationSupplyType__c
Data Type: TEXT
Description: The supply type of location, valid values are: Bill To, Ship To
