# Leverage Data Graphs for Context-Aware AI Agents

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_data_graphs.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Leverage Data Graphs for Context-Aware AI Agents

Data graphs bridge the gap between raw data and AI agents. By aggregating disconnected engagement data such as browsing history, cart activity, and past conversations into a single structure, data graphs provide agents with the real-time context needed to personalize interactions.

To know more about real-time data graphs, see Data Graphs and Grounding with Data Graphs.

Integration Process

The data graph acts as a real-time context engine to capture context, query data, and enrich the profile.

The Web Connector SDK captures the user session and passes the IndividualId to the agent.
The agent uses the IndividualId to query the data graph in real time.
The data graph returns a structured behavioral profile to the agent's context variables.
Implementation Example: Northern Trail Outfitters (NTO)

Scenario:

On NTO's site, a user opens the chat and enters "I need hiking boots for an upcoming trip." Without a data graph, the agent could provide only a generic list of hiking boots. Because NTO set up a data graph based on previous views, chats, and cart engagement, the agent knows that this customer recently did XYZ. The agent replies,

Based on your interest in the Women's RidgeWalker Pro and the trail running shoes in your cart, I'd recommend the Women's FrostStep Thermal Boot (SKU: 9988776) for $130. It offers the same protection you were looking for, plus insulation for cold trail conditions.

Data Graph Structure and Output

Review the data graph's hierarchical structure and the JSON output that provides real-time context to the agent.

Structure:

The data graph organizes engagement data hierarchically under the Individual entity.

Individual
  ├── CatalogEngagement
  ├── CartEngagement
  └── AgentEngagement

JSON Output: This payload represents the data returned to the agent.

{
  "ssot__Id__c": "abc123",
  "CatalogEngagement__dlm": [
    {
      "catalog_id__c": "PROD001",
      "catalog_interactionName__c": "ViewCatalogObject",
      "eventType__c": "product-view"
    }
  ],
  "AgentEngagement__dlm": [
    {
      "agentEngagement_conversationId__c": "CONV001",
      "eventType__c": "agentEngagement",
      "ssot__ConversationEntry__dlm": [
        {
          "ssot__PayloadText__c": "I'm interested in Sales Cloud pricing"
        }
      ]
    }
  ]
}
SEE ALSO
Salesforce Help: Build and Manage Data Graphs
