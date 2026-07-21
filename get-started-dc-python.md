# Get Started with the Python Connector | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/get-started-dc-python.html

---

Data 360 Python Connector

Use the Data 360 Python Connector to extract and analyze your Data 360 data in Python. The connector enables you to:

Query Data 360 data using SQL
Work with data in Pandas DataFrames
Create visual data models
Perform analytical operations
Build machine learning and AI models

Install the connector from PyPI:

After successful installation, you’ll see: Successfully Installed salesforce-cdp-connector-<version>

Choose one of two authentication methods:

Create an external client app:

Go to Set up > App Manager > New External Client App
Complete the basic information
Enable OAuth settings
Enter your callback URL
Select required OAuth scopes
Save and continue

Get your credentials:

Copy the consumer key (client ID)
Copy the consumer secret

Create an external client app (same steps as Method 1)

Select these OAuth scopes:

refresh_token
api
cdp_query_api
cdp_profile_api

Get your OAuth tokens:

Construct the authorization URL:
Get the login URL from Set up > My Domain
Get the callback URL from Set up > App Manager > View External Client App > Call Back URL
Open the URL in your browser
Extract the authorization code from the redirect URL
Make a POST request to get tokens:
Save the access_token and refresh_token from the response

Create a cursor and execute your SQL query:

Choose one of three methods to retrieve your data:

After setting up the Python connector, here are some recommended next steps:

Use the connector to query your Data 360 tables
Examine the schema of your data model objects
Try different SQL queries to understand your data structure
Create Pandas DataFrames for data analysis
Use Python libraries like matplotlib or seaborn for visualization
Perform statistical analysis on your data
Connect the connector to your existing Python applications
Set up automated data extraction workflows
Integrate with your data pipeline tools
Learn about Data 360 Query API
Explore Data 360 data model objects
Understand Data 360 limits and guidelines
Use connection pooling for better performance
Implement proper error handling
Follow security best practices for credential management
Monitor your API usage and stay within limits
Join the Salesforce Developer Community
Check out Trailhead modules on Data 360
Explore GitHub examples for Data 360 integration
