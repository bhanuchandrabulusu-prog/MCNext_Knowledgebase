# Configure Profile Data Graph for the Maximize Clicks Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_profile_dg_for_max_clicks.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Profile Data Graph for the Maximize Clicks Recommender

To use the maximize clicks recommender, make sure to configure these relationships and add these objects and fields to the profile data graph.

Before configuring a profile data graph for use with the maximize clicks recommender, for the Knowledge Article Engagement object relationships, create a N:1 (ManyToOne) active relationship between its Knowledge Article Version field and the Knowledge Article Version Id field of the Knowledge Article Version object.

OBJECT	FIELD	CARDINALITY	RELATED OBJECT	RELATED FIELD
Knowledge Article Engagement	Knowledge Article Version	ManyToOne	Knowledge Article Version	Knowledge Article Version Id

Use the instructions in Create a Data Graph, but select the fields and objects listed here.

Select Unified Link Individual, and click + to add it.
Select Individual, and click + to add it
Add Knowledge Article Engagement to the data graph.
Next to Knowledge Article Engagement, click + and then select Knowledge Article Version.
Select these related objects, and add the required fields.
NOTE Some fields are preselected for some objects. Leave those fields selected.
RELATED OBJECT	FIELD NAME	FIELD API NAME
Knowledge Article Engagement	Created Date	CreatedDate__c
Individual ID	IndividualId__c
Key Qualifier Individual	KeyQualifierIndividual__c
Key Qualifier Knowledge	KeyQualifierKnowledge__c
Article Engagement Id	ArticleEngagementId__c
Key Qualifier Knowledge Article Version	KeyQualifierKnowledgeArticleVersion__c
Knowledge Article Egagement Id	KnowledgeArticleEgagementId__c
Knowledge Article Version	KnowledgeArticleVersion__c
Engagement Channel	EngagementChannel__c
Engagement Channel Action	EngagementChannelAction__c
Engagement Channel Type	Engagement Channel Type__c
Engagement Verb	EngagementVerb__c
Name	Name__c
Personalization	Personalization__c
Knowledge Article Version	Key Qualifier Knowledge Article Version Id	KeyQualifierKnowledgeArticleVersionId__c
 	Knowledge Article Version Id	KnowledgeArticleVersionId__c
 	Article Number	ArticleNumber__c
 	Main Industry	MainIndustry__c
 	Name	Name__c
Add the direct or related attributes that you want to use for decision targeting or recommendation filters.
Add the Data 360 segments or insights that you want to use when making targeting decisions.
To review the structure of the JSON blob, click Preview.
Save and build the data graph.
