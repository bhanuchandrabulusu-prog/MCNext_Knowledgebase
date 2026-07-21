# Standard Profile Data Graphs in Personalization Points

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_personalization_point_standard_profile_data_graphs.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Standard Profile Data Graphs in Personalization Points

Real-time data graphs work across all personalization scenarios, however some use cases don’t necessarily require a real-time understanding of an individual. Use a standard profile data graph in such scenarios.

These are some scenarios where you can use a standards profile data graph:

Outbound Messaging: For many messaging scenarios, recipients aren’t necessarily active when a message is sent. Therefore, unlike the mobile or web scenarios, there is no session level context or interaction data that can improve personalization decisions. In this case, a standard data graph provides all necessary context to make a relevant personalization decision.
Batch Personalization: Batch personalization decisions don’t need real-time data as they aren’t shown to an end customer in real-time. They are often included as part of an outbound message.
IMPORTANT Personalization points available for selection in the Web Personalization Manager (WPM) are restricted to only display personalization points that are built against a real-time profile data graph.

When a personalization request contains a personalization point that uses a standard data graph, the calling and evaluation pattern differs from requests made using real-time profile data graphs. The difference primarily includes omitting profile lookup. By omitting this step, Salesforce Personalization maintains decisioning times in milliseconds, as standard data graphs are not optimized for real-time retrieval.

To avoid improper decision evaluation and ensure necessary access to data for decision evaluation, include the individual’s profile data graph JSON in the context object of the request. Unless an individuals profile data graph is passed as part of the personalization request, Salesforce Personalization uses a blank, anonymous profile for evaluating a decision configured against a standard data graph. As a result, the targeting rules evaluate to false when written against profile data or against recommender filter logic that references profile data.

When Salesforce Personalization receives a request for a personalization point configured using a standard profile data graph, it performs these steps.

Salesforce Personalization Pipeline for Standard Profile Data Graph

Makes a request, including the individual’s full profile data graph JSON and personalization point, to Salesforce Personalization’s decision API.
Omits the call to Data 360 profile API as the personalization point uses a standard data graph.
Evaluates decisions using the profile data graph JSON included in the context object of the request.
Runs the selected decision or cohort.
Returns a decision to the requesting application for rendering.
Logs the decision in the personalization log in Data 360.
NOTE For batch personalization and messages sent using Marketing Cloud Growth or Marketing Cloud Advanced, a calling pattern where the profile data graph is included as part of the personalization request is automatically in place.
