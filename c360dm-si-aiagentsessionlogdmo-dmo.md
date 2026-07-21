# Ai Agent Session Log DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-aiagentsessionlogdmo-dmo.html

---

Captures log events emitted during AI agent sessions, including informational, warning, error, and fatal entries with causal chaining for multi-agent error tracing.

Object API Name: std__AiAgentSessionLogDmo__dlm
Category: Unassigned
Availability: Available in 264 and later versions
Primary Key Field: Id

AiAgentSessionId has a FOREIGNKEY relationship with the Ai Agent Session DMO Id field.
AiAgentInteractionId has a FOREIGNKEY relationship with the Ai Agent Interaction DMO Id field.
AiAgentInteractionStepId has a FOREIGNKEY relationship with the Ai Agent Interaction Step DMO Id field.
TelemetryTraceSpanId has a FOREIGNKEY relationship with the Telemetry Trace Span DMO Id field.
CauseLogId has a FOREIGNKEY relationship with the Ai Agent Session Log DMO Id field.
RootCauseLogId has a FOREIGNKEY relationship with the Ai Agent Session Log DMO Id field.
AiAgentInteractionId
AiAgentInteractionStepId
AiAgentSessionId
Category
CauseLogId
cdp_sys_record_currency
Code
DataSourceId
DataSourceObjectId
Description
DetailedDescription
ExternalSourceId
Id
InternalOrganizationId
LogDateTime
LogLevelType
RootCauseLogId
TelemetryTrace
TelemetryTraceSpanId
Field API Name: std__AiAgentInteractionId__c
Data Type: TEXT
Description: Foreign key to AiAgentInteraction. Nullable.
Field API Name: std__AiAgentInteractionStepId__c
Data Type: TEXT
Description: Foreign key to AiAgentInteractionStep. Nullable.
Field API Name: std__AiAgentSessionId__c
Data Type: TEXT
Description: Foreign key to AiAgentSession. Required.
Field API Name: std__Category__c
Data Type: TEXT
Description: Contextual domain of the log entry. Examples: Tool, LLM, Retrieval, Guardrail, Auth, HTTP, Delegation, Platform, Lifecycle, Performance.
Field API Name: std__CauseLogId__c
Data Type: TEXT
Description: Self-FK. Immediate wrapped/underlying cause. Populated only when LogLevel is ERROR or FATAL.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__Code__c
Data Type: TEXT
Description: Structured code for the event. For errors: user-facing error code. For non-errors: event type identifier.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Description__c
Data Type: TEXT
Description: Short, human-readable summary of the issue.
Field API Name: std__DetailedDescription__c
Data Type: TEXT
Description: Structured JSON payload / diagnostics. Schema varies by Category and LogLevelType.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: Organization identifier used for dataspace filtering.
Field API Name: std__Id__c
Data Type: TEXT
Description: Primary Key.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LogDateTime__c
Data Type: DATETIME
Description: Timestamp of the log event.
Field API Name: std__LogLevelType__c
Data Type: TEXT
Description: Log level. Values: DEBUG | INFO | WARNING | ERROR | FATAL.
Field API Name: std__RootCauseLogId__c
Data Type: TEXT
Description: Self-FK. Deepest known cause (denormalized). Populated only when LogLevel is ERROR or FATAL.
Field API Name: std__TelemetryTrace__c
Data Type: TEXT
Description: Shared identifier used for implicit joins on TraceId among DMOs (AiAgentInteraction, TelemetryTraceSpan, AiAgentSessionLog). Nullable.
Field API Name: std__TelemetryTraceSpanId__c
Data Type: TEXT
Description: Foreign key to TelemetryTraceSpan. Nullable.
