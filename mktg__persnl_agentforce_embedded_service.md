# Create an Enhanced Chat Deployment

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_embedded_service.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create an Enhanced Chat Deployment

To integrate agent conversations into your website, create a web deployment. For adaptive website implementations, create a custom web chat deployment to use the Enhanced Chat REST API for agent conversations outside of the standard Salesforce chat widget.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To set up omni-channel flows, to create or change queues, AND to create Enhanced Chat deployment	Customize Application
Set up routing and queues to channel customer inquiries.
Create a new routing configuration.
Create a queue, and include the routing configuration created in the previous step.
Configure an omni-channel flow.
Create an omni-channel flow.
Drag the Route Work action onto the flow canvas.
Add a label to the action.
For Set Input Values | Record ID, select the recordId variable that you created while setting up the flow in Step 2a.
In the Route To field, select Agentforce Service Agent, and then select your agent to route the work item to.
In the Fallback Queue field, select the queue that you configured in Step 1b.
Activate the flow.
Create a messaging channel.
Create a new messaging channel.
Enter the domain of the website where you want to deploy the agent.
Select the omni-channel flow as well as the fallback queue you have created earlier.
Copy and save the code snippet on the Configuration page to add the messaging deployment to your website.
Create a custom client deployment to deliver a highly customized UI with the Enhanced Chat REST API.

See Configure a Custom Client Deployment for Enhanced Chat.

Enable Enhanced Chat REST API.

See Enhanced Chat API.

Access the code snippet you saved in Step 3d, and copy the values.
The 18-digit Organization ID (orgId).
Enhanced Chat REST API base URL for your instance, such as.

https://myinstance.my.pc-rnd.salesforce-scrt.com

The developer name assigned during deployment creation.
Save the details in this format and keep them for when you configure the website connector.
{
  "OrganizationId": "00D000000000000EAA",
  "DeveloperName": "agent_custom_client",
  "Url": "https://myinstance.my.pc-rnd.salesforce-scrt.com"
}
SEE ALSO
Salesforce Help: Configure an Enhanced Web Chat Deployment
Salesforce Help: Advanced Routing with Omni-Channel Flows
