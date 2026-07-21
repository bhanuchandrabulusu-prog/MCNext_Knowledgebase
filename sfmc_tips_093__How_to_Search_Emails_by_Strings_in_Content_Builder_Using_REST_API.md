# SFMC Tips #93 : How to Search Emails by Strings in Content Builder Using REST API

**Source:** https://medium.com/@marketingcloudtips/how-to-search-emails-by-strings-in-content-builder-using-rest-api-fdb8492bc934

---

# SFMC Tips #93 : How to Search Emails by Strings in Content Builder Using REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fdb8492bc934---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fdb8492bc934---------------------------------------)

4 min read

·

Mar 28, 2025

--

Photo by [Matheo JBT](https://unsplash.com/@matheo_jbt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the past, I’ve introduced various ways to leverage Salesforce Marketing Cloud’s REST API to retrieve data, such as:

- Retrieving the **SQL query texts** of all SQL Query Activities in Automation Studio in bulk.

[## SFMC Tips #53 : How to Retrieve All SQL Queries Using REST API

### In this article, I’ll introduce a powerful REST API that allows you to bulk retrieve SQL queries created in Salesforce…

medium.com](/@marketingcloudtips/how-to-retrieve-all-sql-queries-in-salesforce-marketing-cloud-using-rest-api-3d5872c2c1ed?source=post_page-----fdb8492bc934---------------------------------------)

- Retrieving the **data extension names** and **scheduled start times** used as entry sources in Journey Builder in bulk.

[## SFMC Tips #66 : How to Retrieve All Entry Source Information Using REST API

### Have you ever wondered which Data Extensions are being used as entry sources in your currently active journeys, or how…

medium.com](/@marketingcloudtips/how-to-retrieve-all-entry-source-information-using-rest-api-d595e48e73e7?source=post_page-----fdb8492bc934---------------------------------------)

This time, I’ll explain how to search for emails that contain specific strings in messages stored in Content Builder.

## Scope of the Search

This method includes AMPscript strings in the search scope but excludes HTML tags. In other words, it targets the strings displayed in Content Builder’s **Default View**.

The **Default View** in Content Builder refers to this:

For instance, if the email body contains the following AMPscript:

```
%%=ContentBlockById("30810786")=%%
```

You can see the same string is displayed in the Default View.

If you search for the string `"30810786"`, you can identify emails using this `ContentBlockById`. Additionally, you can refine the search further by combining multiple strings with AND conditions.

Now, let’s dive into the specifics of using the REST API.

## Prerequisites

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----fdb8492bc934---------------------------------------)

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

- **ASSETS — Documents and Images — Read**

For more details, refer to the official documentation:

[## Salesforce Developers

### REST API Permission IDs and Scopes

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_rest_permission_scopes/rest-permissions-and-scopes.html?source=post_page-----fdb8492bc934---------------------------------------)

## Implementation

### 1. Simple String Search

Here’s how to search for a specific string, such as `"30810786"`. Configure the following settings in **Talend API Tester** or **Postman**:

```
--- Method  
POST  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/asset/v1/content/assets/query  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Sample Body  
{  
  "page": {  
    "page": 1,  
    "pageSize": 500  
  },  
  "query": {      
      "property": "content",  
      "simpleOperator": "mustcontain",  
      "value": "30810786"  
  },  
  "fields": [  
    "id",  
    "name"  
  ]  
}
```

The `"mustcontain"` operator supports both single and multiple conditions.

When you execute this request, you’ll get results like this:

If you check the email (e.g., **Sample Email**) in the result, you’ll see it contains `"30810786"`.

### 2. Searching for Multiple Strings

To identify emails containing a phrase like `"Unmissable Opportunity"`, use the following configuration:

```
--- Method  
POST  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/asset/v1/content/assets/query  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Sample Body  
{  
  "page": {  
    "page": 1,  
    "pageSize": 500  
  },  
  "query": {      
      "property": "content",  
      "simpleOperator": "mustcontain",  
      "value": "Unmissable Opportunity"  
  },  
  "fields": [  
    "id",  
    "name"  
  ]  
}
```

The `"mustcontain"` operator supports multiple conditions. Enter the phrase directly.

Executing this request returns results such as a template-based email, **Sample Email 2**.

When you check **Sample Email 2**, you’ll find it includes `"Unmissable Opportunity"`.

### 3. Combined Search with Content Type

Lastly, to refine searches using a specific content type (e.g., `htmlblock`), use the following:

```
--- Method  
POST  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/asset/v1/content/assets/query  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Sample Body  
{  
  "page": {  
    "page": 1,  
    "pageSize": 500  
  },  
  "query": {  
    "leftOperand": {  
      "property": "content",  
      "simpleOperator": "mustcontain",  
      "value": "Spring Sale 2025"  
    },  
    "logicalOperator": "AND",  
    "rightOperand": {  
      "property": "assetType.name",  
      "simpleOperator": "equal",  
      "value": "htmlblock"  
    }  
  },  
  "fields": [  
    "id",  
    "name"  
  ]  
}
```

## Examples of `assetType.name`

- templatebasedemail
- htmlemail
- textonlyemail
- freeformblock
- textblock
- htmlblock
- imageblock
- buttonblock
- layoutblock

For a full list, refer to:

[## Salesforce Developers

### Asset types are the file or content types supported by Content Builder. Base asset types don't represent actual file…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/base-asset-types.html?source=post_page-----fdb8492bc934---------------------------------------)

## Notes

- Search terms work in any order (e.g., `Spring Sale` or `Sale Spring`).
- Case-insensitive (e.g., `Spring Sale` or `spring sale`).

With this method, you can efficiently locate sub-content in emails using phrases. It’s helpful for troubleshooting or updating old email content.

Give it a try!

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
