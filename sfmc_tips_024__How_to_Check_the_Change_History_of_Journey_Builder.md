# SFMC Tips #24 : How to Check the Change History of Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-check-the-change-history-of-journey-builder-1e4015bba67c

---

# SFMC Tips #24 : How to Check the Change History of Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1e4015bba67c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1e4015bba67c---------------------------------------)

5 min read

·

Feb 13, 2024

--

Photo by [mari lezhava](https://unsplash.com/@marilezhava?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Do you ever experience not knowing who made changes to Journey Builder settings? It would be convenient to be able to check the change history of Journey Builder in such cases. Let’s explore the process of auditing Journey Builder using the API.

In this tutorial, we will be utilizing the REST API, specifically the “**Interaction: Get Journey Audit Log**” endpoint, to retrieve the audit log of a journey.

[## Salesforce Developers

### Retrieves an audit log of a journey and its versions by ID or key. Pass in different actions to see history about…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/getInteractionAuditLog.html?source=post_page-----1e4015bba67c---------------------------------------)

## ■ Setting the Stage

Before embarking on this journey, ensure you have the following essentials from a previous guide: the **REST Base URL** and the all-important **Access Token**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----1e4015bba67c---------------------------------------)

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

**AUTOMATION — Journeys — Read**

[## Salesforce Developers

### Review the permission ID, the path to the permission in Marketing Cloud, and the Installed Packages scope for each REST…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html?source=post_page-----1e4015bba67c---------------------------------------)

Now let’s get into the explanation!

## ■ Get Journey ID

First, you need to identify the Journey ID for the journey you want to check. There are two methods to find the Journey ID.

The first one is to use the following SQL query to retrieve the Journey ID:

```
SELECT JourneyID  
, VersionNumber  
, VersionID  
FROM _Journey  
WHERE JourneyName = 'YOUR_JOURNEY_NAME'
```

*Note: You can also retrieve the change history of draft journeys that have never been activated.* ***However, the Journey ID is generated only after saving the draft at least once****.*

The second method is to find the Journey ID in the URL at the location indicated in the diagram below. **Please copy it from after ‘%23’**.

*Note: This ID is different from the Version ID.*

## ■ **Get Journey Audit Log**

In this tutorial, there is no need for additional settings on the Salesforce Marketing Cloud side. Move to “Talend API Tester” for the next steps. Launch a new request, input the following information, and click the “Send” button.

```
--- Method  
GET  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/[Journey ID]/audit/all?versionNumber=[Version Number]  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]
```

Since this is a GET method, there is no need to input anything in the request body. All instructions are specified within the endpoint URL. Extracted endpoint URL is provided below:

Endpoint:  
- Scheme: https  
- Base URL: [REST base URL]  
- Path: /interactions/ [Journey ID] /audit/all  
- Query Parameter: versionNumber= [version number]

Focus on the “all” part; **selecting “all” will retrieve change history of all types**. If you want to examine only a specific type of change history, change “all” to one of the following:

- create (creation)
- modify (modification)
- publish (validate and activate)
- Stop (stop)
- delete (delete)

*\*Unfortunately, “pause” and “resume” events are not included in this change history.*

*\*The* `version Number` *parameter allows you to check only the change history of a specific version. If not needed, you can remove it. Typically, you may want to examine the history of the currently active version, so use the version number of that version.*

By the way, in terms of the content that can be extracted with this API, it includes the following:

- **Who performed the action?**
- **When was the action performed?**

While we would like to know details such as ‘which activity’ and ‘how it was modified’, unfortunately, the API does not provide such granular information. In this context, ‘**modification’ refers to the act of pressing the ‘save’ button in the journey**. Therefore, even if no actual changes were made, pressing the ‘save’ button would still be counted as a ‘modification’.

Regarding the ability to modify email content in the email activity after the journey is active, there may be a question about whether such changes will be recorded in the history. However, since pressing the ‘save’ button in the journey is not involved in this case, these changes won’t be captured in the change history of this REST API.

**As for the change history of email content modifications, a new Job ID is generated, and you can verify the change history by querying the data view**. The extraction method is explained in an article, so please check there for details.

[## SFMC Tips #21 : How to Update Email Content After a Journey Is Active

### After activating a journey in Journey Builder, there may be instances where you want to change part or all of the email…

medium.com](/@marketingcloudtips/how-to-modify-email-content-within-the-same-version-after-activating-a-journey-5dee6fced96c?source=post_page-----1e4015bba67c---------------------------------------)

Let’s return to the topic. After sending the request, success is indicated by a 200 OK response.

The contents initially displayed in the body are folded, so click the ▲ icon on the left of each line to expand only what is necessary.

The following is an example of setting up the email activity.

One important note is that **the timestamps are displayed in the CST timezone**, so you need to calculate them according to your timezone.

## ■ Conclusion

By knowing how to access the change history, troubleshooting becomes more manageable. Give it a try and enhance your Journey Builder management experience.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
