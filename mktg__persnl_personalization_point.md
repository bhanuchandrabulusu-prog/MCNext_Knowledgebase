# Personalization Points in Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_personalization_point.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Personalization Points in Salesforce Personalization

Use Salesforce Personalization in Marketing Cloud Next to create a personalization point. This object delivers personalized content by tying together a data space, profile data graph, personalization type, and response template. After you define these entities, you can add decisions and targeting rules to the personalization point.

Personalization Point Considerations
When configuring a personalization point, keep these considerations in mind.
Profile Data Graphs in Personalization Points
Whether you select a standard or real-time profile data graph for your personalization point impacts how Salesforce Personalization processes personalization requests.
Configure a Personalization Content Schema
Personalization content schemas are required when configuring personalization points and personalization decisions. A personalization content schema defines the configuration options available to marketers when they’re building a personalization decision. The content schema also ensures that all decision responses for a given personalization point return data in the same format.
Configure a Personalization Point
When you configure a personalization point, you define the data space that the personalization point uses for data and the profile data graph to use for making decisions. You also select a personalization type to define the kind of personalization to provide and a schema to ensure that decision responses appear in a consistent format.
Add a Decision to a Personalization Point
A decision consists of targeting rules. The personalization point uses the decision to determine whether the individual who is engaging with your website or app is eligible to receive personalization content.
Create a Targeting Rule
A targeting rule determines who's eligible for a personalization decision and which personalized content to return.
Modify a Decision
You can change decision properties or priority for a personalization point.
Add a Merge Field
To include profile data in personalization decision text, use merge fields.
