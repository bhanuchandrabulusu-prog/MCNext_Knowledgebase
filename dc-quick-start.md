# Quick Start | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-quick-start.html

---

To quickly make calls to the Data 360 API, use the Postman collection. For more information and a video tutorial, see Make Data 360 REST API Calls with Postman.

Explore the Data Cloud Online Help if you’re unfamiliar with the application.

Before you can use Data 360 APIs, you must configure the application. To set up the application, see Data Cloud Implementation Overview Guide.

Your org must be provisioned with a Data 360 license, and users must have the Minimum Access - API Only Integrations profile assigned and appropriate permissions to access required objects in Data 360. See Data Cloud Standard Permission Sets.

If you’re using an existing Data 360 instance, confirm with your admin that your user profile has permissions to use Data 360 APIs.

After you create your Data 360 instance, you can control the scope of data ingestion and activation from within the instance.

Set up your data sources by creating an app connector in the Data 360 app. Configure data streams to ingest data for data mapping and segments.

Set up an external client app to authenticate and request access to Data 360 APIs. The external client app enables standard OAuth protocols for authentication and authorization and is a newer version of a connected app. Follow the instructions in Create an External Client App and configure the app depending on the type of OAuth 2.0 flow you intend to use to authenticate to the Salesforce platform and how you want to implement it. For information on configuring an external client app for different OAuth 2.0 flows, see Configure the External Client App OAuth Settings.

In general, you must select Enable OAuth under OAuth Settings and then select the necessary OAuth scopes. These scopes define the permissions for the external client app and are granted as tokens after the app is authorized.

Perform ANSI SQL queries on Data Cloud data (cdp_query_api): The cdp_query_api scope allows ANSI SQL queries of Data Cloud data on behalf of the user.
Manage Data Cloud profile data (cdp_profile_api): The cdp_profile_api scope allows you to manage Data Cloud profile records.
Manage Data Cloud Ingestion API data (cdp_ingest_api): The cdp_ingest_api scope allows access to manage Data Cloud Ingestion API data.
Perform requests at any time (refresh_token): The refresh_token scope allows a refresh token to be returned when the requesting client is eligible to receive one. With a refresh token, the app can interact with the user’s data while the user is offline.
Manage user data via APIs (api): The api scope allows access to the current logged-in user’s account using APIs, such as REST API and Bulk API 2.0.

After creating the external client app, navigate to the Settings tab of the app, click Consumer Key and Secret under OAuth Settings, and copy the Consumer Key and Consumer Secret. You need to use these details to authenticate to Data 360 APIs.

For example, you can configure the external client app to use the web server OAuth 2.0 flow to authenticate to the Salesforce platform. For more information, see Configure a Web Server Flow.

Authentication to the Data 360 API is a two-step process. First, you must authenticate to the Salesforce platform to obtain a Salesforce access token. Then, you use that Salesforce access token to authenticate to the Data 360 tenant for a Data 360 access token. You can then use the Data 360 access token to make API calls to the Data 360 API.

To use the OAuth 2.0 web server flow to authenticate to the Salesforce platform, perform these settings in the external client app:

For simplicity, disable Require Proof Key for Code Exchange (PKCE) Extension for Supported Authorization Flows in the external client app. Depending on the OAuth 2.0 flow type you intend to use, you must configure the required settings in the external client app. For more information, see Configure the External Client App OAuth Settings.

To authenticate to the Salesforce platform, you need a callback URL where Salesforce sends the authorization code after successful authentication. You can either set up a local server (like localhost:3000) for testing or use your actual client URL. You must use the same URL as the callback URL in your external client app.

To authenticate to the Salesforce platform:

Initiate authorization and retrieve the Salesforce authorization code.

a. Navigate to this URL in your web browser.

In this section, the commands use placeholder variables written in uppercase letters with underscores separating the words.

b. In the Salesforce login page, log in using your credentials. After successful login, a consent screen appears.

c. Click Allow to authorize access to Data Cloud APIs. You are redirected to the web page of the redirect URL specified in your request.

d. Copy the Salesforce OAuth code displayed on the web page to use it in the next step.

Exchange the OAuth code obtained in the previous step for the Salesforce access token.

Request

Response

Copy the SALESFORCE_ACCESS_TOKEN to use it in the next step.

Exchange the SALESFORCE_ACCESS_TOKEN for the Data Cloud access token.

Request

Response

Copy these values from the response to use in the Data 360 API requests.

DATA_CLOUD_ACCESS_TOKEN: The token used to access Data Cloud resources.
DATA_CLOUD_INSTANCE_URL: The tenant-specific endpoint where Data 360 API requests are sent.

After you’ve acquired your org-specific Data 360 endpoint (DATA_CLOUD_INSTANCE_URL), use it for your organization’s Data 360 API calls.

Let’s make a sample API call to get the metadata of your Data 360 tenant.

Request
