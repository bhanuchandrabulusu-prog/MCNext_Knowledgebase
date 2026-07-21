# Recommender Considerations

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_considerations.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Recommender Considerations

When configuring a recommender, keep these considerations in mind.

Recommenders use Data 360 data graphs to identify who is eligible to receive personalized content and which content is available to recommend.
A profile data graph configured in a recommender must have a Data Model Object (DMO) of Profile category and have a primary DMO set to Unified Individual, Individual, or Account.
By default, a recommender returns up to 12 recommendations at a time for each personalization point.
If a recommender receives duplicate items for recommendation, one item is selected for display and all other duplicates are dropped.
Before an objective-based recommender can provide recommendations, it must complete minimal training. This training requires at least 3 engagement activities be recorded across the engagement objects that are referenced by the recommender.
