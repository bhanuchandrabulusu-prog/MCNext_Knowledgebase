# Create an Agent Action

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_create_agent_action.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create an Agent Action

To help your agent automatically recognize customer requests and respond with structured, data-driven suggestions, convert your prompt template into an agent action. Agent actions turn flex prompt templates into conversational building blocks that agents can invoke dynamically.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To create a custom agent action:	Manage Agentforce Service Agents AND Manage AI Agents

For example, when you convert a flex prompt template, such as NTO_OutdoorGearFinder, into an agent action, you equip your agent with a dynamic tool to handle specific customer requests. If a customer asks for hiking boots, the agent identifies this intent and automatically invokes the action without human intervention. The agent then retrieves real-time data from Data 360 to generate personalized product recommendations. Instead of requiring custom code for every potential inquiry, the agent uses the defined logic and data retrieval capabilities of the template to deliver structured, data-driven responses directly within the conversation.

Create a custom agent action.

See Create a Custom Agent Action in the Legacy Builder.

This example configuration shows the agent action specifications for the Northern Trail Outfitters agent.

FIELD	ACTION
Reference Action Type	Select Prompt Template.
Reference Action	Select your prompt template. For example, NTO_OutdoorGearFinder.
Agent Action Label	Keep default.
Agent Action API Name	Keep default.
Click Next.
Configure the action instructions based on your requirements.

This example shows the agent action instructions for the Northern Trail Outfitters website.

This action is used to generate personalized outdoor gear recommendations for customers 
based on their activity interests and preferences. The action searches the Northern Trail 
Outfitters product catalog and returns gear suggestions in JSON format for display in the 
web component. Execute this action when customers ask for product recommendations, want to 
see gear options, or inquire about specific outdoor activities.
For the Input parameter, set the instructions.

This example shows the input instructions for the Northern Trail Outfitters website.

Customer query or request for recommendations. Contains the user's input about activities, 
preferences, or specific product types.
For Prompt Response Output, select Show in conversation.
Click Finish.
Add the action to the topic. To allow the agent to use this action when discussing outdoor gear, add it to the Outdoor Gear Recommendations topic you created earlier.

See Add an Action to a Topic in the Legacy Builder.

SEE ALSO
Salesforce Help: Agent Actions in the Legacy Builder
Salesforce Help: Best Practices for Agent Action Instructions
