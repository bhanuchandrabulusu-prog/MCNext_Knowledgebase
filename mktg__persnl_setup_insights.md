# Configure Data 360 Insights for Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_insights.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Data 360 Insights for Personalization

You can configure Data 360 insights to define and calculate multidimensional metrics for use by Salesforce Personalization. Using insights, you can define specialized metrics to provide more in-depth views into customer activity, better understand site or app interaction, or gauge customer satisfaction.

Using Data 360 Insights with Personalization
You can use any Data 360 insight type with Salesforce Personalization. After you configure the insight types, you add them to data graphs that Personalization uses when making decisions or filtering personalized recommendation content.
Calculated Insight DMO Name and Field Requirements
How you name calculated insight DMOs and their field references depends on the data space that you configure them in. If you configure an insight in the default data space, prepend all DMO names and DMO fields with ssot__. If you’re configuring an insight in a non-default data space, prepend all DMO names and DMO fields with {prefix}__.
Configure a Real-Time Insight for Individual Interactions (Example)
The Individual Interactions Count real-time insight provides the number of events associated with a unified profile. You use the Visual Builder to create a real-time insight.
Configure the Top Sellers Standard Insight for Rule-Based Recommenders
Salesforce Personalization enables you to generate recommendations using controlled business logic. Using a rule-based recommender, you can provide recommendations for top selling, most viewed, co-bought, or co-browsed products, and much more. To rank and sort recommendable content, rule-based recommendations rely on inputs from calculated insights that you add to the item data graph.
