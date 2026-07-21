# Account DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountdmo-dmo.html

---

How the party want to interact with your enterprise e.g. have multiple billing or service accounts, can be hierarchical in nature and normally one particular business unit within the company owns the account.

Object API Name: std__AccountDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point DMO Id field.
PartyId has a FOREIGNKEY relationship with the Individual DMO Id field.
FaxPhoneId has a FOREIGNKEY relationship with the Contact Point Phone DMO Id field.
SalesPhoneId has a FOREIGNKEY relationship with the Contact Point Phone DMO Id field.
PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point Address DMO Id field.
OrderDeliveryMethodId has a FOREIGNKEY relationship with the Order Delivery Method DMO Id field.
PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point Social DMO Id field.
ShippingAddressId has a FOREIGNKEY relationship with the Contact Point Address DMO Id field.
AutoPaymentMethodId has a FOREIGNKEY relationship with the Payment Method DMO Id field.
ParentAccountId has a FOREIGNKEY relationship with the Account DMO Id field.
BillContactAddressId has a FOREIGNKEY relationship with the Contact Point Address DMO Id field.
PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point Email DMO Id field.
ShippingContactId has a FOREIGNKEY relationship with the Account Contact DMO Id field.
PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point Phone DMO Id field.
PartyId has a FOREIGNKEY relationship with the Party DMO Id field.
PrimarySalesContactPointId has a FOREIGNKEY relationship with the Contact Point App DMO Id field.
ShippingPhoneid has a FOREIGNKEY relationship with the Contact Point Phone DMO Id field.
AutoPaymentMethodId has a FOREIGNKEY relationship with the Voucher DMO Id field.
PrimarySalesRepId has a FOREIGNKEY relationship with the User DMO Id field.
OwnerId has a FOREIGNKEY relationship with the User DMO Id field.
OperatingHoursId has a FOREIGNKEY relationship with the Operating Hours DMO Id field.
IndividualId has a FOREIGNKEY relationship with the Individual DMO Id field.
ShippingEmailId has a FOREIGNKEY relationship with the Contact Point Email DMO Id field.
AccountBusinessType
AccountId
AccountNumber
AccountOwnershipType
AccountPriority
AccountRatingType
AccountSegmentType
AccountServiceEntitlements
AccountSource
AccountType
AccountTypeId
AccountWebsiteUrl
AlternateName
AnnualRevenueAmount
AssignTerritoryFlag
AutoPayEnabledFlag
AutoPaymentAmount
AutoPaymentAmountCurrency
AutoPaymentMethodId
BalanceAmount
BalanceAmountCurrency
BalanceAmountLimit
BalanceAmountLimitCurrency
BalanceUnitOfMeasureCurrency
BalanceUnitOfMeasureCurrencyId
BalanceUnitOfMeasureId
BillContactAddressId
BillDeliveryMethod
BillDeliveryMethodId
BillFrequency
BusinessUnitId
cdp_sys_record_currency
ContactPointAddressId
ContactPointAppId
ContactPointEmailId
ContactPointLocationId
ContactPointPhoneId
ContactPointSocialId
CreatedDate
CreditLimitAmount
CreditRatingType
DataSourceId
DataSourceObjectId
DefaultFreightTerms
DefaultFreightTermsId
DefaultPriceBookId
Description
EffectiveDate
EmployeeCount
EndDate
ExternalRecordId
ExternalSourceId
FaxPhoneId
FixedFundingOverdrawPercent
GeneralLedgerAccountId
GroupIncome
GroupSize
HoldStatusReason
HoldStatusReasonId
Id
IndividualId
InternalOrganizationId
IsActive
IsCreditBlocked
IsCustomer
IsInternal
IsPartner
IsSeller
IsSupplier
LastActivityDate
LastModifiedById
LastModifiedDate
LastVisitDate
NameInterfaceField
NextInteractionDate
NextReviewDate
NinetyDayBalanceAmount
NinetyDayBalanceAmountCurrency
Number
OperatingHours
OperatingHoursId
OrderDeliveryMethod
OrderDeliveryMethodId
OrganizationId
OwnerId
ParentAccountId
PartyId
PartyObject
PartyRoleId
PartyWebAddressId
PaymentTerm
PaymentTermId
PrimaryIndustry
PrimarySalesContactPointId
PrimarySalesRepId
ProfileImageUrl
RateBasedFundingOverdrawPercent
RecordType
ReviewFrequencyText
SalesPhoneId
ShippingAddressId
ShippingContactId
ShippingEmailId
ShippingPhoneid
SixtyDayBalanceAmount
SixtyDayBalanceAmountCurrency
SlaexpirationDate
Slatype
SlatypeId
SourceSystemIdentifier
SourceSystemModifiedDateTime
TaxPaymentJurisdictionCode
ThirtyDayBalanceAmount
ThirtyDayBalanceAmountCurrency
TradeClassificationType
UseAsBillingAccount
UseAsSalesAccount
UseAsServiceAccount
UseAsShippingAccount
WebsiteAddr
Field API Name: std__AccountBusinessType__c
Data Type: TEXT
Description: The primary business purpose or kinds of transactions the Account is used for. Possible values include Charge Account, Rebate Account, and Rental Account.
Field API Name: std__AccountId__c
Data Type: TEXT
Description: The unique identifier for the related Account record.
Field API Name: std__AccountNumber__c
Data Type: TEXT
Description: Unique identifier number assigned to the account.
Field API Name: std__AccountOwnershipType__c
Data Type: TEXT
Description: The Ownership type of the Account. Possible values include Private, Public, and Subsidiary.
Field API Name: std__AccountPriority__c
Data Type: TEXT
Description: A unique identifier for each Account Priority Record. The priority level helps classify accounts based on their importance. Possible values include A-Priority, B-Priority, and C-Priority.
Field API Name: std__AccountRatingType__c
Data Type: TEXT
Description: The account’s prospect rating. Possible values include Hot, Warm, and Cold.
Field API Name: std__AccountSegmentType__c
Data Type: TEXT
Description: A unique identifier for each Account Segment Type record, which is the type of grouping applied to accounts (such as stores) based on business logic.
Field API Name: std__AccountServiceEntitlements__c
Data Type: TEXT
Description: Service entitlements associated with the account, such as support levels or contracted services.
Field API Name: std__AccountSource__c
Data Type: TEXT
Description: The source of the account record. For example, Advertisement or Trade Show. The source is selected from a picklist of available values, which are set by an administrator. Each picklist value can have up to 40 characters.
Field API Name: std__AccountType__c
Data Type: TEXT
Description: The type of account, for example, Customer, Competitor, or Partner. Maximum size is 36 characters.
Field API Name: std__AccountTypeId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__AccountWebsiteUrl__c
Data Type: TEXT
Description: The URL for account website url.
Field API Name: std__AlternateName__c
Data Type: TEXT
Description: The alternate name of the account.
Field API Name: std__AnnualRevenueAmount__c
Data Type: DOUBLE
Description: The estimated annual revenue of the account.
Field API Name: std__AssignTerritoryFlag__c
Data Type: TEXT
Description: Whether the account reached a state where it must be assigned a territory.
Field API Name: std__AutoPayEnabledFlag__c
Data Type: TEXT
Description: Whether Auto Pay is enabled for the customer.
Field API Name: std__AutoPaymentAmount__c
Data Type: DOUBLE
Description: The amount to be automatically paid next time.
Field API Name: std__AutoPaymentAmountCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the auto payment amount currency.
Field API Name: std__AutoPaymentMethodId__c
Data Type: TEXT
Description: The payment instrument to be used. Possible values include paypal, credit card, and bank acc.
Field API Name: std__BalanceAmount__c
Data Type: DOUBLE
Description: The balance amount. Possible values include 100 points, 3 miles, and 6 visits.
Field API Name: std__BalanceAmountCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the balance amount currency.
Field API Name: std__BalanceAmountLimit__c
Data Type: DOUBLE
Description: The maximum balance allowed before usage action is taken. Sometimes referred to as the credit limit.
Field API Name: std__BalanceAmountLimitCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the balance amount limit currency.
Field API Name: std__BalanceUnitOfMeasureCurrency__c
Data Type: TEXT
Description: Currency used for the balance unit of measure associated with the account.
Field API Name: std__BalanceUnitOfMeasureCurrencyId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__BalanceUnitOfMeasureId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__BillContactAddressId__c
Data Type: TEXT
Description: The contact point billing address, if applicable.
Field API Name: std__BillDeliveryMethod__c
Data Type: TEXT
Description: Method used to deliver billing statements to the account, such as email or postal mail.
Field API Name: std__BillDeliveryMethodId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__BillFrequency__c
Data Type: TEXT
Description: How often to bill the contact, for example, monthly.
Field API Name: std__BusinessUnitId__c
Data Type: TEXT
Description: The logical Internal Organization to which the Account record belongs.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ContactPointAddressId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ContactPointAppId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ContactPointEmailId__c
Data Type: TEXT
Description: The primary email address of the account.
Field API Name: std__ContactPointLocationId__c
Data Type: TEXT
Description: The primary location of the Account.
Field API Name: std__ContactPointPhoneId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ContactPointSocialId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__CreatedDate__c
Data Type: DATETIME
Description: The date and time the record was originally created.
Field API Name: std__CreditLimitAmount__c
Data Type: DOUBLE
Description: The overall credit limit of the account.
Field API Name: std__CreditRatingType__c
Data Type: TEXT
Description: The credit rating of the account. Possible values are A, B, and C.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DefaultFreightTerms__c
Data Type: TEXT
Description: Default freight or shipping terms associated with orders for the account.
Field API Name: std__DefaultFreightTermsId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DefaultPriceBookId__c
Data Type: TEXT
Description: The standard price book for the customer.
Field API Name: std__Description__c
Data Type: TEXT
Description: Text description of the account. Limited to 32, 000 KB.
Field API Name: std__EffectiveDate__c
Data Type: DATETIME
Description: The date and time of the effective date.
Field API Name: std__EmployeeCount__c
Data Type: DOUBLE
Description: Total number of employees working at the company represented by this account. Label is Employees. Maximum size is 8 digits.
Field API Name: std__EndDate__c
Data Type: DATETIME
Description: Date and time when the record or activity ended.
Field API Name: std__ExternalRecordId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: The system where the ExternalRecordId was assigned.
Field API Name: std__FaxPhoneId__c
Data Type: TEXT
Description: The fax number of the account.
Field API Name: std__FixedFundingOverdrawPercent__c
Data Type: DOUBLE
Description: The overdraw allowance percentage for fixed funding.
Field API Name: std__GeneralLedgerAccountId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__GroupIncome__c
Data Type: DOUBLE
Description: The total income for accounts of type Household or Group Party.
Field API Name: std__GroupSize__c
Data Type: DOUBLE
Description: The size of the group for accounts of type Household or Group Party.
Field API Name: std__HoldStatusReason__c
Data Type: TEXT
Description: The reason for the hold status.
Field API Name: std__HoldStatusReasonId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the Account record. Maximum size is 36 characters.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: A person. The PartyId field is used in Data Cloud to refer to an Individual. Its label is Individual Party due to existing use of that field for the individual.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsActive__c
Data Type: TEXT
Description: Whether the patient’s record is in active use. The field is used primarily in Healthcare scenarios.
Field API Name: std__IsCreditBlocked__c
Data Type: TEXT
Description: Whether the status of the account’s credit role is blocked (true) or unblocked (false).
Field API Name: std__IsCustomer__c
Data Type: TEXT
Description: Whether the Organization or Individual to which the Account belongs is a customer of your organization (true) or not (false).
Field API Name: std__IsInternal__c
Data Type: TEXT
Description: Alphanumeric string representing the is internal.
Field API Name: std__IsPartner__c
Data Type: TEXT
Description: Alphanumeric string representing the is partner.
Field API Name: std__IsSeller__c
Data Type: TEXT
Description: Alphanumeric string representing the is seller.
Field API Name: std__IsSupplier__c
Data Type: TEXT
Description: Alphanumeric string representing the is supplier.
Field API Name: std__LastActivityDate__c
Data Type: DATETIME
Description: The date and time of the last activity date.
Field API Name: std__LastModifiedById__c
Data Type: TEXT
Description: The user who most recently changed the record.
Field API Name: std__LastModifiedDate__c
Data Type: DATETIME
Description: The date and time when a user last modified the record.
Field API Name: std__LastVisitDate__c
Data Type: DATEONLY
Description: The date when the last customer physical visit was made by a sales representative.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__NextInteractionDate__c
Data Type: DATETIME
Description: The date and time of the next interaction date.
Field API Name: std__NextReviewDate__c
Data Type: DATETIME
Description: The date and time of the next review date.
Field API Name: std__NinetyDayBalanceAmount__c
Data Type: DOUBLE
Description: The Account Balance from 90 days ago.
Field API Name: std__NinetyDayBalanceAmountCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the ninety day balance amount currency.
Field API Name: std__Number__c
Data Type: TEXT
Description: Numeric identifier associated with the account record.
Field API Name: std__OperatingHours__c
Data Type: TEXT
Description: Hours of operation for the account.
Field API Name: std__OperatingHoursId__c
Data Type: TEXT
Description: The operating hours associated with the account. Available only if Field Service is enabled.
Field API Name: std__OrderDeliveryMethod__c
Data Type: TEXT
Description: Method used to deliver the order, such as shipping, pickup, or digital delivery.
Field API Name: std__OrderDeliveryMethodId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__OrganizationId__c
Data Type: TEXT
Description: A company with which business is or is intended to be done, for example, Northern Trail Outfitters USA. The value can also be at a lower level within a company, for example, Northern Trail Outfitters: Calfornia USA.
Field API Name: std__OwnerId__c
Data Type: TEXT
Description: The ID of the user who currently owns this account. Default value is the user logged in to the API to perform the create.
Field API Name: std__ParentAccountId__c
Data Type: TEXT
Description: The ID of the parent object, if any. This is a One to One (1:1) relationship field. Accounts is the relationship name and Account is the referenced object. Maximum size is 36 characters.
Field API Name: std__PartyId__c
Data Type: TEXT
Description: A person with whom the account is used for business relationships.
Field API Name: std__PartyObject__c
Data Type: TEXT
Description: The type of entity referenced by Party Id. Possible values are Party, Individual, and Organization.
Field API Name: std__PartyRoleId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__PartyWebAddressId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__PaymentTerm__c
Data Type: TEXT
Description: Alphanumeric string representing the payment term.
Field API Name: std__PaymentTermId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__PrimaryIndustry__c
Data Type: TEXT
Description: The primary line of business or production the Account’s organization is engaged in. Maximum size is 40 characters.
Field API Name: std__PrimarySalesContactPointId__c
Data Type: TEXT
Description: The best way to communicate with the customer for Sales purpose.
Field API Name: std__PrimarySalesRepId__c
Data Type: TEXT
Description: The primary sales rep who currently owns the account. The field encourages security.
Field API Name: std__ProfileImageUrl__c
Data Type: TEXT
Description: The Account’s social network profile image.
Field API Name: std__RateBasedFundingOverdrawPercent__c
Data Type: DOUBLE
Description: The percentage for the Account’s Rate-Based Funding overdraw allowance.
Field API Name: std__RecordType__c
Data Type: TEXT
Description: Type classification of the account record, used to differentiate account categories or business processes.
Field API Name: std__ReviewFrequencyText__c
Data Type: TEXT
Description: The text content for the review frequency of the account. Maximum size is 255 characters.
Field API Name: std__SalesPhoneId__c
Data Type: TEXT
Description: The phone number of the account.
Field API Name: std__ShippingAddressId__c
Data Type: TEXT
Description: The shipping address of the account, if applicable.
Field API Name: std__ShippingContactId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ShippingEmailId__c
Data Type: TEXT
Description: The email address to use for shipping inquiries.
Field API Name: std__ShippingPhoneid__c
Data Type: TEXT
Description: The phone number to use for shipping inquiries.
Field API Name: std__SixtyDayBalanceAmount__c
Data Type: DOUBLE
Description: The Account Balance from 60 days ago.
Field API Name: std__SixtyDayBalanceAmountCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the sixty day balance amount currency.
Field API Name: std__SlaexpirationDate__c
Data Type: DATETIME
Description: The date and time of the slaexpiration date.
Field API Name: std__Slatype__c
Data Type: TEXT
Description: Service level agreement (SLA) type associated with the account, indicating the level of service contracted.
Field API Name: std__SlatypeId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__SourceSystemIdentifier__c
Data Type: TEXT
Description: The ID of the system the request was sourced from.
Field API Name: std__SourceSystemModifiedDateTime__c
Data Type: DATETIME
Description: The timestamp of the most recent update from the source system.
Field API Name: std__TaxPaymentJurisdictionCode__c
Data Type: TEXT
Description: The jurisdiction code of the location at which taxes are to be paid.
Field API Name: std__ThirtyDayBalanceAmount__c
Data Type: DOUBLE
Description: The Account Balance from 30 days ago.
Field API Name: std__ThirtyDayBalanceAmountCurrency__c
Data Type: TEXT
Description: Alphanumeric string representing the thirty day balance amount currency.
Field API Name: std__TradeClassificationType__c
Data Type: TEXT
Description: The classification of the trade the account business deals in. Possible values include Supermarket, Drugstore, Restaurant, Hypermarket, Department, and Grocery.
Field API Name: std__UseAsBillingAccount__c
Data Type: TEXT
Description: Whether the account is used for billing purposes.
Field API Name: std__UseAsSalesAccount__c
Data Type: TEXT
Description: Whether the account is used for sales purposes.
Field API Name: std__UseAsServiceAccount__c
Data Type: TEXT
Description: Whether the account is used for service purposes.
Field API Name: std__UseAsShippingAccount__c
Data Type: TEXT
Description: Whether the account is used for shipping purposes.
Field API Name: std__WebsiteAddr__c
Data Type: TEXT
Description: The website of the account. Maximum of 255 characters.
