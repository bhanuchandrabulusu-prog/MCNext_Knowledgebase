# Decisioning API Pipeline Diagnostics | Decisioning API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/decisioning-api-pipeline-diagnostics.html

---

Personalization assigns diagnostic codes to the execution of all requests made to the Decisioning API. Diagnostic codes are returned in the response for an authenticated request and included in the associated PersonalizationLog entry for unauthenticated requests.

While diagnostic codes resemble HTTP error codes, avoid interpreting them as such. They’re specific to the Decisioning API and serve a different purpose.

Information diagnostic codes provide information about the normal operation of the Decisioning API, indicating that either no issues or only minor issues were encountered.

No unexpected or exceptional issues occurred during the execution of the request.

Diagnostic message: No Decision qualified

This diagnostic code appears in requests where the individual doesn’t qualify for any of the associated personalization point’s configured decisions.

Processing and general 4XX diagnostic codes indicate issues that occurred due to client-side errors or issues with the request itself. Such errors typically require you to correct the request so that they can be processed successfully.

Diagnostic message: Requested Personalization Point is not configured.

This diagnostic code indicates that Personalization was unable to locate the personalization point specified in the request, due to one or more of the following reasons.

There’s a typo in the name or id of the personalization point specified in the request. To avoid this error, ensure that the personalization point details matches those that you configured.
Incorrect Tenant Specific Endpoint.
Temporary network connectivity issues while fetching a personalization point configuration. If network connectivity impacts your request, retry your request after 30 seconds.
The personalization point configuration couldn’t be synchronized with backend services. Edit and re-save the personalization point and retry your request.
Conflicting IDs and names of more than one personalization point.

Diagnostic message: Requested Personalization Point is missing id and name

This diagnostic code indicates that your request is missing properties needed to identify your requested personalization point. To accurately identify a personalization point, your API request must include at least one appropriate identifier such as name or id.

Diagnostic message: Request contained no Personalization Points

This diagnostic code indicates that the request didn’t contain any personalization points that could be used to process the request. This issue can occur if all personalization points specified in the request are rejected due to issues described by 401 and 402 diagnostic codes.

Diagnostic message: Permission Denied

This diagnostic code indicates that your request couldn’t be processed due to permission-related issues such as:

Attempting to request a CoPilot Action personalization decision in an unauthenticated requested. To resolve this issue, either ensure the request is authenticated, or request a non-CoPilot personalization.
Attempting to request batch personalization decisions for CoPilot Actions. CoPilot Action personalizations must be requested individually.
Attempting to request a personalization decision without having Personalization enabled in your instance.

Diagnostic message: Too Many Requests

This internal-only diagnostic code lets internal users know that our backend services are handling too many requests. If backend services encounter this issue, your API requests will receive a 429 HTTP response code, indicating that you must throttle or hold-off requests.

Diagnostic message: No Decision found with specified Decision Id

This diagnostic code is logged when a request includes a decisionId field, but the specified decision can’t be found for the requested personalization point. To resolve this issue, check your personalization point’s configuration in the UI and ensure that the decision you’re requesting by ID is mapped to that personalization point.

Diagnostic message: Specified Decision Feature is not supported for unauthenticated calls

This internal-only diagnostic code indicates that an unauthenticated request included a decisionId field. Such requests result in a 400 HTTP response with the message “Specified Decision Feature is not supported for unauthenticated calls”.

Diagnostic message: No Personalizer was selected

This diagnostic code is logged when Personalization attempts to identify which personalizer to invoke for the request but was unable to find one. This error can occur when:

No decision qualifies for the personalization request, as described by codes 407 and 408. To avoid this issue, ensure that a valid decision qualifies for the request and that a valid personalizer is selected for the request.
No valid personalizer is configured for the decision selected for the request. To resolve this issue, check your personalization point configuration in the UI and ensure a personalizer is configured for the decision being invoked in the request.

Diagnostic message: Requested Personalizer Type is not found

This diagnostic code indicates that a problem with the personalization point’s configuration is preventing Personalization from recognizing the personalizer type associated with an associated decision.

Diagnostic message: Unexpected Error

This diagnostic code is logged when there is an error while formatting content received from the personalizer for writing to the PersonalizationLog, resulting in the Content property of the log being empty. Additionally, errors can occur while preparing to record the request results to the PersonalizationLog.

Diagnostic message: Server interrupted

This diagnostic code indicates that your request couldn’t be processed due to a low-level interruption. Retry your request.

Diagnostic message: Timeout

This internal-only diagnostic code indicates that your request failed due to a timeout.

Although this code doesn’t get logged as a diagnostic code, it’s used in the message of an error response. If you encounter this error during a REST API request, it’ll result in a 503 SERVICE UNAVAILABLE response with the message “Timeout Exceeded”.

Diagnostic message: Failed to lookup Points from Process Object Service

This internal-only diagnostic code indicates that Personalization couldn’t retrieve the configuration information for the personalization points specified in your request.

Although this code doesn’t get logged as a diagnostic code, it’s used in the message of an error response. If you encounter this error during a REST API request, it’ll result in a 503 response with the message “Failed to lookup tenant metadata”.

Diagnostic message: Failed to call Query Service to look up profile

This diagnostic code indicates that an error occurred while calling Data Cloud Query Service to fetch an individual’s profile Data Graph.

Depending on your configuration, your request request either proceeds, treating the individual as anonymous, or returns a 503 failure response with the message “Empty response from Query Service when querying for profile”.

Diagnostic message: Query Service response missing profile

This diagnostic code indicates that Personalization successfully called the Data Cloud Query Service to fetch an individual’s profile data graph, but the response showed that the individual has no profile data graph.

In such cases, your request gets processed, treating the individual as anonymous.

Diagnostic message: Failed to parse profile

This diagnostic code indicates that the response to Personalization’s call to the Data Cloud Query Service to fetch an individual’s profile data graph contains data in an unexpected format. As a result of this error:

targeting rules that require a profile data graph fail to execute properly
recommenders can’t use the individual’s profile data graph to personalize recommendations

Diagnostic message: Failed to execute rules for Decision

This diagnostic code indicates that the evaluation of targeting rules for the associated decision encountered an error. This error occurs if:

Targeting rules were misconfigured. To resolve this issue, check the configuration of your targeting rules for the decision in the UI.
Rules couldn’t be evaluated at runtime due to unexpected data format in the associated profile data graph. To fix this issue, check the individual’s profile data graph to see if there are any data type mismatches.

Diagnostic message: Failed to execute experiment

This diagnostic code indicates that an error occurred while evaluating an experiment, resulting in no personalizer being selected for use in the request.

To resolve this issue, check the configuration of the experiment associated with the specified personalization point.

Diagnostic message: Validation error of rules configurations

This diagnostic code indicates that an error occurred while evaluating the targeting rules for a given decision for the individual’s profile data graph. This error occurs due to reason similar to those that result in diagnostic code 521: RULE_EVALUATION_FAILURE.

Diagnostic message: Error retrieving content from Recommendation Service

This diagnostic code indicates that an error occurred while calling the Recommendation Service to retrieve personalized content for this request. This error could involve either a standard recommendation personalizer or a CoPilot Action personalizer. Additional details about the error are included in the accompanying error message.

Diagnostic message: Error retrieving content

This diagnostic code indicates that the Recommendation Service encountered an error while retrieving personalized content for this request. Additional details about the error are included in the accompanying error message.

Diagnostic message: Content items returned from Recommender exceed limit

This diagnostic code indicates that Personalization has received more items than expected when calling the Recommendation Service to retrieve personalized content for this request. The response is truncated to include only the maximum number of items allowed.
