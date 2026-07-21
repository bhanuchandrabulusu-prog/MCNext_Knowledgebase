# Example Filters for Promotion Eligibility Criteria

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_example_filters_for_promotion_eligibility_criteria.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Example Filters for Promotion Eligibility Criteria

Promotions often include criteria around who is eligible to receive it. While Salesforce Personalization does not enforce end-stage validation criteria, such as meeting a minimum spend at checkout, you can suppress recommendations by filtering by profile criteria or user context.

Here’s a list of use cases to define eligibility criteria around promotions in the Salesforce standard data model, and how these use cases translate as filtering criteria in a recommender.

Use Case	Filter Configuration
Limit access to promotion based on Promotion Market Segments inclusion where the individual must be part of all segments	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Market Segment > Market Segment

Filter Type: {profile dg}

Operator: isSubset

Evaluation Criteria: Unified Individual > Segments.Unified Individual - Latest


Limit access to promotion based on Promotion Market Segments inclusion where the individual can be part of any segments	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Market Segment > Market Segment

Filter Type: {profile dg}

Operator: match any

Evaluation Criteria: Unified Individual > Segments.Unified Individual - Latest


Limit access to the loyalty program (which contains promotions and offers) based on loyalty tier attribute	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Loyalty Program > Loyalty Member Tier > Loyalty Tier

Filter Type: {profile dg}

Operator: is equal to

Evaluation Criteria: profileDG.Individual__dlm > … > Loyalty Member Tier > Loyalty Tier


Limit access to the Program (which contains promotions and offers) based on loyalty tier group attribute	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Loyalty Program > Loyalty Member Tier > Loyalty Tier > Loyalty Tier Group

Filter Type: {profile dg}

Operator: is equal to

Evaluation Criteria: profileDG.Individual__dlm > … > Loyalty Member Tier > Loyalty Tier > Loyalty Group Tier


Show promotions and child offers that are relevant to the product page that the individual is currently viewing	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Product

Filter Type: {decision context}

Operator: match any

Evaluation Criteria: Promotion > Promotion Product > Products.ID


Show promotions and child offers that are relevant to the product category page that the user is currently viewing	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Product Category

Filter Type: {decision context}

Operator: match any

Evaluation Criteria: Promotion > Promotion Product Category > Products.Category ID


Show promotions and child offers for product that an individual has not purchased	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Product, orOffer > Offer Product

Filter Type: {profile dg}

Operator: Is Not Equal To

Evaluation Criteria: Unified Individual > Linked Individual > Individual > Sales Order Products > Item ID


Show eligible promotions based on the individual’s birth date	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Channel

Filter Type: {decision context}

Operator: match any

Evaluation Criteria: {!PromotionChannel}


Show partner promotions - partner product is linked to the promotion through Promotion Loyalty Partner Product object (could be product or product category)	

Include or Exclude Filter: Include

Item Data Graph Filter: Promotion > Promotion Product

Filter Type: {decision context}

Operator: match any

Evaluation Criteria: Promotion > Loyalty Program > Loyalty Program Partner > Loyalty Partner Product

SEE ALSO
Recommendation Filter Operators
