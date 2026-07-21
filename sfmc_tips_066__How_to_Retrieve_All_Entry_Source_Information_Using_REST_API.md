# SFMC Tips #66 : How to Retrieve All Entry Source Information Using REST API

**Source:** https://medium.com/@marketingcloudtips/how-to-retrieve-all-entry-source-information-using-rest-api-d595e48e73e7

---

# SFMC Tips #66 : How to Retrieve All Entry Source Information Using REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d595e48e73e7---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d595e48e73e7---------------------------------------)

8 min read

·

Nov 27, 2024

--

Photo by [Aarón Blanco Tejedor](https://unsplash.com/@the_meaning_of_love?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Have you ever wondered which Data Extensions are being used as entry sources in your currently active journeys, or how those journeys are scheduled?

If you’ve ever wished for a convenient way to view all of this information at once within Salesforce Marketing Cloud, you’re not alone.

In this article, I’ll show you how to access entry sources in Journey Builder and retrieve details such as Data Extension names and schedule settings in bulk. This method leverages the techniques introduced in my previous article, ***How to Retrieve All SQL Queries Using REST API***.

[## SFMC Tips #53 : How to Retrieve All SQL Queries in Salesforce Marketing Cloud Using REST API

### In this article, I’ll introduce a powerful REST API that allows you to bulk retrieve SQL queries created in Salesforce…

medium.com](/@marketingcloudtips/how-to-retrieve-all-sql-queries-in-salesforce-marketing-cloud-using-rest-api-3d5872c2c1ed?source=post_page-----d595e48e73e7---------------------------------------)

## End Goal:

By the end of this tutorial, you’ll be able to view all entry source information in a structured Excel file like the example below:

## Preparation

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----d595e48e73e7---------------------------------------)

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

- **AUTOMATION — Journeys — Read**

For more details, refer to the official documentation:

[## Salesforce Developers

### REST API Permission IDs and Scopes

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_rest_permission_scopes/rest-permissions-and-scopes.html?source=post_page-----d595e48e73e7---------------------------------------)

## API Overview: GET Event Definitions

The entry source settings we aim to retrieve are categorized under “Event Definitions”. These definitions are not limited to entry sources; they also include settings for activities like “Wait Until Event”, which are triggered by events. Keep this broader context in mind as we work with this data.

The official documentation introduces the API we’ll use, but it lacks certain details. I’ll provide practical tips and supplementary information to help you effectively use this API:

[## Salesforce Developers

### Journeys and Events

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/getEventDefinitions.html?source=post_page-----d595e48e73e7---------------------------------------)

## Key Details About Event Definitions

- **Creation/Update Timing:**  
  Event Definitions for entry sources are created or updated when a journey is ***saved***. Drafting an entry source without saving won’t generate an Event Definition. For “Wait Until Event” activities, the definition is created upon completing the activity setup.
- **Multiple Definitions Per Journey:**  
  A single journey can have multiple Event Definitions. For instance, repeatedly creating, deleting, and recreating entry sources generates a new Event Definition each time. Deleted definitions remain in the backend indefinitely, even if the journey is deleted.

## Field Breakdown

Here are the key fields you’ll retrieve using the API:

### 1. id, eventDefinitionKey

These are unique **ID** and **Key** automatically generated when an event definition is created. They uniquely identify each event definition and can be used to reference specific event definitions via API.

### 2. dataExtensionId

This is a unique ID for the data extension associated with the event, distinct from the external key of the data extension. It cannot be retrieved from the Marketing Cloud UI.

***Note:*** *It’s important to mention that this API does not allow you to retrieve the external key of the data extension.*

### 3. type

The **type** field indicates the “type” of the event definition. As mentioned earlier, event definitions are not limited to entry sources. By using this type as a parameter, you can filter results when querying the API.

Here are some key examples of **type** values:

- **EmailAudience**: Standard Data Extension sends
- **AutomationAudience**: Data Extension sends from Automation Studio
- **APIEvent**: API Event
- **CloudPagesSmartCaptureSubmissionEvent**: CloudPages
- **SalesforceObjectTriggerV2**: Salesforce Data

### 4. sourceApplicationExtensionId

This field refers to a unique ID specific to the **type** of the event definition. However, it is rarely used in practical scenarios.

### 5. category

There are two categories for event definitions: **Audience** and **Event**.

- **Audience:** Includes **EmailAudience** and **AutomationAudience** types
- **Event:** Covers all other types

To efficiently narrow down the data, consider adding this **category** as a parameter. For instance, since this article focuses on determining “which data extensions are being used as entry sources”, we will use the parameter `category=Audience`.

### 6. iconUrl

The **iconUrl** field provides an image URL associated with the event type.  
For example:

- For **API Event** types, the URL `/images/icon_journeyBuilder-event-api-blue.svg` indicates an entry source API Event.
- For activities triggered by event definitions, like **Wait Until Event**, the URL might be `/images/xxx.svg`.

### 7. name

For entry source event definitions, the **name** represents the **Journey name** at the time the entry source was created.

***Note:*** *The name reflects the journey name as it was last saved when the entry source was maintained.*

For example:

- If a journey was named “A” during entry source creation and later renamed to “B”, the name of the initial entry source will remain “A”.
- A newly created entry source after renaming the journey to “B” will reflect “B” as its name.

This discrepancy can lead to multiple names for the same draft journey. You can use the **name** field as a parameter for filtering via API.

***Caution:*** *For activities like* ***Wait Until Event****, the name refers to the event definition name itself, not the journey name.*

### 8. dataExtensionName

This displays the name of the data extension selected in the entry source. Unfortunately, this field cannot be used as a parameter for API filtering.

### 9. interactionCount

This counts how many times an event definition has been activated across versions. This field is rarely used in practical scenarios.

### 10. publishedInteractionCount

This is a key field indicating whether the journey is currently active:

- `1`: Active
- `0`: Not active

***Note:*** *This field cannot be used to filter results directly via API; filtering must be done manually, such as in Excel.*

### 11. metaData.scheduleFlowMode

This field indicates the execution mode of the schedule:

- **Run Once**: One-time execution
- **Recurring**: Scheduled recurring execution
- **Automation**: Triggered by Automation Studio

***Note:*** *If no schedule is set, this field will be* `NULL`*.*

### 12. **metaData.runOnceScheduleMode**

This field contains the schedule mode when `scheduleFlowMode` is set to "run once":

- **onSchedule:** At specific date and time
- **onPublish:** On Activation

***Note:*** *If* `scheduleFlowMode` *is set to "recurring" or "automation", this field will be* `NULL`*.*

### 13. metaData.criteriaDescription

If filters were configured during entry source setup, the filtering conditions will be displayed in this field as text. This is particularly helpful when identifying journeys with filtered entry sources.

## How to Configure the REST API

Let’s begin by setting up **Talend API Tester** with the following settings:

```
--- Method  
GET  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/eventDefinitions?$page=1&$pagesize=1000&category=Audience  
  
--- Header  
Content-Type: application/json  
Authorization: Bearer [Access Token]
```

## Notes

- Since this is a `GET` method, there’s no need to input a body.
- If you don’t specify parameters like `$page=1&$pagesize=1000`, only a maximum of 50 event definitions will be retrieved by default.
- Adding the parameter `category=Audience` limits the results to entry sources associated with data extensions.

## Retrieving and Processing the JSON File

Once you execute the request using **Talend API Tester**, the event definitions will be retrieved in JSON format.

In my demo environment, I was able to retrieve **349 event definitions**.

### Step 1: Download the JSON File

Download the retrieved JSON data.

The file should be saved as `eventDefinitions.json`.

![]()

### Step 2: Open Excel and Import the JSON File

Open a new Excel file and navigate to the **Data** tab:

Select **Get Data** → **From File** → **From JSON**, and choose the JSON file you downloaded:

### Step 3: Use the Power Query Editor

The Power Query Editor will open automatically. Click on the **List** field to proceed:

### Step 4: Convert to a Table

Click **To Table**:

When a pop-up appears, proceed with the default settings by clicking **OK**:

### Step 5: Expand Columns

Click the red **expand icon** next to the **List** column:

Select the following fields to expand:

- **name**: The name of the journey
- **dataExtensionName**: The name of the associated data extension
- **metaData** (required for further expansion)
- **publishedInteractionCount**: Indicates whether the journey is active
- **schedule** (required for further expansion)

### Step 6: Expand `metaData` and `schedule`

Expand **metaData** by clicking the red **expand icon**:

Select these three fields:

- **criteriaDescription**: Entry source filter conditions
- **scheduleFlowMode**: Execution mode of the schedule
- **runOnceScheduleMode:** Schedule mode for a “run once” execution

Expand **schedule** by clicking its red **expand icon**:

Select these six fields:

- **startDateTime**: Schedule start time
- **endDateTime**: Schedule end time
- **timeZone**: Time zone of the schedule
- **occurrences**: Number of scheduled executions
- **endType**: How the schedule ends (by count or date)
- **frequency**: Frequency of the schedule (daily, weekly, monthly, etc.)

### Step 7: Load the Data into Excel

When the final preview appears, click **Close & Load** → **Close & Load**:

## Final Output

The **349 event definitions** will now be displayed in Excel, one per row:

## Additional Tips

To view only active journeys, use Excel’s filter feature and filter **publishedInteractionCount** to `1`.

In addition, sort `schedule.endDateTime` in ascending order to find schedules starting from today onward. This will provide **a list of journeys that are active and scheduled to run on or after today**. 👈😄

## Conclusion

By following these steps, you can efficiently access entry sources, data extension names, and schedule settings in **Salesforce Marketing Cloud** using the **REST API** and manage them in bulk. Try applying this method to streamline your processes!

That’s it for now. Hope this was helpful!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

### Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
