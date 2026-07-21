# Account Relationship DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountrelationshipdmo-dmo.html

---

Description: Reason for associating two accounts via Account Relationship. Possible values include Implementation Partner and Sales Partner.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__EffectiveEndDate__c
Data Type: DATEONLY
Description: The date until which the Account Relationship is active.
Field API Name: std__EffectiveStartDate__c
Data Type: DATEONLY
Description: The date from which the Account Relationship is active.
Field API Name: std__HierarchyType__c
Data Type: TEXT
Description: The hierarchy between related accounts. For example, an account is related to another account as a parent, peer, or child.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for this AccountRelationship record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsActive__c
Data Type: TEXT
Description: Whether the relationship is active (true) or not (false). The default value is true.
Field API Name: std__IsPrimaryRelationship__c
Data Type: TEXT
Description: Whether the relationship is a primary relationship in a given role. Account can have multiple Bill To accounts, but only one is the Primary Bill To account.
Field API Name: std__IsSelfRelationship__c
Data Type: TEXT
Description: Whether the relationship is a self-relationship. For example, if the account is Bill To to itself, this checkbox is selected.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__PartyRelationshipTypeId__c
Data Type: TEXT
Description: Reference to the party relationship type that indicates the role played by each Account in this relation.
Field API Name: std__RelatedAccountId__c
Data Type: TEXT
Description: The second of two accounts associated via Account Relationship.
Field API Name: std__RelatedInverseRecordId__c
Data Type: TEXT
Description: The record that specifies the inverse relationship between the accounts.
