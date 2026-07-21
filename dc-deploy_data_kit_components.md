# Deploy Data Kit Components by Using Deploy Data Kit Components Flow | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-deploy_data_kit_components.html

---

Deploy all standard data kit components sequentially to a target org using the Deploy Data Kit Components flow. You provide the input for the flow: data kit name, data space name, and the component payload list and send the POST request to trigger the flow. Before moving to the next component, the flow waits for the deployment status of the previous component. The response body contains the Flow_InterviewGuid.

This flow is available by using the REST API version 61.0 and later.

The basic workflow to deploy standard data kit components includes these steps.

Install your package with a data kit and its components in a target org.
Trigger the flow by using the REST API.

This is the syntax required for the request payload. The payload can be in either JSON or XML format.

POST

Authorization: Bearer token

Name	Type	Description
dataKitComponentsInput	sfdatakit__DeployComponentInput	Required. A collection of data kit components to deploy. The collection list contains the payload details about the components.
dataKitNameInput	Text	Required. The data kit name that contains the components.
dataKitDataSpaceInput	Text	Optional. The name of the data space to deploy the data kit. If a data space isn’t defined, the system deploys the components in the default data space.

The example shows sample input payloads for different data kit components:

Data Stream Bundle

Connector Framework

Ingest API

Streaming App

Calculated Insights

Data Lake Object

Data Graph

Data Transform

DataStream B2C Commerce

Identity Resolution

Segment

To find out which Data 360 components are packageable, see Data 360 Extensibility Readiness Matrix. Deployment Example

This example request triggers the deploy data kit components flow to deploy the data stream bundle, data lake objects, and data transforms components from the ** MyTestDatakit** data kit.

curl https://{MyDomainName}.my.salesforce.com/services/data/v{version}/actions/custom/flow/sfdatakit__DeployDataKitComponents

Data Kit Request Body

Data Kit Response Body

REST API Developer Guide: Deploy Data Kit Components by Using Deploy Data Kit Components Flow
