# Configure Personalization: Get Context Action

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_configure_get_context_action.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Personalization: Get Context Action

Use Salesforce Personalization with Agentforce to enable your agents to make better decisions based on real-time access to summarized profile data.

REQUIRED EDITIONS
Available in: Lightning Experience in Enterprise, Unlimited, Professional, and Developer editions with Data 360.
USER PERMISSIONS NEEDED
To assign actions to a topic	

Manage AI agents AND the required permissions for your agent type

OR

Customize Application

Meet these prerequisites before configuring the agent topic to add the Get Context action and update the instructions.

Set up Data 360.
Set up the required profile data graphs with either the Individual ID or the Unified Individual ID as the root DMO, containing useful contextual information to help your agent perform actions more effectively.
Set Up Einstein Generative AI.
Launch the agent and add the Personalization: Get Context action to the required topic using the instructions in Add an Action to a Topic. If you're editing a standard topic, use the instructions in Edit a Standard Topic.
TIP You can add the action to multiple topics, and new topics.
From the Topic Configuration tab, edit the topic field to add a new instruction and paste the following instruction.
If an individualId is known, before performing another action, call the createContextPersonalization action to retrieve {DataGraph API Name} context. Use the sourceId {Agent Version ID} and subjectId {Topic API Name}.
FIELD	DESCRIPTION
DataGraph API Name	The API name of the data graph representing your individual. You can find this on the Data Graphs tab.
Agent Version ID	The version ID of the agent. You can find it appended to the end of the URL when editing the agent in Agent Builder.
Topic API Name	The API name of the topic you're currently editing. You can find this in the Topic Configuration tab.

Example: If an individualId is known, before performing another action, call the createContextPersonalization action to retrieve IndividualDG context. Use the sourceId 0X9SB000000ymMj0AI and subjectId CustomerServiceAssistant.

(Optional) Add additional instructions to guide the agent to use the data from the data graph in a specific way. For example, you can instruct the agent to call createContextPersonalization only once per topic if you don’t expect real time updates to the source data graph during the conversation.
To save your changes, click Finish.
Activate the agent.

After activation, allow the agent a minimum of 60 seconds to allow Personalization to preprocess the configuration.

SEE ALSO
Salesforce Help: Personalization: Get Context
