# Get Personalization Decision Invocable Action | Personalization Invocable Actions

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/invocable-actions.html

---

Retrieves personalized recommendations from Salesforce Personalization for the specified context and personalization point.

This action is available in API version 63.0 and later.

The Get Personalization Decisions action is available in Salesforce orgs with the Personalization license. For more information on Personalization permissions, see Set Up Salesforce Personalization User Permissions.

URI

/services/data/v63.0/actions/standard/getPersonalizationDecisions

Formats

JSON, XML

HTTP Methods

POST

Authentication

Authorization: Bearer token

Input Parameter	Type	Required?	Description
persnlDecisionInputRepresentation	Apex-defined	Yes	An Apex input representation record that contains context and personalization point details for retrieving a personalization decision.
persnlDecisionContextInputRepresentation	Apex-defined	Yes	An Apex input representation record record that contains details about an individual’s context and the anchor used by Personalization to exclude specific content from recommendations and recommend similar content.
persnlPointInputRepresentation	Array of objects	Yes	A collection of Apex input representation records that contain details about personalization points.
individualId	String	Yes	The ID of the individual to retrieve a personalization decision for.
unifiedIndividualId	String	No	An optional unified ID that associates an individual to a Data Cloud Unified Profile. This ID ensures consistent experimentation cohort assignments for all interactions, even if a user has different individual IDs across channels. Without this ID, a user can end up in different cohorts across channels. Use unifiedIndividualId for experimentation-only use cases.
dataSpace	String	No	The data space in Data Cloud that establishes the logical partition within which the personalization context exists.
anchorId	String	No	A unique ID to be used by Personalization to reference content that the end user is interacting with. This ID helps Personalization stop this content from being recommended. It also lets you suggest more relevant suggestions based on your targeting rules and the filtering rules you set for recommenders.
anchorType	String	No	The API name of the source Data Model Object that contains content that the end user is interacting with.
persnlPointId	String	No	The ID of a personalization point. This value is optional if you specify the name of a personalization point.
persnlPointName	String	No	The API name of a personalization point. This value is optional if you specify the ID of a personalization point.
dynamicContextVariables	Array of objects	No	A list of field-value pairs used to pass dynamic filters, such as category, price, and brand to filter recommendations. Each object in the list must have a field (string) and a value (string).
persnlRecommenderDynamicVariableInputRepresentation	Apex-defined	No	An Apex input representation record that contains a dynamic filter field and value for personalized recommendations.
decisionId	String	No	Optional. The ID of a specific decision to return without rule evaluation. You can specify the decisionId to test whether the Salesforce Personalization Decisioning API returns a particular decision.
invocationType	String	Yes	The type of invocation used for configuring the output response format. Accepted values for use in Flow are FLOW and FLOW_JSON.
Output Parameter	Description
persnlData	A JSON string containing personalized recommendations.
persnlFieldRepresentation	The DMO field representation.
field	The API name of the field.
value	The value associated with the field.
additionalFields	A list of field and value pairs from the personalization recommendation matching the expected schema of the personalization point.
persnlAttributeRepresentation	The content attributes to be returned as configured on the personalization decision
attributeName	The name of the attribute.
attributeValue	The value associated with the attribute.
contentAttributes	Content attributes returned in the personalized decision response as configured in the personalization schema.
persnlDecisionOutputRepresentation	An Apex output representation record that contains details about personalized recommendations, associated data, and diagnostic information.
persnlRepresentation	An Apex output representation record containing personalized recommendations received from Personalization.
persnlRecommendationsOutputRepresentation	An Apex output representation record that contains details about personalized recommendations data, including structured content objects that align with a personalization schema.
persnlDiagnosticsRepresentation	An Apex output representation record that contains diagnostic information related to the personalization request.
persnlPointId	The ID of the personalization point used in the request.
persnlPointName	The name of the personalization point used in this request.
persnlRecommendations	An array of personalized content objects matching the expected schema of the personalization point.
persnlContentId	The ID of a Personalization Content Record.
diagnostics	Diagnostic information about the request, aiding in analysis and troubleshooting.
diagnosticsCode	A diagnostics code tied to the request’s processing or outcome.
diagnosticsDescription	A detailed message offering context and insights related to the diagnostics code.
requestId	A unique ID for the request and its corresponding response.
