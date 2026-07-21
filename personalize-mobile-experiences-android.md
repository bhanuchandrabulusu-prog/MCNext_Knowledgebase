# Android Integration | Personalize Mobile Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalize-mobile-experiences-android.html

---

Configure the Android app to identify users and manage consent settings, enabling you to request and display content tailored to specific user interactions.

Install the SDK
Initialize the Data 360 and Personalization Modules
Request Personalization
Access Responses
Error Handling

Integrate the Personalization module into your Android project by updating your Gradle configuration files.

Update the Personalization repository in your module-level build.gradle file.
Add the SDK dependencies to your app’s build.gradle file.
To download the SDK, see Android.

Initialize the Data 360 module and the Personalization module early in your application’s lifecycle. You must configure both modules.

The system uses the default data space if you don’t explicitly provide one.

To enable debug logging during development, add this snippet to the code. Make sure this setting is disabled or removed before building your application for production.

For more information on logging, see Logging and Debugging.

Consent should be set to opt_in for using the Personalization SDK. In your production application, you must explicitly manage user consent using the solution provided in the Engagement Mobile SDK. See Data 360 Consent Management.

The fetchDecisions method enables you to interact with the Decisioning API and request one or more personalizations for specific areas of your mobile application. The SDK provides two methods for fetching personalization decisions: suspend functions (recommended) and callbacks.

Call fetchDecisions within a coroutine scope to handle personalization requests asynchronously.

Parameter	Description
personalizationPointNames	An array of at least one personalization point name for which you want to return decisions.
decisionsRequestContext	(Optional) Additional context information. See Request Personalization By Using Context. If you don’t have any context, pass nil.
timeoutMs	(Optional) The duration, in seconds, before the fetch task times out. The default is 10 seconds.

Grouping personalization point names by datagraph is the responsibility of the caller. This method does not automatically group or separate requests based on datagraph configuration. See Request Personalization.

If your architecture does not support coroutines, use the callback-based implementation of fetchDecisions to handle responses.

Parameter	Description
personalizationPointNames	An array of at least one personalization point name for which you want to return decisions.
context	(Optional) Additional context information. See Request Personalization By Using Context. If you don’t have any context, pass nil.
timeoutMs	(Optional) The duration, in seconds, before the fetch task times out. The default is 10 seconds.
callbackDispatcher	(Optional) The dispatcher for callback. The default is Dispatchers.Main.
callback	Function that executes when the fetch operation completes. The callback receives a Result object containing either a DecisionsResponse on success or a PersonalizationException on failure.

Grouping personalization point names by datagraph is the responsibility of the caller. This method does not automatically group or separate requests based on datagraph configuration. See Request Personalization.

You can use additional context to influence personalization decisions. Use this method only if you have specific context available to affect the decisions. To know about context variables and how they can be used, see Filter Recommendations Using Dynamic Context Variables.

Construct a DecisionsRequestContext object and use the required context.

For the DecisionsRequestContext builder, optionally add the following fields.

Optional Field	Description
anchorID	The unique identifier of the specific item the user is currently viewing. This is helpful in context-aware strategies, such as “People who bought this item also bought…“
anchorDmoName	The API Name of the DMO that corresponds to the anchorId. This tells the system what kind of item the anchor is. The DMO name should correspond to the actual one set up in Data 360. Example: ssot__GoodsProduct__dlm.
contextualAttribute	Run-time attributes that help refine recommendation responses and enable advanced filtering logic in your recommenders. To pass multiple attributes, you need to chain a separate method call for each specific key-value pair. For information on contextual attributes, see Filter Recommendations Using Dynamic Context Variables.

The fetchDecisions method interacts with the Decisioning API and requests one or more personalizations for specific areas of your mobile application.

The fetchDecisions method returns a DecisionsResponse object. This object contains both the raw list of personalizations and an optimized dictionary lookup.

Field	Type	Description
requestId	String	The unique identifier associated with the underlying network request, useful for diagnostics.
personalizations	[DecisionsResponsePersonalization]	An array of all personalization objects returned.
personalizationsByName	Map<String, DecisionsResponsePersonalization	A dictionary of personalization points indexed by name. We recommend this instead of an array for efficient access.

Each item in the personalizations array (accessible via personalizationsByName) represents the content returned for a specific personalization point:

Field	Type	Description
personalizationId	String	The unique ID of the personalization.
personalizationPointName	String	The name of the personalization point requested.
personalizationPointId	String	The ID of the personalization point.
attributes	Map<String, JsonElement>	Mapped JSON object of attributes (metadata) returned for this personalization. The schema is defined by the personalization setup.
data	[DecisionsResponseContentObject]	The JSON object with content items (the actual personalized content).
decisionId	String?	(Optional) The unique identifier for the specific decision made by the server.

In the example, fetchDecisions sends the user context to the server to request content for both homeHero and product_recs simultaneously. After the response arrives, personalizationsByName allows you to access the results for each point independently.

Implement error handling for decision fetching. We recommend logging the exception.
