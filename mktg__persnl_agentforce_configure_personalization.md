# Configure Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_configure_personalization.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Personalization

After your data is correctly configured in Data 360, set up the necessary components in Salesforce Personalization.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED

To create engagement signals
To create recommenders
	Personalization Admin permission set
Create an engagement signal based on Web Search Engagement DMO so that the recommender knows to use the Search Query data to understand user intent. For more information, see Configure an Engagement Signal.
Select Web Search Engagement as the Data Model Object.
Leave the Catalog id field empty.
Create a custom objective-based recommender that uses the newly created engagement signal. For more information, see Configure an Objective-Based Recommender.
When configuring the custom objective, ensure that you select the newly created engagement signal in the engagement signal selection field, in addition to any others you wish to use.
Assign your new recommender to a personalization point through a personalization decision to make it accessible to your agent. For more information, see Add a Decision to a Personalization Point.
