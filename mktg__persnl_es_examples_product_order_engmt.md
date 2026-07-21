# Example: Product Order

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_product_order_engmt.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example: Product Order

This engagement signal monitors for and tracks catalog product (object) order engagement by individuals. Configuring this engagement signal creates a default product order count metric.

IMPORTANT The settings provided in this example reflect those in the recommended Salesforce Interactions SDK setup configuration.
CONFIGURATION SEQUENCE	PARAMETER	SETTING
Record Properties	Data Space	default
Engagement DMO	Product Order Engagement
Name	Product Order
API Name	ProductOrder
Field Parameters	User Identifier	Product Order Engagement > Individual
Item Identifier (Optional)	Sales Order Product Engagement > Product
Timestamp Identifier	Product Order Engagement > Engagement Date Time
Unique Engagement Identifier	Product Order Engagement > Product Order Engagement Id
Filter	Condition	All Conditions Are Met
Filter Resource	Product Order Engagement > Engagement Channel Action
Operator	Is Equal To
Value	Purchase
SEE ALSO
Example Engagement Signals
Configure an Engagement Signal
