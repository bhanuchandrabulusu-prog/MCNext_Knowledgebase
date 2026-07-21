# Using Data 360 Insights with Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_insights_using.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Using Data 360 Insights with Personalization

You can use any Data 360 insight type with Salesforce Personalization. After you configure the insight types, you add them to data graphs that Personalization uses when making decisions or filtering personalized recommendation content.

Calculated Insights

Use a calculated insight to create metrics to better understand things like purchasing or browsing behavior.

When creating a calculated insight for Personalization, keep these considerations in mind.

A calculated insight is near real time and best used when creating metrics associated with items or products, not for real-time Personalization applications.
You can build a calculated insight using either SQL or the Visual Builder.
In an Personalization item data graph, you can use a calculated insight as the source for creating rule-based recommendations.
Real-Time Insights

Use real-time insights to build more complex personalization logic and for tracking things like cumulative website activity for individuals.

When creating a real-time insight, keep these considerations in mind.

Use a real-time insight for events that require real-time consideration.
You can build a real-time insight only on a real-time data graph.
Before building a real-time insight, add all the dimensions and measures that you plan to use to the data graph.
You can only build real-time insights using the Visual Builder. You can’t use SQL.
SEE ALSO
Salesforce Help: Enhance Data with Insights
Using Data Graphs With Personalization
