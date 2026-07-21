# Agent Service Presence DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-agentservicepresencedmo-dmo.html

---

Description: The duration that the user is at full capacity. This field is updated when the agent’s capacity changes, such as when the agent is assigned, declines, or closes a work item.
Field API Name: std__AverageCapacity__c
Data Type: DOUBLE
Description: The user’s average capacity. This field is updated when the agent’s capacity changes, such as when the agent is assigned, declines, or closes a work item.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__ConfiguredCapacity__c
Data Type: DOUBLE
Description: The total configured primary capacity of the user.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Description__c
Data Type: TEXT
Description: A description of the Agent Service Presence.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AgentServicePresence record. Maximum size is 15 characters.
Field API Name: std__IdleDuration__c
Data Type: DOUBLE
Description: The duration that the user is idle. This field is updated when the agent’s capacity changes, such as when the agent is assigned, declines, or closes a work item.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsAway__c
Data Type: TEXT
Description: Indicates whether the agent service presence is away (true) or not (false). The default value is false.
Field API Name: std__IsCurrentState__c
Data Type: TEXT
Description: Indicates whether a presence status is the user’s current state (true) or not (false). The default value is false. If true, the agent is in that presence status.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__ServicePresenceStatusId__c
Data Type: TEXT
Description: The ID of the presence status of the the presence user that’s specified by the UserId. This is a One to One (1:1) relationship field. AgentServicePresences is the relationship name and Service Presence Status is the referenced object. Maximum size is 15 characters.
Field API Name: std__StatusDurationSeconds__c
Data Type: DOUBLE
Description: The duration of the user service presence status. This field is set only when the current user service presence status ends, such as when the agent changes to another presence status or logs out. This amount is equal to StatusEndDate minus StatusStartDate. This field is a calculated field.
Field API Name: std__StatusEndDate__c
Data Type: DATETIME
Description: The end date of the user service presence status. This field is set only when the current user service presence status ends, such as when the agent changes to another presence status or logs out.
Field API Name: std__StatusStartDate__c
Data Type: DATETIME
Description: The start date of the user service presence status.
Field API Name: std__UserId__c
Data Type: TEXT
Description: The ID of the Omni-Channel user. This is a One to One (1:1) relationship field. AgentServicePresences is the relationship name and User is the referenced object. Maximum size is 15 characters.
