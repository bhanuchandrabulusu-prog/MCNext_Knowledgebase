# Account Plan Related Object Analysis DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-accountplanrelatedobjectanalysisdmo-dmo.html

---

Represents the strategic analyses done on objects related to the account plan. This object helps to identify various internal and external factors that could potentially affect the plan, its objectives, or any related objects.

Object API Name: std__AccountPlanRelatedObjectAnalysisDmo__dlm
Category: Unassigned
Availability: Available in 254 and later versions
Primary Key Field: Id

AccountPlanId has a FOREIGNKEY relationship with the Account Plan DMO Id field.
RelatedObjectRecordId has a FOREIGNKEY relationship with the Life Science Marketable Product DMO Id field.
RelatedObjectRecordId has a FOREIGNKEY relationship with the Product DMO Id field.
AccountPlanId
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
EconomicalAnalysisInfoText
EnvironmentalAnalysisInfoText
Id
InternalOrganizationId
LegalAnalysisInfoText
OpportunitiesAnalysisInfoText
PoliticalAnalysisInfoText
RelatedObject
RelatedObjectRecordId
SocialAnalysisInfoText
StrengthAnalysisInfoText
TechnologicalAnalysisInfoText
ThreatsAnalysisInfoText
WeaknessAnalysisInfoText
Field API Name: std__AccountPlanId__c
Data Type: TEXT
Description: The account plan for which object analysis is done.
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

Field API Name: std__EnvironmentalAnalysisInfoText__c
Data Type: TEXT
Description: The detailed assessment of environmental factors that can

impact the account, such as sustainability considerations, climate change-related risks, and regulatory compliance with environmental standards.

Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LegalAnalysisInfoText__c
Data Type: TEXT
Description: The detailed assessment of legal information relevant to the account,

including regulations, compliance requirements, and potential legal risks or opportunities.

Field API Name: std__OpportunitiesAnalysisInfoText__c
Data Type: TEXT
Description: The in-depth analysis of identified opportunities within the account

based on factors like their potential impact, feasibility, and alignment with the overall strategic objectives.

Field API Name: std__PoliticalAnalysisInfoText__c
Data Type: TEXT
Description: The detailed assessment of political factors that can influence the account,

such as government policies, regulatory changes, and political stability in the relevant regions.

Field API Name: std__RelatedObject__c
Data Type: TEXT
Description: The specific product or service associated with an account plan.
Field API Name: std__RelatedObjectRecordId__c
Data Type: TEXT
Description: The specific product or service associated with an account plan.
Field API Name: std__SocialAnalysisInfoText__c
Data Type: TEXT
Description: The examination of social factors that can impact the account, including

demographic trends, cultural considerations, and social responsibility initiatives.

Field API Name: std__StrengthAnalysisInfoText__c
Data Type: TEXT
Description: The assessment of the internal strengths of the account,

such as key capabilities, competitive advantages, and resources that can be leveraged to achieve the plan’s objectives.

Field API Name: std__TechnologicalAnalysisInfoText__c
Data Type: TEXT
Description: The evaluation of technological factors that can affect the account,

including emerging technologies, industry-specific innovations, and the customer’s technological capabilities and infrastructure.

Field API Name: std__ThreatsAnalysisInfoText__c
Data Type: TEXT
Description: The identification and assessment of potential threats to the account,

such as competitive pressures, market disruptions, and regulatory changes.

Field API Name: std__WeaknessAnalysisInfoText__c
Data Type: TEXT
Description: The detailed assessment of internal weaknesses of the account,

such as areas for improvement, resource constraints, and potential vulnerabilities that could hinder the achievement of the plan’s objectives.
