# Choosing a Recommendation Type

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_recommendation_type_choosing.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Choosing a Recommendation Type

The recommendation type defines the method that the recommender uses to provide content. You can choose either objective-based recommendations or rule-based recommendations. Objective-based recommendations use a deep learning model to produce personalized, targeted recommendations for an individual. Rule-based recommendations use business logic to mathematically determine a list of recommendations based on Data 360 calculated insights. For both recommendation types, you can add filters to include or exclude items.

OBJECTIVE-BASED RECOMMENDATIONS	RULE-BASED RECOMMENDATIONS
Uses deep learning algorithms on activity and behavioral data associated with a unique individual to provide personalized experiences.	Relies on calculated insights from the item data graph to rank and sort recommendable content.
Uses deep learning to predict which recommendations to present to an individual to best achieve the selected business goal.	Generates recommendations based on mathematical calculations associated with specific profile attributes (like sales or views) or item attributes (like price, brand, or publish date).
Eligible individuals receive their own, unique set of recommendations based on what the algorithm determines to accomplish the selected business objective.	Eligible individuals receive recommendations based on attributes included in the selected calculated insight.
