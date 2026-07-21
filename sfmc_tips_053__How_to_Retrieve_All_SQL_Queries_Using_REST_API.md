# SFMC Tips #53 : How to Retrieve All SQL Queries Using REST API

**Source:** https://medium.com/@marketingcloudtips/how-to-retrieve-all-sql-queries-in-salesforce-marketing-cloud-using-rest-api-3d5872c2c1ed

---

# SFMC Tips #53 : How to Retrieve All SQL Queries Using REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3d5872c2c1ed---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3d5872c2c1ed---------------------------------------)

4 min read

·

Sep 1, 2024

--

Photo by [Yu Kato](https://unsplash.com/@yukato?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I’ll introduce a powerful **REST API that allows you to bulk retrieve SQL queries created in Salesforce Marketing Cloud’s Automation Studio**. With this API, you can easily identify:

- Which SQL queries use specific fields.
- The target Data Extensions specified in the queries.

This allows you to conveniently check the usage in the relevant SQL queries before deleting a Data Extension, deleting its fields, or changing field names.

## Prerequisites

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----3d5872c2c1ed---------------------------------------)

```
--- METHOD   
POST  
  
--- ENDPOINT  
https://[Authentication Base URL].auth.marketingcloudapis.com/v2/token  
  
--- HEADERS   
Content-Type：application/json  
  
--- BODY  
{  
 "grant_type": "client_credentials",  
 "client_id": "[Client Id]",  
 "client_secret": "[Client Secret]",  
 "account_id": "[MID]"  
}
```

In the **Scope** of this API configuration, the following is required:

- **AUTOMATION — Automation — Read**

With these ready, let’s proceed to retrieve the SQL queries in bulk.

## Setting Up the REST API Request

First, configure the following settings in Talend API Tester (or your preferred API testing tool):

```
--- Method  
GET  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/automation/v1/queries?$page=1&$pagesize=500  
  
--- Header  
Content-Type：application/json   
Authorization：Bearer [Access Token]
```

### Notes:

- By using the `?$page=1&$pagesize=500` parameters, **you can retrieve up to 500 SQL query activities at once**. Without these parameters, only 25 queries will be returned.
- If you have more than 500 queries, you can fetch additional pages by adjusting the parameters, e.g., `?$page=2&$pagesize=500`.

### Considerations:

- As this is a GET method, no request body is needed.
- The `queryText` filter parameter is not supported.
- **The endpoint used here is unofficial**, and therefore not documented in Salesforce’s official help pages.

[## Salesforce Developers

### Automation Studio

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_automation_studio_automations?meta=Summary&source=post_page-----3d5872c2c1ed---------------------------------------)

## Retrieving and Processing the JSON File

When you execute the API request, the response will return the details of up to 500 SQL query activities in JSON format. For example, in my environment, I was able to retrieve 277 queries.

Next, please click the download button in the bottom right corner. After downloading the JSON file (named `queries.json`), follow these steps to process it in Excel:

![]()

1. Open a new Excel file and click on the **Data** tab.

2. Select **Get Data** → **From File** → **From JSON**.

3. Choose the `queries.json` file you just downloaded.

4. Power Query Editor will automatically open. Click on the **List** part to expand it.

5. Convert the list to a table by clicking **To Table**.

6. A pop-up will appear — click **OK** to proceed with the default settings.

7. Click the icon in the red circle to select columns to expand.

8. In the column selection screen, simply click **OK**.

9. The JSON data will be expanded into a preview of your SQL query activities. Click **Close & Load** to finalize.

10. This resulted in 277 SQL query activities being expanded into individual rows.

11. Your SQL query activities will now be displayed, with the `queryText` in column E and the target Data Extension name in column F.

12. Afterward, you can use Excel’s filter feature to search for specific queries using text filters.

## Conclusion

With the steps above, you can efficiently manage your SQL query activities in Salesforce Marketing Cloud using the REST API. This method allows you to access data that is not typically available through the user interface, enhancing your data management capabilities.

I hope you find this guide helpful. Give it a try and see how it can streamline your workflow!

Happy querying!

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
