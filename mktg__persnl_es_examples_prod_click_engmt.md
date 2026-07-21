# Example: Product Click

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_prod_click_engmt.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example: Product Click

This engagement signal monitors for and tracks catalog product (object) click engagement by individuals. Configuring this engagement signal creates a default click count metric.

IMPORTANT The settings provided in this example reflect those in the recommended Salesforce Interactions SDK setup configuration.
CONFIGURATION SEQUENCE	PARAMETER	SETTING
Record Properties	Data Space	default
Engagement DMO	Product Browse Engagement
Name	Product Click
API Name	ProductClick
Field Parameters	User Identifier	Product Browse Engagement > Individual
Item Identifier (Optional)	Product Browse Engagement > Product SKU
Timestamp Identifier	Product Browse Engagement > Engagement Date Time
Unique Engagement Identifier	Product Browse Engagement > Product Browse Engagement Id
Filter	Condition	All Conditions Are Met
Filter Resource	Product Browse Engagement > Engagement Channel Action
Operator	Is Equal To
Value	catalog-object-click
SEE ALSO
Example Engagement Signals
Configure an Engagement Signal
