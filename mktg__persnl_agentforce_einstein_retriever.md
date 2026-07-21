# Configure an Einstein Retriever and Reference it in a Prompt Template

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_einstein_retriever.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure an Einstein Retriever and Reference it in a Prompt Template

Create an Einstein Retriever to fetch relevant DMO data based on conversation context and inject it into prompt templates.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To manage retrievers or versions in Einstein Studio (create, edit, and delete):	Data Cloud Architect
To create and manage prompt templates in Prompt Builder:	

Prompt Template Manager permission set

Manage Prompt Templates
Execute Prompt Templates

To create and manage Agentforce Service agents:	Manage Agentforce Service Agents permission set AND Manage AI Agents

Einstein Retrievers implement Retrieval Augmented Generation (RAG), acting as semantic search engines that query Data 360 indexes. When an Agentforce interaction occurs, the retriever searches indexed DMO data using the customer's intent, then dynamically injects results into prompt templates as contextual variables. Prompt templates then use this retrieved data to generate personalized, context-aware responses that combine LLM reasoning with your real-time business information.

Configure a retriever based on your created search index and Data Model Objects (DMOs)

See Create an Individual Retriever.

Create a prompt template.

See Create a Flex Prompt Template.

FIELD	ACTION
Template Type	Select Flex.
Template Name	Add a descriptive name (for example, NTO_OutdoorGearFinder).
Description	Add a description (for example, Outputs JSON of suggested products based on user input).
Resources	Add your retriever.
Write the prompt template text with these sections:
Role - Define the agent's persona and purpose.
Context - Describe your product categories and data structure.
Format and Guardrails - Specify response rules (JSON only, no invented data).
Instructions - Define the process for handling user queries.
Data Source - Reference your Einstein Retriever with the syntax {!$EinsteinSearch:Your_Retriever_Name.results}
Output Instructions - Map DMO fields to JSON output structure.
Example - Provide sample input and expected JSON output.
Create an agent action with the prompt template.

See Create a Custom Agent Action in the Legacy Builder.

FIELD	ACTION
Reference Action Type	Select Prompt Template
Action Name	Add a name (for example, NTO_OutdoorGearRecommendations).
Description	Add a description (for example, Provides personalized outdoor gear recommendations using the product catalog).
Template Selection	Select the your prompt template (in this example, NTO_OutdoorGearFinder).

For the expected JSON schema and formatting requirements for the Adaptive Web Agent Component (AWAC), see Response Structure.

SEE ALSO
Salesforce Help: Retrieve Data
Salesforce Help: Best Practices for Building Prompt Templates
