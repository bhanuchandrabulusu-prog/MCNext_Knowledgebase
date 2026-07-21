# Get Started with the Power BI Connector | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/data-cloud-odbc.html

---

Use the Power BI Desktop Connector to connect Microsoft Power BI Desktop to Data 360 and query your data. With this connector, you can authenticate using an OAuth-based flow, connect Power BI Desktop to Data 360, and build dashboards from your query results.

The Power BI Desktop Connector offers these benefits.

DirectQuery Access: Query 360-degree datasets in real-time. Experience live data updates without the need for manual data imports.
Streamlined Navigation: Browse your Data 360 tables and schemas natively within the Power BI Navigator with no SQL required.
Secure OAuth Integration: Authenticate safely using your existing Salesforce credentials for a seamless, governed connection.

Make sure you have the following requirements met:

Turn on Data 360
Configure Users, Admins, and Permission Sets
Assign Data 360 Permission Sets
Install Power BI Desktop on your local machine.
Create an External Client App with OAuth set up.
Download the Power BI Desktop Connector.
Run the setup executable.
If you receive a “could not copy important connector files” error during installation, manually copy the Salesforce.SalesforceData360.pqx file from C:\\Program Files\\Salesforce\\Power BI Connector for Salesforce Data 360 to C:\\Users\\\<your username\>\\Documents\\Power BI Desktop\\Custom Connectors.
If prompted, install the Microsoft Visual C++ 2015-2022 Redistributable.
Restart Power BI Desktop after the installation is complete.

The installation process typically creates a user DSN called Salesforce SalesforceData360 Source and a system DSN called PBI SalesforceData360 Sys. Use the Microsoft ODBC Data Source Administrator to configure these.

Open ODBC Data Sources from the Windows Start menu.
Select either the User DSN or System DSN tab.
Note: Use a System DSN if you are using Power BI’s On-Premises Data Gateway.
Select your Data 360 DSN and click Configure.
On the Connection tab, provide the following:
Login URL: Your org’s login URL. For example, your My Domain URL.
AuthScheme: Set to OAuth.
Client ID / Client Secret: From your configured external client app (required for custom OAuth applications).
Callback URL: The URL of the instance running your desktop Power BI. For example, http://localhost:3333.
Save the DSN and test the connection.
In Power BI Desktop, select Get data.
Search for and select Salesforce Data 360.
Choose the Data 360 DSN you configured.
Choose a Connectivity Mode.
Select Import to import a copy of the data into your project. You can refresh this data on demand.
Select DirectQuery to work with the remote data.
When prompted, complete the OAuth sign-in flow in your browser to grant permissions.
Select the data objects you wish to query and load them into Power BI.

Usage is calculated based on the number of records processed. The count of records processed depends on the structure of a query as well as other related factors such as the total number of records in the objects being queried. When an object is queried in the context of a data space, the number of rows processed is based on the total number of processed rows in the source object, not the number of rows pertaining to the particular data space.

If you choose DirectQuery Power Bi periodically queries your data to keep your dashboards and views up to date. When you choose Import, the Power Bi queries your data only one time.

Review the help documentation included in the connector executable.
