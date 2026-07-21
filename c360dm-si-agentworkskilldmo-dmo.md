# Agent Work Skill DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-agentworkskilldmo-dmo.html

---

Description: Required. A unique, system-generated identifier for the AgentWorkSkill record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsAdditionalSkill__c
Data Type: TEXT
Description: After a designated timeout period, a skill marked as additional is dropped from Omni-Channel routing. The case is then routed to the best-matched agent, even if the agent doesn’t have all the skills. The default value is false. Available in API version 48.0 and later.
Field API Name: std__IsDropped__c
Data Type: TEXT
Description: Whether the Agent Work Skill was dropped (true) or not (false). Applies to skills marked as additional.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__SkillId__c
Data Type: TEXT
Description: The skill that’s required or additional.
Field API Name: std__SkillLevel__c
Data Type: DOUBLE
Description: The level of the required or additional skill. Skill levels can range from 1 to 10. Depending on your business needs, you might want the skill level to reflect years of experience, certification levels, or license classes.
Field API Name: std__SkillPriority__c
Data Type: DOUBLE
Description: For additional skills, specifies the order in which skills are dropped if after the specified timeout no agent with that skill is available. Higher priority-value skills are dropped first. Lower priority-value skills, for example 0, are dropped last. Skills with the same priority value are dropped as a group. You can set skill priority using attribute setup for skills-based routing or Apex code.
