# Ai Participant Insight DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiparticipantinsightdmo-dmo.html

---

The AiParticipantInsight entity is a derived knowledge object designed to capture distilled, confidence-scored insights extracted from interactions. For e.g. between an agent (e.g. Ai Agent) and a participant (Such as a User or IndividualId). This object serves as a centralized repository for various learning outputs, categorized by Type—including Summary, Insight, Memory, or Preference. During a conversation, a versioned system prompt (eventually customizable by customers) triggers the LLM to generate a LearningPayload. This payload includes structured summarizations and specific Learning Domains (e.g., Commerce, HR, Finance, Travel). For high-performance retrieval and analysis, records are organized using the Grouping Attribute, which supports filtering by SessionId, ConversationId, OwnerId, or an array of identifiers. This structure ensures a persistent, actionable record of user behavior and intent, enabling real-time personalization and long-term memory for AI agents.

Object API Name: std__AiParticipantInsightDmo__dlm
Category: Unassigned
Availability: Available in 260 and later versions
Primary Key Field: Id

IndividualId has a FOREIGNKEY relationship with the Individual DMO Id field.
UserId has a FOREIGNKEY relationship with the User DMO Id field.
ConversationId has a FOREIGNKEY relationship with the Conversation DMO Id field.
AgentIdentifier
cdp_sys_record_currency
ConfidenceLvlTxt
ConversationId
CreatedDate
DataSourceId
DataSourceObjectId
GroupIdentifier
Id
IndividualId
InsightPayloadTxt
InsightScopeType
InsightType
InternalOrganizationId
ParticipantId
ParticipantObject
ReferenceTxt
UserId
ValidToTimestamp
Field API Name: std__AgentIdentifier__c
Data Type: TEXT
Description: Identifier of the agent that is part of the conversation from which this insight was extracted.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ConfidenceLvlTxt__c
Data Type: TEXT
Description: LLM-assigned confidence score that represents the reliability or quality of this insight.
Field API Name: std__ConversationId__c
Data Type: TEXT
Description: If the insight is generated from a single conversation, the Identifier of the conversation from which this insight was derived.
Field API Name: std__CreatedDate__c
Data Type: DATETIME
Description: Timestamp when the system created this insight record.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__GroupIdentifier__c
Data Type: TEXT
Description: Identifier of the group that includes multiple related and incremental insight records.
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key.
Field API Name: std__IndividualId__c
Data Type: TEXT
Description: Identifier of the individual (person entity) to whom this insight applies, if applicable. Used when the insight is associated with a real-world individual rather than an authenticated user.
Field API Name: std__InsightPayloadTxt__c
Data Type: TEXT
Description: Insight content derived from the conversation(s).
Field API Name: std__InsightScopeType__c
Data Type: TEXT
Description: Aggregation scope for insights. Examples: grouping by sessionId or owner id or conversation Id.
Field API Name: std__InsightType__c
Data Type: TEXT
Description: Insight classification. Examples: preference, summary, insight, memory.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ParticipantId__c
Data Type: TEXT
Description: Polymorphic reference to participant type. Examples: User, Individual.
Field API Name: std__ParticipantObject__c
Data Type: TEXT
Description: Name of the object to which ParticipantId refers.
Field API Name: std__ReferenceTxt__c
Data Type: TEXT
Description: Structured references to source artifacts from which this insight was derived. Examples: conversation entry Id, Session Id. Supports auditability and explainability.
Field API Name: std__UserId__c
Data Type: TEXT
Description: Identifier odescriptionf the user account associated with this insight, if applicable. Used when insights are scoped to a platform user.
Field API Name: std__ValidToTimestamp__c
Data Type: DATETIME
Description: Timestamp after which this insight is considered stale or invalid.
