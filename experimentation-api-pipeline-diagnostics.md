# Experimentation Assignment API Pipeline Diagnostics | Experimentation Assignment API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-api-pipeline-diagnostics.html

---

Experimentation assigns diagnostic codes to every request you make to the Experimentation Assignment API. The API returns these codes in the response for authenticated requests and includes them in the associated ExperimentationLog entry.

While diagnostic codes resemble HTTP status codes, they are specific to the Experimentation Assignment API. Don’t interpret them as standard HTTP errors.

Informational codes indicate normal operation or minor processing notes that don’t prevent the request from completing.

The request executed successfully without unexpected issues.

Diagnostic message: No Experiment qualified

The individual doesn’t qualify for any of the associated experiments in the request.

Processing and general 4XX diagnostic codes indicate issues that occurred due to client-side errors or issues with the request itself. Such errors typically require you to correct the request so that they can be processed successfully.

Diagnostic message: Requested Experiment is not configured.

The Experimentation service cannot locate the experiment specified in the request. This issue occurs when:

The experiment name or ID in the request contains a typo. Ensure the experiment details match the configuration in Data 360.
The request uses an incorrect Tenant Specific Endpoint.
A temporary network issue impacted the request. Retry the request after 30 seconds.
Backend services failed to synchronize the experiment configuration. To resolve, edit and save the experiment, and then retry the request.
The request contains conflicting IDs and names for multiple experiments.

Diagnostic message: Too Many Requests

Internal backend services are handling a high volume of requests. If this occurs, the API returns an HTTP 429 response code. Throttle or hold-off your requests to resolve this issue.

Diagnostic message: Request contained no experiments.

The request doesn’t contain any valid experiments for processing. This error can occur if the service rejects all experiments in the request due to issues identified by codes 401 or 402.

Diagnostic message: Unexpected Error

The service encountered an error while formatting content for the ExperimentationLog or while recording request results.

Diagnostic message: Server interrupted

A low-level server interruption prevented processing. Retry the request.

Diagnostic message: Timeout

This internal-only diagnostic code indicates that your request failed due to a timeout.

This internal code indicates a request timeout. While the service doesn’t include this code in the response body, it triggers a 503 SERVICE UNAVAILABLE response with the message “Timeout Exceeded”.

Diagnostic message: Failed to lookup Experiments from Process Object Service

The service can’t retrieve configuration information for the specified experiments.

While the service doesn’t include this code in the response body, it’s used in the message of an error response. If you encounter this error during a REST API request, it triggers a 503 response with the message “Failed to lookup tenant metadata”.
