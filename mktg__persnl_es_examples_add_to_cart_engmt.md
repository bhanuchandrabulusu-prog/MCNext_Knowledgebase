# Example: Add To Cart

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_add_to_cart_engmt.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example: Add To Cart

This engagement signal monitors for and tracks when items are added to the cart by individuals. Configuring this engagement signal creates a default add-to-cart count metric.

IMPORTANT The settings provided in this example reflect those in the recommended Salesforce Interactions SDK setup configuration.
CONFIGURATION SEQUENCE	PARAMETER	SETTING
Record Properties	Data Space	default
Engagement DMO	Shopping Cart Product Engagement
Name	Add To Cart
API Name	AddToCart
Field Parameters	User Identifier	Shopping Cart Product Engagement > Individual
Item Identifier (Optional)	Shopping Cart Product Engagement > Product
Timestamp Identifier	Shopping Cart Product Engagement > Engagement Date Time
Unique Engagement Identifier	Shopping Cart Product Engagement > Product Browse Engagement Id
Filter	Condition	All Conditions Are Met
Filter Resource	Shopping Cart Product Engagement > Engagement Channel Action
Operator	Is Equal To
Value	Add To Cart
SEE ALSO
Example Engagement Signals
Configure an Engagement Signal
