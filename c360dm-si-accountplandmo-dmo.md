# Account Plan DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplandmo-dmo.html

---

Represents a detailed strategic outline of the vital customer information used to effectively manage and expand customer relationships.

Object API Name: std__AccountPlanDmo__dlm
Category: Unassigned
Availability: Available in 252 and later versions
Primary Key Field: Id

AccountId has a FOREIGNKEY relationship with the Account DMO Id field.
AccountChallengesText
AccountCmptvWeaknessesText
AccountCompetitiveStrengthsText
AccountCompetitorsText
AccountId
AccountIndustryTrendsText
AccountPrfmIndicatorsText
AccountStrategicPrioritiesText
AccountVisionText
ActionPlanCompletedPct
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
EconomicalAnalysisInfoText
EndDate
EnvironmentalAnalysisInfoText
Id
InternalOrganizationId
LegalAnalysisInfoText
Notes
PoliticalAnalysisInfoText
RelationshipOpportunitiesText
RelationshipStrengthsText
RelationshipThreatsText
RelationshipWeaknessesText
SocialAnalysisInfoText
StartDate
Status
TechnologicalAnalysisInfoText
Field API Name: std__AccountChallengesText__c
Data Type: TEXT
Description: The key obstacles to the growth of the account.
Field API Name: std__AccountCmptvWeaknessesText__c
Data Type: TEXT
Description: The shortcomings that hinder the account’s ability to outperform competitors in the market.
Field API Name: std__AccountCompetitiveStrengthsText__c
Data Type: TEXT
Description: The abilities of the account to outperform their competitors in the market.
Field API Name: std__AccountCompetitorsText__c
Data Type: TEXT
Description: The businesses or companies that offer similar products or services and compete for the same target market as the account.
Field API Name: std__AccountId__c
Data Type: TEXT
Description: Parent Account to whom account plan being targetted.
Field API Name: std__AccountIndustryTrendsText__c
Data Type: TEXT
Description: The shifts in the pattern of the industry that are specific to the account.
Field API Name: std__AccountPrfmIndicatorsText__c
Data Type: TEXT
Description: The key performance indicators used by the account to measure the success and effectiveness of a product or service.
Field API Name: std__AccountStrategicPrioritiesText__c
Data Type: TEXT
Description: The key priorities of the account.
Field API Name: std__AccountVisionText__c
Data Type: TEXT
Description: The long-term value statement of the account.
Field API Name: std__ActionPlanCompletedPct__c
Data Type: PERCENT
Description: Specifies the completed percentage of the account plan.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__EconomicalAnalysisInfoText__c
Data Type: TEXT
Description: Evaluation of the economic factors that could affect the account,

including market trends, economic indicators, and financial health of the customer and their industry.

Field API Name: std__EndDate__c
Data Type: DATEONLY
Description: End date of the account plan.
Field API Name: std__EnvironmentalAnalysisInfoText__c
Data Type: TEXT
Description: Assessment of the environmental factors that could impact the account,

such as sustainability considerations, climate change-related risks, and regulatory compliance with environmental standards.

Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LegalAnalysisInfoText__c
Data Type: TEXT
Description: Detailed analysis of the legal landscape relevant to the account,

including regulations, compliance requirements, and potential legal risks or opportunities.

Field API Name: std__Notes__c
Data Type: TEXT
Description: The notes or observations for the account plan.
Field API Name: std__PoliticalAnalysisInfoText__c
Data Type: TEXT
Description: The detailed assessment of political factors that can influence the account,

such as government policies, regulatory changes, and political stability in the relevant regions.

Field API Name: std__RelationshipOpportunitiesText__c
Data Type: TEXT
Description: The list of sales or potential deal opportunities in the relationship with the account.
Field API Name: std__RelationshipStrengthsText__c
Data Type: TEXT
Description: The strengths in the relationship with the account.
Field API Name: std__RelationshipThreatsText__c
Data Type: TEXT
Description: The possible concerns in the relationship with the account.
Field API Name: std__RelationshipWeaknessesText__c
Data Type: TEXT
Description: The shortcomings in the relationship with the account.
Field API Name: std__SocialAnalysisInfoText__c
Data Type: TEXT
Description: The examination of social factors that can impact the account, including

demographic trends, cultural considerations, and social responsibility initiatives.

Field API Name: std__StartDate__c
Data Type: DATEONLY
Description: Start date of the account plan.
Field API Name: std__Status__c
Data Type: TEXT
Description: Specifies the status of the account plan. Possible values are: Active, Inactive, Not Started
Field API Name: std__TechnologicalAnalysisInfoText__c
Data Type: TEXT
Description: The evaluation of technological factors that can affect the account,

including emerging technologies, industry-specific innovations, and the customer’s technological capabilities and infrastructure.
