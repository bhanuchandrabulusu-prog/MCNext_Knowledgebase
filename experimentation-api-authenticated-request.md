# Send an Authenticated Experimentation Assignment Request | Experimentation Assignment API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-api-authenticated-request.html

---

Place authenticated requests for experiment cohort assignments based on data derived from Salesforce Data 360 through an authenticated endpoint.

POST /experimentation/v1/authenticated/assignment

To authenticate your request, provide a Data 360 access token in the header. For instructions on generating an access token, see Data 360 Developer Guide: Quick Start.

Media type: application/json

Parameter	Type	Description
context	Object	Details regarding the context from which the request is taking place.
experiments	Array of Strings	An array of experiment API names or platform IDs in the corresponding dataspace referenced in the context.
experimentsOverride	String of Object	Optional. Test or preview specific experiment variants by forcing an assignment for a user, bypassing the normal evaluation process. This object requires an experiment (ID or API name) and a cohortId (the specific variant). This override only functions when the TestMode flag is included in executionFlags.
profile	Object	Optional. A Data 360 Hot Layer Profile.
Full profile: The API skips the Data 360 lookup.
Partial profile: The API merges this data with the existing Data 360 profile. If keys match, this request’s value takes priority.

executionFlags	Array of Strings	Modifiers that change how the request is processed. Supported values:
TestMode: Evaluate assignments without saving data to the lake.
ContextOnly: Skip the profile lookup.
EnableDiagnostics: Include troubleshooting data in the response.
IncludeUnstartedExperiment: Show experiments that haven’t launched (requires authentication).

Media type: application/json

Parameter	Type	Description
Response Array	Array	A list of one or more experiment responses, based on the number of experiment references specified in the request.
experiment	String	The Platform ID of the Experiment.
variableAssignments	Array	Variable assignments for the experiment. Simple experiments contain one response; multivariate experiments contain nested assignments.
variableAssignments.variableId	String	The ID of the assigned cohort. For simple experiments, this matches the cohortId in the attributes object that follows.
variableAssignments.experimentId	String	The Platform ID of the Experiment.
variableAssignments.experimentName	String	The API name of the Experiment.
variableAssignments.data	String	An optional array of data that can be returned along with the cohort assignment. This is dependent on the response template you chose when designing the experiment.
variableAssignments.attributes	Array	An array of attributes that can be returned with the cohort assignment. The attributes returned vary depending on the template you chose when designing the experiment.
diagnostics	Array	Information about errors or warnings encountered during processing.
diagnostics.code	String	The error code.
diagnostics.description	String	A detailed message describing the error.
requestId	String	The unique identifier for the request and response.

Details regarding the context from which the request is taking place.

Parameter	Type	Description
individualId	String	The Individual ID associated with a Data 360 Profile.
dataspace	String	The data space that defines the boundary of an experimentation context.
Parameter	Type	Description
variableId	String	The parent cohort ID for multivariate experiments. For simple experiments, this matches the cohortId.
experimentId	String	The Platform ID of the Experiment.
experimentName	String	The API Name of the Experiment.
data	String	Optional data returned with the cohort assignment based on the response template.
attributes	Array	Attributes returned with the cohort assignment based on the response template.

A request for one or more experiment assignments for an individual. If values conflict between context, events, and profile, context takes precedence.

Parameter	Type	Description
context	Object	Details regarding the context from which the request is taking place.
experiments	Array of Strings	Array of experiment API names or platform IDs in the corresponding dataspace referenced in the context.
executionFlags	Array of Strings	Enumerated values:
TestMode: Indicates whether the call is operating in test mode. In this mode, no outputs are recorded to the data lake.
Parameter	Type	Description
Response Array	Array	A list of one or more experiment responses, based on the number of experiment references specified in the request.
experiment	String	The Platform ID of the Experiment.
variableAssignments	Array	Variable assignments for the experiment. Simple experiments contain one response, and multivariate experiments contain nested assignments.
variableAssignments.variableId	String	The ID of the assigned cohort. For simple experiments, this matches the cohortId in the attributes object that follows.
variableAssignments.experimentId	String	The Platform ID of the Experiment.
variableAssignments.experimentName	String	The API name of the Experiment.
variableAssignments.data	String	An optional array of data that can be returned with the cohort assignment. This is dependent on the response template you chose when designing the experiment.
variableAssignments.attributes	Array	An array of attributes that can be returned with the cohort assignment. The attributes returned vary depending on the template you chose when designing the experiment.
diagnostics	Array	Information about errors or warnings encountered during processing.
diagnostics.code	String	The error code.
diagnostics.description	String	A detailed message describing the error.
requestId	String	The unique identifier for the request and response.
