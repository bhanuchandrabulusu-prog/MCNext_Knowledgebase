# iOS Integration | Personalize Mobile Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalize-mobile-experiences-ios.html

---

Configure the iOS app to identify users and manage consent settings, enabling you to request and display content tailored to specific user interactions.

Install the SDK
Initialize the Data 360 and Personalization Modules
Request Personalization
Access Responses
Example with Request and Response
Error Handling

Add the Personalization module to your Xcode project using Swift Package Manager or CocoaPods.

Install the Data 360 module. See Install the SDK.

Install the Personalization module using either the Swift Package Manager (SPM) or Cocoapods.

Swift Package Manager In Xcode, add this repository to your Xcode project.

https://github.com/salesforce-marketingcloud/Personalization-IOS

Cocoapods Include this pod in your Podfile. See Personalization-IOS.

pod 'Salesforce-Personalization'

Initialize the Data 360 module and the Personalization module early in your application’s lifecycle. You must configure both modules.

The system uses the default data space if you don’t explicitly provide one.

To enable debug logging during development, add this snippet to the code. Make sure this setting is disabled or removed before building your application for production.

For more information on logging, see Logging and Debugging.

The example sets consent to optIn for demonstration purposes. In your production application, you must explicitly manage user consent using the solution provided in the Engagement Mobile SDK. See Data 360 Consent Management.

To retrieve personalization decisions, call fetchDecisions() with the personalization point names.

The fetchDecisions method enables you to interact with the Decisioning API and request one or more personalizations for specific areas of your mobile application.

Use the fetchDecisions method structure to define how your app requests and receives personalization decisions.

Parameter	Description
personalizationPointNames	Array of at least one personalization point name for which you want to return decisions.
context	(Optional) Additional context information. If you don’t have any context, pass nil. See Request Personalization By Using Context.
timeoutSeconds	(Optional) The duration, in seconds, before the fetch task times out. The default is 10 seconds.

If successful, this request returns a DecisionsResponse object. If the task is canceled, it throws a PersonalizationError, or a CancellationError error.

You can use additional context to influence personalization decisions. Use this method only if you have specific context available to affect the decisions. To know about context variables and how they can be used, see Filter Recommendations Using Dynamic Context Variables.

For the DecisionsRequestContext builder, you can optionally add these fields.

Optional Field	Description
anchorID	The unique identifier of the specific item the user is currently viewing. This is helpful in context-aware strategies, such as “People who bought this item also bought…“
anchorDmoName	The API Name of the DMO or the name of the item type (for example, Product or Article) that corresponds to the anchorId. This tells the system what kind of item the anchor is. The DMO name should correspond to the actual one set up in Data 360. Example: ssot__GoodsProduct__dlm.
contextualAttribute	Run-time attributes that help refine recommendation responses and enable advanced filtering logic in your recommenders. To pass multiple attributes, chain a separate method call for each specific key-value pair. For information on contextual attributes, see Filter Recommendations Using Dynamic Context Variables.

The fetchDecisions method interacts with the Decisioning API and requests one or more personalizations for specific areas of your mobile application.

The fetchDecisions method returns a DecisionsResponse object. This object contains both the raw list of personalizations and an optimized dictionary lookup.

Field	Type	Description
requestId	String	The identifier associated with the underlying network request, useful for diagnostics.
personalizations	[DecisionsResponsePersonalization]	An array of all personalization objects returned.
personalizationsByName	[String: DecisionsResponsePersonalization]	A dictionary of personalization points indexed by name. We recommend this instead of an array for efficient access.

Each item in the personalizations array (accessible via personalizationsByName) represents the content returned for a specific personalization point:

Field	Type	Description
personalizationPointName	String	The name of the personalization point requested.
attributes	[String: Any]	The dictionary of attributes (metadata) returned for this personalization. The schema is defined by the personalization setup.
data	[DecisionsResponseContentObject]	An array of content items (the actual personalized content).
decisionId	String?	The optional identifier for the specific decision made by the server.
personalizationId	String	The unique identifier for specific personalization result. This identifier can be used for tracking, analytics, or correlation with other systems.

In the example, fetchDecisions sends the user context to the server to request content for both homeHero and product_recs simultaneously. Once the response arrives, personalizationsByName allows you to access the results for each point independently.

Implement error handling for decision fetching. We recommend logging the exception.
