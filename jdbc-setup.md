# Set up and Configure JDBC | Get Started with Data 360 JDBC | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/jdbc-setup.html

---

With the Data 360 Java Database Connectivity (JDBC) driver, you can access and retrieve data from Data 360 by using tools that support JDBC and Data 360 SQL. This document provides information about setting up and configuring the Data 360 JDBC driver.

Note: Connected Apps are being phased out and cannot be created after February 21, 2026. Use External Client Apps (ECAs) instead. ECAs support the OAuth 2.0 JWT Bearer Flow for JDBC connections. Username-Password Flow and Refresh Token Flow are not supported with ECAs.

Before connecting to Data 360 with the JDBC driver:

Turn on Data 360
Configure Users, Admins, and Permission Sets
Assign Data 360 Permission Sets

Required Permissions:

To create an External Client App and connect JDBC, see the user permissions table in Create an External Client App.
To use your External Client App in a non-default data space, associate the chosen permissions set with the data space. For more information, see Salesforce Help: Associate a Permissions Set with a Data Space.

To connect to your app by using JDBC, create and configure an external client app. Basic app configuration includes creating the app, naming it, and setting the app type to “Server-to-Server Integration.” For complete instructions, see Create an External Client App in Salesforce Help.

After you complete the basic app configuration, complete these steps.

Enable OAuth Settings and configure these options:
Callback URL: Use any valid URL such as http://localhost:55555. The callback URL is required for JWT Bearer authentication.
OAuth Scopes: Select the following scopes:
Manage user data via APIs (api): This scope allows your app to fetch a list of available data spaces and request a Data 360 token.
Perform ANSI SQL queries on Customer Data Platform data (cdp_query_api): This scope allows your app to perform queries with the Data 360 API.
Perform requests at any time (refresh_token, offline_access): This scope enables refresh tokens for offline access.
Configure authentication by enabling JWT Bearer Flow.
Configure OAuth Policies: In the External Client App, go to the Policies tab and click Edit.
Under OAuth Policies, in the Permitted Users section, select Admin approved users are pre-authorized.
Under Select Profiles, choose the permitted profile or, under Select Permission Sets, choose the permitted permission set (but not both).
Click Save.
Retrieve the Consumer Key from the OAuth Usage page of your External Client App in the External Client Apps Manager. Note that the Consumer Secret is not required for JWT Bearer Flow.

Apps using the JDBC driver establish an OAuth 2.0 session with a Salesforce organization configured for Data 360 and then use the provided access token to obtain a Data 360 token. External Client Apps support the OAuth 2.0 JWT Bearer Flow for JDBC connections. See OAuth Authorization Flows.

To use the OAuth 2.0 JWT Bearer Flow, create a public and private key pair and a self-signed certificate. See OAuth 2.0 JWT Bearer Flow in Salesforce Help.

Generating a Key Pair and Certificate

Open a terminal or command prompt and go to the directory where you want to store the generated files.

Create a private and public key pair.

Create a self-signed digital certificate from the key pair, providing your country, state, and organization name when prompted.

Create a PKCS#8 private key from the key pair. PKCS#8 is a standard format for storing private key information that’s compatible with the JDBC driver.

You now have keypair.key, private.key, and certificate.crt files in the folder that you selected.

Configuring the External Client App

In your External Client App configuration, under the API section, click Enable JWT Bearer Flow.
Upload the certificate.crt file to the Digital Signatures section.
Save your configuration.

When connecting with the JDBC driver, provide the contents of the private.key file in the connection settings.

Configure the driver by using a connection URL combined with Java properties. The URL format is jdbc:salesforce-datacloud://<Salesforce Domain Name>.

For the JWT Bearer Flow with External Client Apps, use the Salesforce login domain name: jdbc:salesforce-datacloud://login.salesforce.com. You can use login.salesforce.com instead of your organization-specific My Domain address (such as mycompany.my.salesforce.com).

During connection setup, provide these properties for JWT Bearer Flow authentication:

clientId: Consumer Key from your External Client App
privateKey: Contents of the private key file (PEM format)
userName: Username for the account

Note: The clientSecret (Consumer Secret) is not required for JWT Bearer Flow authentication.

dataspace: Data Space for queries. Default: default.
maxRetries: Number of authentication request retries. Default: 3
User-Agent: This value identifies your application and can help Salesforce Support with debugging. It must be a valid product component as defined in RFC7231, including a version component. Format: salesforce-datacloud-jdbc/version.
