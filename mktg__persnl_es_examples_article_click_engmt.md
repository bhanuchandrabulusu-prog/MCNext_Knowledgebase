# Example: Knowledge Article Click

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_article_click_engmt.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example: Knowledge Article Click

This engagement signal monitors for and tracks knowledge article click engagement by individuals. Configuring this engagement signal creates a default article click count metric.

CONFIGURATION SEQUENCE	PARAMETER	SETTING
Record Properties	Data Space	default
Engagement DMO	Knowledge Article Engagement
Name	Article Click
API Name	ArticleClick
Field Parameters	User Identifier	Knowledge Article Engagement > Individual
Item Identifier (Optional)	Knowledge Article Engagement > Knowledge Article Version Id
Timestamp Identifier	Knowledge Article Engagement > Created Date
Unique Engagement Identifier	Knowledge Article Engagement > Knowledge Article Engagement Id
Filter	Condition	All Conditions Are Met
Filter Resource	Knowledge Article Engagement > Engagement Channel Action
Operator	Is Equal To
Value	catalog-object-click-start
SEE ALSO
Example Engagement Signals
Configure an Engagement Signal
