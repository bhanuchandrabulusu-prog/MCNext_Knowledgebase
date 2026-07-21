# Create an Agent

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_create_agent.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create an Agent

Create the foundational Agentforce Service Agent that serves as your customer-facing representative.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED


To build and manage Service Agents:

To create a custom topic:

	

Manage Agentforce Service Agents AND Manage AI Agents

OR

Customize Application

Create an Agentforce Service Agent.

See Create an Agent from an Agentforce Service Agent Template.

For this example, use these values to configure the Northern Trail Outfitters agent. Customize these values based on your use case.

FIELD	VALUE
Label	Northern Trail Outfitters Agent
API Name	Northern_Trail_Outfitters_Agent
Description	This is the Northern Trail Outfitters Agent that helps customers discover and purchase outdoor gear, providing expert recommendations for hiking, trail running, and outdoor adventures.
Role	The agent's job is to assist customers in discovering the right outdoor gear for their adventures, providing personalized product recommendations, answering questions about equipment specifications, and guiding customers through their outdoor gear selection process.
Company	Northern Trail Outfitters is a premier outdoor equipment and apparel retailer specializing in hiking gear, trail running equipment, outdoor clothing, and adventure accessories for outdoor enthusiasts.
Agent User	New Agent User
Keep a record of conversations with enhanced event logs to review agent behavior	Select
Assign the agent's permission set to users.
From Setup, in the Quick Find box, enter Permission Sets, and then click Permission Sets.
Select the agent’s permission set (for example, here Northern Trail Outfitters Agent Permissions). The permission set is created automatically.
Click Manage Assignments and then Add Assignments.
Select the checkboxes next to EinsteinServiceAgent User, and click Next.
Click Assign.
Create a custom topic to add to your agent, and add it to your agent.

To create custom topics or to add topics, see Create a Custom Topic in the Legacy Builder or Add a Topic to Your Agent in the Legacy Builder.

This example shows an Agent Topic configuration for the Northern Trail Outfitters website.

FIELD	VALUE
Name	Outdoor Gear Recommendations
Classification Description	When a user asks to see, view, or display outdoor gear, products, or equipment use this topic. You must also use this topic when a customer writes they want to know more about a category or specific gear types like "Tell me more about hiking boots", or "I want to discover trail running shoes", or "Show me waterproof jackets".
Scope	Display the output from the NTO_OutdoorGearFinder action. If you are not able to answer a question, gently explain that you are not able to answer. Never try to transfer to an agent. If a customer's intent is to purchase gear, check availability, or need detailed sizing assistance, use the Topic "Product Support".
Instructions	

Display the exact JSON received as an output from NTO_OutdoorGearFinder action and it must start with ```JSON.

Before launching any output action, analyze the customer utterance. Take into account Northern Trail Outfitters has 2 main gender categories: Men, Women. However, gender is just one dimension of our product organization.

Under our product structure, Northern Trail Outfitters has these main categories.

Product Types:

Shoes,

Jackets,

Tops,

Bottoms,

Accessories

Activity Categories:

Hiking,

Trail Running,

Boots,

Rainwear,

Hoodies & Sweatshirts,

Sandals,

Radical Series

SEE ALSO
Salesforce Help: Get to Know Agentforce Service Agent
Salesforce Help: Topics in the Legacy Builder
