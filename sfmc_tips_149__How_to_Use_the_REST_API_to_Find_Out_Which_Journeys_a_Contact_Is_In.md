# SFMC Tips #149 : How to Use the REST API to Find Out Which Journeys a Contact Is In

**Source:** https://medium.com/@marketingcloudtips/how-to-use-the-rest-api-to-find-out-which-journeys-a-contact-is-in-de16f3f2a43f

---

# SFMC Tips #149 : How to Use the REST API to Find Out Which Journeys a Contact Is In

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--de16f3f2a43f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--de16f3f2a43f---------------------------------------)

5 min read

·

Jul 16, 2025

--

Photo by [Cesar La Rosa](https://unsplash.com/@obcesar?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I introduced the unofficial Salesforce app **“Marketing Cloud Engagement Journeys for Salesforce”**, which allows you to check which journeys a contact or lead is currently in — and even remove them from specific journeys — directly from the record page in Salesforce CRM.

[## SFMC Tips #148 : Introduction to the Marketing Cloud Journeys for Salesforce App

### Released in June 2020 by Salesforce Labs, the unofficial Salesforce app Marketing Cloud Engagement Journeys for…

medium.com](/@marketingcloudtips/introduction-to-the-marketing-cloud-journeys-for-salesforce-app-a5f1c6edde3c?source=post_page-----de16f3f2a43f---------------------------------------)

One example use case of this app would be at a customer support center. If a representative receives a complaint and decides that the customer should no longer receive emails, they can quickly remove that customer from all active journeys.

But what if you’re in an environment where “Marketing Cloud Engagement Journeys for Salesforce” isn’t available?

In that case, you can use the **REST API** to search for the relevant journeys and perform actions programmatically. This article will walk you through the specific steps required.

## Preparation

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----de16f3f2a43f---------------------------------------)

```
--- Method   
POST  
  
--- Endpoint  
https://[Authentication Base URL].auth.marketingcloudapis.com/v2/token  
  
--- Headers  
Content-Type：application/json  
  
--- Body  
{  
 "grant_type": "client_credentials",  
 "client_id": "[Client Id]",  
 "client_secret": "[Client Secret]",  
 "account_id": "[MID]"  
}
```

In the **Scope** of this API configuration, the following is required:

- `Automation - Journeys - Read`
- `Automation - Journeys - Execute`
- `Automation - Journeys - Activate/Stop/Pause/Resume/Send/Schedule`
- `Contacts - List and Subscribers - Read`
- `Data - Data Extensions - Read`

⚠️ Note: Having only `Automation - Journeys - Read` is not sufficient for accurate search results.

[## Salesforce Developers

### REST API Permission IDs and Scopes

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_rest_permission_scopes/rest-permissions-and-scopes.html?source=post_page-----de16f3f2a43f---------------------------------------)

## Check Which Journeys a Contact Is In

You can use the following instructions with **Talend API Tester** or **Postman** to check which journeys a specific contact is currently in.

```
--- Scopes  
Automation - Journeys - Read  
Automation - Journeys - Execute  
Automation - Journeys - Activate/Stop/Pause/Resume/Send/Schedule  
Contacts - List and Subscribers - Read  
Data - Data Extensions - Read  
  
--- Method  
POST   
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/contactMembership  
  
--- Headers   
Content-Type：application/json   
Authorization：Bearer [Access Token]   
  
--- Body  
{  
   "ContactKeyList":["BOR501", "0035Y000072MKdIQAW", "ContactKey_3"]  
}
```

In this example, I’m checking the journey membership of three contacts: `"BOR501"`, `"0035Y000072MKdIQAW"`, and `"ContactKey_3"`. You can include up to **50 contact keys** in a single request using the same format.

## Response

The response will look something like this:

- The `contactMemberships` section contains the journey version information for each contact.
- The `contactNotFound` section lists the contact keys that are **not currently in any journey**.

Note: This response only includes the `definitionKey` of each journey, not the **journey name**. To retrieve the name, you’ll need to make an additional request.

## Retrieve Journey Name from definitionKey

Copy the `definitionKey` from the result above and use it in the following request. You can execute this with **Talend API Tester** or **Postman**.

```
--- Scopes  
Automation - Journeys - Read  
Automation - Journeys - Execute  
Automation - Journeys - Activate/Stop/Pause/Resume/Send/Schedule  
Contacts - List and Subscribers - Read  
Data - Data Extensions - Read  
  
--- Method  
GET  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/key:28f23a58-3797-31f4-6e69-63fc8c642f34  
  
--- Headers   
Content-Type：application/json   
Authorization：Bearer [Access Token]   
  
--- Body  
None
```

## Response

The response will include the journey name. For example, it may return something like `"Journey 008"`.

You’ll notice that the same result can be obtained using the **“Marketing Cloud Engagement Journeys for Salesforce”** app, as shown in a previous article.

## How to Remove a Contact from a Journey

There are two main ways to remove a contact from a journey:

1. Navigate to the journey in **Marketing Cloud Journey Builder** and remove the contact via the **“Health”** section
2. Use the **REST API** to remove the contact programmatically

### 1. Remove via Journey Builder’s “Health” Section

Once you’ve identified the journey name (e.g., **“Journey 008”**), go to **Journey Builder** and click on the **“Health”** button for that journey.

Search by **Contact Key**.

Once the results appear, click **“Remove from Journey”** to delete the contact from the journey.

⚠️ **Note**: The “Health” feature only shows results from the past **30 days**, due to the journey’s activity history limitations.  
 If the contact entered the journey more than 30 days ago and does not appear, you’ll need to use the **REST API** to remove them.

### 2. Remove via REST API

You can also use **Talend API Tester** or **Postman** to remove a contact from a journey.

```
--- Scopes  
Automation - Journeys - Read  
Automation - Journeys - Execute  
Automation - Journeys - Activate/Stop/Pause/Resume/Send/Schedule  
Contacts - List and Subscribers - Read  
Data - Data Extensions - Read  
  
--- Method  
POST   
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/contactexit  
  
--- Headers  
Content-Type：application/json   
Authorization：Bearer [Access Token]   
  
--- Body  
[  
  {  
    "ContactKey": "0035Y000072MKdIQAW",  
    "DefinitionKey": "28f23a58-3797-31f4-6e69-63fc8c642f34"  
  }  
]
```

## Final Thoughts

Once you’ve set this up in **Talend API Tester** or **Postman**, all you need to do is replace the **ContactKey**, and you can reuse the same setup repeatedly.

I highly recommend setting this up once to streamline your contact removal process.

That’s it for now!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
