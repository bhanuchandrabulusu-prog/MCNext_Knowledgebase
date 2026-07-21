# Simulate a Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_simulate_recommender.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Simulate a Recommender

After you create a recommender and train it, you can preview recommendations for specific users and for the items that the user is viewing at the time the recommendations are presented. By previewing recommendation results, you can verify the simulation before publishing the recommender.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommenders:	Change and Edit Recommenders
On the Recommenders page, select the recommender you want to simulate.
Click Simulate in the top-right corner.
In the Sample Recipient field, specify the ID of the individual that you want to simulate recommendations for.
Depending on which is used for the root DMO of the profile data graph, the ID is either the user's Individual ID or Unified Individual ID. Use Data Explorer to look up a user’s individual ID or the Unified Individual ID.
(Optional) Enter an Anchor Item ID.
This is the ID of a specific item (for example, a product ID) used as a base item when generating recommendations. For example, if you enter the ID of a "Large Blue T-shirt" as the anchor item, and there’s a filter in place to recommend similar items by color and category, then the simulator displays other blue clothing items in the results. By changing the anchor item, you can test how different starting points affect the recommendations.
Click Simulate.
Review the Results section to view the simulated recommendations.
SEE ALSO
Using Data Graphs With Personalization
Configure Data 360 Insights for Personalization
Personalization Points in Salesforce Personalization
Add Recommendation Filters
