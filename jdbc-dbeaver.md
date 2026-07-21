# Use JDBC with DBeaver | Get Started with Data 360 JDBC | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/jdbc-dbeaver.html

---

This guide explains how to establish a connection between DBeaver and Data 360. DBeaver provides built-in drivers for Data 360, including one based on the Data 360 Query API and a legacy version using the Data 360 Query V2 API.

Install DBeaver from https://dbeaver.io/download.
Configure an External Client App in Salesforce. See Configure and Establish an OAuth Session. External Client Apps support the JWT Bearer Flow for JDBC connections.

Note: Username-Password Flow does not work with External Client Apps. Use JWT Bearer Flow for authentication.

Open DBeaver: Launch the DBeaver application.

Create New Connection: Go to Database > New Database Connection.

Select Driver: In the connection dialog, search for and select Salesforce Data Cloud, and then click Next.

Configure Connection (Main Tab): The connection dialog appears. On the Main tab, enter:

Username: Your Salesforce username, which corresponds to the userName property.
Password: Leave this field empty when using JWT Bearer Flow with External Client Apps.

Configure Driver Properties (Driver Properties Tab): Go to the Driver properties tab. Configure the necessary properties for JWT Bearer Flow authentication.

Add New Property: Right-click in the blank area under User Properties, and select Add new property.

Enter Property Name: Enter the required property name and click OK.

Enter Property Value: Click in the value field next to the newly added property and enter the corresponding value.

Required Properties for JWT Bearer Flow:

clientId: The Consumer Key from your External Client App
privateKey: The private key associated with your External Client App. Ensure correct configuration. See OAuth 2.0 JWT Bearer Flow.

Optional Properties: For a list of additional configurable properties, see Optional Properties.

Finish Connection: Click Finish.

Verify Connection: Your new Salesforce Data Cloud connection should appear in the DBeaver Database Navigator.

You can query and interact with your Data 360 data through DBeaver. For example, you can use SQL queries to retrieve specific data or create visualizations of your data. See the Get Started with Data 360 SQL guide. Refer to the DBeaver documentation for information on using its features.

To connect to multiple data spaces, create a new connection for each data space.
