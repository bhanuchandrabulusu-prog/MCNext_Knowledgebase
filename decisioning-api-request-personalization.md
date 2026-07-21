# Request Personalization | Decisioning API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/decisioning-api-request-personalization.html

---

To request personalized content for an Account, replace "individualId": "" with "profileId": "". You can also pass individualId as part of the profileId attribute.

To request personalized content for an Account, replace "individualId": "" with "profileId": "". You can also pass individualId as part of the profileId attribute.

Media type: application/json

Parameter	Type	Description
context	Object	Details that define the circumstances surrounding a personalization request when it occurs. Personalization records the context provided as an extension of Personalization Record in the Personalization Record Data Lake Object (DLO) for this request.
personalizationPoints	Array	Details of the personalization points used in this request. Make sure all personalization points use the same profile data graph.
personalizationPoints.id	String	The core ID of a personalization point. Optional if name is provided.
personalizationPoints.name	String	The API name of a personalization point. Optional if id is provided.
personalizationPoints.decisionId	String	Optional ID of the specific decision that must be returned without rule evaluation (for testing purpose)
profile	Object	A Data 360 Hot Layer Profile. If a profile is provided, the API always uses this profile and skips retrieving the profile from Data 360.
executionFlags	Array of Strings	Enumerated values:
TestMode: Indicates whether the call is operating in test mode. In this mode, no outputs are recorded to the data lake.
ContextOnly: Indicates that a call must not look up a profile.
EnableDiagnostics: Indicates that the response must include diagnostics.

Media type: application/json

Parameter	Type	Description
personalizations	Array	Details of the personalization content matching the expected schema of the Personalization Point, and diagnostics.
personalizations.personalizationId	String	The response ID.
personalizations.personalizationPointId	String	The core identifier for the personalization point used in this request.
personalizations.personalizationPointName	String	The API name identifier for the personalization point used in this request. This identifier is a reflection of what was passed in the request.
personalizations.data	Array	An array of content objects matching the expected schema of the Personalization Point.
personalizations.attributes	Object	Personalization Attribute values by Attribute Developer Name.
personalizations.diagnostics	Array	Diagnostic information on errors. Available only for authenticated requests.
diagnostics	Array	Diagnostic information on errors. Available only for authenticated requests.
diagnostics.code	String	The error code. Available only for authenticated requests.
diagnostics.description	String	The detailed message describing the error. Available only for authenticated requests.
requestId	String	Unique identifier for this request and response.

Details regarding the context from which the request is taking place. Schema to match, or be an extension of, a Personalization Record. Personalization records the context provided as an extension of Personalization Record in the Personalization Record Data Lake Object (DLO) for this request.

Parameter	Type	Description
individualId	String	The individual ID to be associated with a Data 360 Profile.
profileId	String	The individual or account ID to be associated with a Data 360 profile.
unifiedIndividualId	String	Optional Unified Individual ID to be associated with a Data 360 Profile. This ID isn’t used for profile lookup. It’s only used to enable accurate experimentation partitioning in cases that don’t require a profile lookup.
dataspace	String	The data space that defines the boundary of a personalization context.
anchorId	String	The anchor ID to be used by Personalizers referencing a DMO that the end user is interacting with.
anchorType	String	The anchor type to be used by Personalizers.
correlationId	String	Optional ID used for attribution involving multiple personalization requests where a future engagement can contain this ID and is attributed to more than one personalization.
messageId	Any	Optional ID representing an individual outbound message.
requestUrl	String	Optional URL used to automatically parse data such as UTM parameters.
customContextVariable	String	The custom context value that the recommendation filters refer to filter items. This data isn’t recorded in Data 360. For information about configuring recommendation filters to use custom context variables, see Filter Recommendations Using Dynamic Context Variables
Parameter	Type	Description
personalizationId	String	The ID of the response.
personalizationPointId	String	The core identifier for the personalization point used in the request.
personalizationPointName	String	The API name identifier for the personalization point used in the request. This identifier is a reflection of what was passed in the request.
data	Array	An array of Content Objects matching the expected schema of the Personalization Point.
data.personalizationContentId	String	The identifier for a Personalization Content Record.
attributes	Object	Personalization Attribute values by Attribute Developer Name.
diagnostics	Array	Diagnostic information on errors.
diagnostics.code	String	The error code
diagnostics.description	String	The detailed message describing the error.
Parameter	Type	Description
id	String	The core ID of a personalization point. Optional if name is provided.
name	String	The API name of a personalization point. Optional if id is provided.
decisionId	String	Optional ID of the specific decision that must be returned without rule evaluation (for testing purpose).

A request for one or more personalizations to be made for an individual. If values conflict due to duplicate keys within context, events, and profile, context takes precedence.

Parameter	Type	Description
context	Object	Required. Details regarding the context from which the request is taking place. Schema to match, or be an extension of, a Personalization Record. Context provided as an extension of Personalization Record is recorded in the Personalization Record Data Lake Object (DLO) for this request.
personalizationPoints	Array	Required
personalizationPoints.id	String	The core ID of a personalization point. Optional if name is provided.
personalizationPoints.name	String	The API name of a personalization point. Optional if id is provided.
personalizationPoints.decisionId	String	Optional ID of the specific decision that must be returned without rule evaluation (for testing purpose).
profile	Object	A Data 360 Hot Layer Profile. If a profile is provided, the API always uses this profile and skips retrieving the profile from Data 360.
executionFlags	Array of Strings	Enumerated values:
TestMode: Indicates whether the call is operating in test mode. In this mode, no outputs are recorded to the data lake.
ContextOnly: Indicates that a call must not look up a profile.
EnableDiagnostics: Indicates that the response must include diagnostics.‘
Parameter	Type	Description
personalizations	Array	
personalizations.personalizationId	String	The ID of the response.
personalizations.personalizationPointId	String	The core identifier for the personalization point used in this request.
personalizations.personalizationPointName	String	The API name identifier for the personalization point used in this request. This identifier is a reflection of what was passed in the request.
personalizations.data	Array	An array of Content Objects matching the expected schema of the Personalization Point.
personalizations.attributes	Object	Personalization Attribute values by Attribute Developer Name.
personalizations.diagnostics	Array	Diagnostic information on errors
diagnostics	Array	Diagnostic information on errors
diagnostics.code	String	The error code
diagnostics.description	String	The detailed message describing the error
requestId	String	Unique identifier for this request and response.
