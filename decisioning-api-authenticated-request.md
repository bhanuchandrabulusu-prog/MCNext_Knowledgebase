# Send an Authenticated Personalization Request | Decisioning API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/decisioning-api-authenticated-request.html

---

Place authenticated requests for personalized content for data derived from Salesforce Data Cloud through an authenticated endpoint.

POST /personalization/authenticated/decisions

/personalization/v1/authenticated/decisions

You can authenticate your requests by providing a Data Cloud access token in the header of your request. For guidance on how to generate an access token, see the Getting Started section of the Data Cloud Reference Guide.

Media type: application/json

Parameter	Type	Description
context	Object	Details regarding the context from which the request is taking place. Personalization records the context provided as an extension of Personalization Record in the Personalization Record Data Lake Object (DLO) for this request.
personalizationPoints	Array	
personalizationPoints.id	String	The core ID of a personalization point. Optional if name is provided.
personalizationPoints.name	String	The API name of a personalization point. Optional if id is provided.
personalizationPoints.decisionId	String	Optional ID of the specific decision that must be returned without rule evaluation (for testing purpose)
profile	Object	A Data Cloud Hot Layer Profile. If a profile is provided, the API always uses this profile and skips retrieving the profile from Data Cloud.
executionFlags	Array of Strings	Enumerated values:
TestMode: Indicates whether the call is operating in test mode. In this mode, no outputs are recorded to the data lake.
ContextOnly: Indicates that a call must not look up a profile.

Media type: application/json

Parameter	Type	Description
personalizations	Array	
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
individualId	String	The individual ID to be associated with a Data Cloud Profile.
unifiedIndividualId	String	Optional Unified Individual ID to be associated with a Data Cloud Profile. This ID isn’t used for profile lookup. It’s only used to enable accurate experimentation partitioning in cases that don’t require a profile lookup.
dataspace	String	The data space that defines the boundary of a personalization context.
anchorId	String	The anchor ID to be used by Personalizers referencing a DMO that the end user is interacting with.
anchorType	String	The anchor type to be used by Personalizers.
correlationId	String	Optional ID used for attribution involving multiple personalization requests where a future engagement can contain this ID and is attributed to more than one personalization.
messageId	Any	Optional ID representing an individual outbound message.
requestUrl	String	Optional URL used to automatically parse data such as UTM parameters.
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
profile	Object	A Data Cloud Hot Layer Profile. If a profile is provided, the API always uses this profile and skips retrieving the profile from Data Cloud.
executionFlags	Array of Strings	Enumerated values:
TestMode: Indicates whether the call is operating in test mode. In this mode, no outputs are recorded to the data lake.
ContextOnly: Indicates that a call must not look up a profile.
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
