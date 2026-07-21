# Recommendation Filters

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Recommendation Filters

Use Recommendation Filters to control which items the recommender suggests to your customers.

On the recommender's Filters page, you include or exclude items based on item attributes, the item the visitor is viewing, or the visitor's profile data.

Add Recommendation Filters
Use filters to control exactly which items appear in your recommendations.
Example Filters for Promotion Eligibility Criteria
Promotions often include criteria around who is eligible to receive it. While Salesforce Personalization does not enforce end-stage validation criteria, such as meeting a minimum spend at checkout, you can suppress recommendations by filtering by profile criteria or user context.
Filter Recommendations Using Dynamic Context Variables
Include or exclude items based on the dynamic variables passed when a user makes a personalization request. For example, you can configure a filter to include items that match the category value passed in the personalization request.
Recommendation Filter Operators
Select the appropriate operator to compare catalog fields against static values, customer profile attributes, or session context to refine recommendation logic.
Filter Items with the Is Subset Operator
Create strict eligibility rules before showing a recommendation or promotion.
