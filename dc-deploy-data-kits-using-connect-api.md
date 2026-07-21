# Use the Connect REST API to Deploy Data 360 Data Kits | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-deploy-data-kits-using-connect-api.html

---

Use the deploy data kit components Connect REST API endpoint to programmatically deploy components from a specific data kit to a Data 360 instance. The Connect API offers a seamless, asynchronous deployment process for both standard and DevOps data kits. This API replaces the legacy, flow-based single-click deploy method.

Before starting the deployment, complete these requirements:

Install the package containing your data kit in the target org.
Obtain a valid OAuth access token with scopes for Data 360 Connect APIs.
Locate the API name of your data kit.
Identify the target data space (defaults to default for DevOps data kits).
Obtain the data kit developer name (dataKitDevName).
Assign the Data 360 Architect permission set.

Follow this three-step process to deploy your data kit:

Send a POST request to the deploy data kit components endpoint with asyncMode=true to process the metadata asynchronously. For DevOps data kits, specify only the developerName in the request body. For standard data kits, use the CdpDataKitDeployInputRepresentation object to specify the components you want to deploy.

For complete request schemas and standard data kit component configuration, see the deploy data kit components endpoint.

A successful request returns a 202 Accepted status. The response body includes a jobId, which you use to track the deployment progress.

Poll the status endpoint using the job ID until the jobStatus reaches Completed or Error. See the get deployment job status endpoint for more details about the response schema.

Mandatory Async Mode: Always set asyncMode=true. If you omit this parameter, the system can time out before completing the deployment.

Handle Errors: If the jobStatus is Error, check the errors for details. Typically, failures occur when:

Connectors Are Inactive: Reauthorize sensitive connection data in the target org after installation.
Duplicate API Names: A component with the same API name exists in the target data space.
Environment Parity: Verify that the target data space name exactly matches the data space configuration you used when creating the data kit in the sandbox.
Data 360 Connect REST API: Get data kit manifest
Data 360 Connect REST API: Deploy data kit components
