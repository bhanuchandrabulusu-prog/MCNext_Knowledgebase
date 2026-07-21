# Agent Work DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-agentworkdmo-dmo.html

---

Description: The amount of time an agent is actively working on a work item in their console. Active time is tracked only for tasks routed using the tab-based capacity model and only when the work tab is open and in focus in the console. If the agent switches console tabs, the time spent on the other tabs isn’t counted. Active time continues to count if you switch to a new browser tab or window. Active time stops when the agent closes the work item or the after conversation work time ends, whichever happens first.
Field API Name: std__AftConvWorkActualTime__c
Data Type: DOUBLE
Description: The number of seconds an agent spent on After Conversation Work (ACW) after customer contact ended.
Field API Name: std__AftConvWorkExtensionCount__c
Data Type: DOUBLE
Description: The number of times an agent extended the After Conversation Work (ACW) timer.
Field API Name: std__AgentWorkRoutingType__c
Data Type: TEXT
Description: The type of Omni-Channel routing. Possible values are: - QueueBased - SkillsBased Maximum size is 15 characters.
Field API Name: std__AgentWorkStatus__c
Data Type: TEXT
Description: The working status of the work item. Possible values are: - Assigned – The item is assigned to the agent but hasn’t been opened. - Canceled – The item no longer needs to be routed. For example: a chat visitor cancels their Omni-Channel routed chat request before it reaches an agent. - Closed – The item is closed. - Declined – The item was assigned to the agent but the agent explicitly declined it. - DeclinedOnPushTimeout – The item was declined because push time-out is enabled and the item request timed out with the agent. - Opened – The agent opened the item. - Transferred–The item was transferred from an agent to another agent, queue, or skill. - Unavailable – The item was assigned to the agent but the agent became unavailable (went offline or lost connection). Maximum size is 15 characters.
Field API Name: std__BotlId__c
Data Type: TEXT
Description: The ID of the associated bot for the Agent Work.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__CloseDateTime__c
Data Type: DATETIME
Description: Indicates when the work item was closed.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Description__c
Data Type: TEXT
Description: A description of the Agent Work.
Field API Name: std__HandleTimeSeconds__c
Data Type: DOUBLE
Description: The amount of time an agent had the work item open. This is calculated by CloseDateTime minus AcceptedDateTime. Handle time stops when the agent closes the work item or the after conversation work time ends, whichever happens first.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AgentWork record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__PreferredUserId__c
Data Type: TEXT
Description: The ID of the preferred user to handle the work. This field is a relationship field. This field is available in API v46.0 and later.
Field API Name: std__RelatedToId__c
Data Type: TEXT
Description: The ID of the object that’s routed to the agent through Omni-Channel. This field is a polymorphic relationship field. Maximum size is 15 characters.
Field API Name: std__RelatedToObject__c
Data Type: TEXT
Description: The name of the related object for the Agent Work.
Field API Name: std__RequestDateTime__c
Data Type: DATETIME
Description: Indicates when the work was requested.
Field API Name: std__SpeedToAnswerSeconds__c
Data Type: DOUBLE
Description: The amount of time between when the work was requested and when an agent accepted it.
Field API Name: std__UserGroupId__c
Data Type: TEXT
Description: The ID of the queue that the work assignment was originally routed to. This is a One to One (1:1) relationship field. AgentWorks is the relationship name and User Group is the referenced object. Maximum size is 15 characters.
Field API Name: std__UserId__c
Data Type: TEXT
Description: The ID of the user that the work item was assigned to. This field is a relationship field.
