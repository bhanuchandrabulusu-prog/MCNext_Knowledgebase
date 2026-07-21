# Ai Agent Generative Ai Usage DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentgenerativeaiusagedmo-dmo.html

---

Captures granular AI usage analytics, including token consumption and LLM metadata for attributing consumption to specific agents and features.

Object API Name: std__AiAgentGenerativeAiUsageDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

AgentDeveloperName
AgentIdentifier
AgentTypeCode
AiAgentInteractionId
AiAgentSessionId
AiAgentToolIdentifier
AiAgentToolInvTargetCode
AiAgentToolName
cdp_sys_record_currency
DataSourceId
DataSourceObjectId
FeatureDescriptorName
GenAiGatewayFeatureName
GenAiGatewayModelName
Id
InfraTenantIdentifier
InternalOrganizationId
IsBillableIndicator
IsMeteredIndicator
MeteringSkipReasonCode
ModelClassType
ModelProviderModelName
ModelProviderName
PromptCompletionTokenCount
PromptInputTokenCount
PromptTemplateDeveloperName
PromptTemplateIdentifier
PromptTotalTokenCount
RequestIdentifier
TelemetryTraceIdentifier
TelemetryTraceSpanId
TierQualifierType
Timestamp
UnitTypeCode
UsageQuantity
UsageTypeCode
UserContext
UserId
Field API Name: std__AgentDeveloperName__c
Data Type: TEXT
Description: BotDefinition Developer Name (0Xx)
Field API Name: std__AgentIdentifier__c
Data Type: TEXT
Description: BotDefinition identifier (0Xx)
Field API Name: std__AgentTypeCode__c
Data Type: TEXT
Description: Type (e.g., Service Agent, Sales Coach)
Field API Name: std__AiAgentInteractionId__c
Data Type: TEXT
Description: Reference to a single interaction in a chat
Field API Name: std__AiAgentSessionId__c
Data Type: TEXT
Description: Links multiple interactions in one chat.
Field API Name: std__AiAgentToolIdentifier__c
Data Type: TEXT
Description: Reference on a base tool fully qualified name
Field API Name: std__AiAgentToolInvTargetCode__c
Data Type: TEXT
Description: Name of the tool invoked by the agent.
Field API Name: std__AiAgentToolName__c
Data Type: TEXT
Description: Name of the tool invoked by the agent.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__FeatureDescriptorName__c
Data Type: TEXT
Description: Salesforce Feature Name
Field API Name: std__GenAiGatewayFeatureName__c
Data Type: TEXT
Description: Generative AI Gateway Feature Name
Field API Name: std__GenAiGatewayModelName__c
Data Type: TEXT
Description: LLM Gateway Model Name
Field API Name: std__Id__c
Data Type: TEXT
Description: Event Identifier
Field API Name: std__InfraTenantIdentifier__c
Data Type: TEXT
Description: Infrastructure tenant identifier
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsBillableIndicator__c
Data Type: BOOLEAN
Description: Whether the event was intended to be billable by product feature
Field API Name: std__IsMeteredIndicator__c
Data Type: BOOLEAN
Description: Whether the event was metered and charged (final decision)
Field API Name: std__MeteringSkipReasonCode__c
Data Type: TEXT
Description: Reason the usage was not metered
Field API Name: std__ModelClassType__c
Data Type: TEXT
Description: LLM Model Usage Class
Field API Name: std__ModelProviderModelName__c
Data Type: TEXT
Description: LLM Model Name
Field API Name: std__ModelProviderName__c
Data Type: TEXT
Description: LLM Model Provider Name
Field API Name: std__PromptCompletionTokenCount__c
Data Type: DOUBLE
Description: Prompt Completion Tokens
Field API Name: std__PromptInputTokenCount__c
Data Type: DOUBLE
Description: Prompt Input Tokens
Field API Name: std__PromptTemplateDeveloperName__c
Data Type: TEXT
Description: Name of the prompt design used
Field API Name: std__PromptTemplateIdentifier__c
Data Type: TEXT
Description: ID of the prompt design used.
Field API Name: std__PromptTotalTokenCount__c
Data Type: DOUBLE
Description: Prompt Total Tokens
Field API Name: std__RequestIdentifier__c
Data Type: TEXT
Description: Unique ID for the specific Gateway request
Field API Name: std__TelemetryTraceIdentifier__c
Data Type: TEXT
Description: B3 Trace ID for end-to-end log correlation
Field API Name: std__TelemetryTraceSpanId__c
Data Type: TEXT
Description: Identifier used for distributed tracing. Associates this step within a broader tracing context
Field API Name: std__TierQualifierType__c
Data Type: TEXT
Description: Incoming event tier qualifier
Field API Name: std__Timestamp__c
Data Type: DATETIME
Description: Timestamp when event occurred
Field API Name: std__UnitTypeCode__c
Data Type: TEXT
Description: Incoming unit type
Field API Name: std__UsageQuantity__c
Data Type: DOUBLE
Description: Quantity of business usage units
Field API Name: std__UsageTypeCode__c
Data Type: TEXT
Description: Type of Digital Wallet Usage
Field API Name: std__UserContext__c
Data Type: TEXT
Description: User context used for metering evaluation
Field API Name: std__UserId__c
Data Type: TEXT
Description: Salesforce core user identifier
