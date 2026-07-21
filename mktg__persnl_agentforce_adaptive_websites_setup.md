# Set Up Agentforce Adaptive Websites

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_adaptive_websites_setup.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Set Up Agentforce Adaptive Websites

Building an adaptive website involves orchestrating five key layers of technology: data, AI, conversation, web integration, and behavioral tracking. The process moves from establishing a data foundation to deploying client-side components that render the experience.

These phases guide you through the complete setup process for Agentforce Adaptive Websites.

Phase I: Data Foundation
What's involved: Ingest business data, such as product catalogs and customer profiles, into Data 360 DMOs. Create Data 360 search indexes for fast information retrieval. Set up retrievers to fetch real-time data via Retrieval Augmented Generation (RAG). Configure prompt templates in Agent Builder to format AI responses into structured JSON that your website can read.
Outcome: A single source of truth (SSOT) that acts as the backbone for all downstream AI capabilities.
STEP	GOAL
Prepare Data for Your Agent	Consolidate business data into Data 360 DMOs.
Configure an Einstein Retriever	Connect search indexes to prompt templates.
Leverage Data Graphs for Context-Aware AI Agents	Build unified customer profiles for personalization.
Phase II: AI Intelligence
What's involved: Establish the agent's core intelligence by creating a new agent and assigning actions linked to prompt templates. Configure the response structure to return JSON data that the web component renders as personalized content.
Outcome: An intelligent agent capable of understanding natural language and generating data-driven, structured responses.
STEP	GOAL
Create an Agent	Configure an agent to deploy intelligent conversational AI directly to your customers.
Create an Agent Action	Add prompt templates as agent capabilities.
Phase III: Conversation Infrastructure
What's involved: Deploy Enhanced Chat. Configure the Enhanced Chat REST API. Set up context variables to pass user IDs from the website to the agent.
Outcome: A secure channel where the agent can receive user queries and context.
STEP	GOAL
Create an Enhanced Chat Deployment	Enable agent conversations on external websites.
Phase IV: Web Integration
What's involved: Implement the Adaptive Web Agent Component (AWAC) on your site. Create custom React templates to render the JSON responses. For example, render a list of products as a visual carousel rather than text.
Outcome: Agent responses appear as native, integrated web elements, such as product grids or dynamic banners, rather than just chat text.
STEP	GOAL
Set Up the Adaptive Web Agent Component	Add the AWAC library to your website.
Phase V: Behavioral Intelligence
What's involved: Configure the Data 360 web connector to capture real-time signals. Build real-time data graphs to aggregate behavior. For example, "User viewed hiking boots."
Outcome: Live behavioral data flows back into the customer profile, which allows the agent to become smarter and more personalized with every click.
STEP	GOAL
Configure a Data 360 Web Connector	Track real-time customer behavior.
Set Up Agent Engagement Tracking	Capture agent interaction events in Data 360.
SEE ALSO
Agentforce Adaptive Websites
