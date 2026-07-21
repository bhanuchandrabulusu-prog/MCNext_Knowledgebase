# Set Up Salesforce CRM Connector for Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_connect_salesforce_org_with_ep_data_data_cloud.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Set Up Salesforce CRM Connector for Salesforce Personalization

Bring your Salesforce Personalization data into Data 360 from another Salesforce org using the Salesforce CRM Connector. You must have admin permissions for the org that you’re connecting.

REQUIRED EDITIONS
USER
PERMISSIONS NEEDED
To use Data 360 for Personalization:	Data Cloud Architect

When using the Salesforce CRM Connector, keep these considerations in mind.

You can’t use the Salesforce CRM Connector to ingest big objects.
Salesforce archives tasks and events that are over 1 year old. When ingesting data, these archived records aren’t included.
The Salesforce CRM Connector uses Bulk API to extract data from Data 360. The concurrency limit for Bulk API extraction is 25 concurrent requests with a duration of 20 seconds or longer.
In Data 360, click Data Cloud Setup.
In the Quick Find box, enter Salesforce CRM, and select Salesforce CRM.
Click New.
Select the Salesforce org that has Data 360 provisioned, and click Connect.
Enter your login credentials.
Give the connection an identifiable name.
Review the connection details.
SEE ALSO
Salesforce Help: Salesforce CRM Connector
