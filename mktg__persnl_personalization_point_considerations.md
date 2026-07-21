# Personalization Point Considerations

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_personalization_point_considerations.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Personalization Point Considerations

When configuring a personalization point, keep these considerations in mind.

A personalization point requires access to certain data before you configure it. This data resides in Data 360 or is generated using Data 360 functions, such as a data graph or calculated insight. Before configuring a personalization point, set up Data 360 for use with Salesforce Personalization.
A personalization point is linked to a single data space, but a data space can have multiple personalization points linked to it.
You associate a personalization point with a profile data graph that resides in the data space that you select.
The profile data graph you associate with a personalization point impacts the configuration of experiment cohorts and decisions in these ways:
Availability of Recommenders: For personalization points that provide recommendations, you can select only recommenders that were built using the same profile data graph as the personalization point. This restriction ensures that necessary profile data is available for the recommender to reference at run time.
Availability of Data Points for Targeting: The data points available on the profile data graph are eligible for use in decision or experiment targeting logic. The profile data graph data types available for use in targeting rules include direct attributes, related attributes, calculated insights, and segment memberships.
For increased security, you can designate a personalization point as requiring authentication. When authentication is required for the personalization point, evaluations can occur only when using Salesforce Personalization's authenticated decisioning API end point.
When defining a personalization point or personalization decision, you assign a personalization content schema. The personalization content schema defines the format of the personalized content, schema selection options are dependent on the personalization type that you select.
You can create multiple decisions for each personalization point.
The order in which you create each decision determines its initial priority, but you can modify a decision’s priority at any time.
SEE ALSO
Configure a Personalization Point
Add a Decision to a Personalization Point
Configure a Personalization Content Schema
