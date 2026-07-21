# SFMC Tips #61 : How to Download Compressed Journey History

**Source:** https://medium.com/@marketingcloudtips/how-to-download-compressed-journey-history-676042a5ac6d

---

# SFMC Tips #61 : How to Download Compressed Journey History

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--676042a5ac6d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--676042a5ac6d---------------------------------------)

4 min read

·

Oct 28, 2024

--

Photo by [Sharon Pittaway](https://unsplash.com/@sharonp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this post, I’ll walk through the new Summer ’24 feature in Salesforce Marketing Cloud, **which allows us to download journey history in a compressed format**.

### Important Note

The journey history compression feature relies on using `curl`, so its compatibility depends on your computer environment. The process differs between Mac and Windows, and even on different Windows machines. For instance, it didn’t work on my work PC, but it did work on my personal one. This example will focus on Windows, but if you encounter issues, I suggest trying on another device. If it still doesn’t work, it may mean your environment doesn’t support compression.

Let’s start by testing the uncompressed version of the Journey History REST API download. Once you confirm it works, we can move on.

[## Extracting Contacts Passing Through Wait activities Using Journey Builder REST API

### In the ever-evolving landscape of Salesforce Marketing Cloud, developers often grapple with the challenge of…

medium.com](/@marketingcloudtips/extracting-contacts-passing-through-wait-activities-using-journey-builder-rest-api-8d22ff0048a0?source=post_page-----676042a5ac6d---------------------------------------)

### REST API for Journey History Download

Refer to the following API documentation:

[## Salesforce Developers

### Journeys and Events

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/downloadJourneyHistory.html?source=post_page-----676042a5ac6d---------------------------------------)

As mentioned in the documentation, this feature requires `curl`, a tool for making HTTP requests. It’s pre-installed on Linux and macOS, and available on Windows 10 and later.

### Step 1: Check `curl` Availability

To check if `curl` is available on your computer, open Command Prompt, paste the following command, and hit Enter:

```
curl --version
```

Ensure `curl` is usable, but note that this doesn’t guarantee successful compression.

### Step 2: Obtain an Access Token

Refer to this article on how to get an **access token** using the Talend API Tester.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----676042a5ac6d---------------------------------------)

### Step 3: Set File Location for the Compressed File

For this example, we’ll save the generated `.gz` file on the **desktop**. To specify this location, you’ll need your PC’s `USER_NAME`, which appears in Command Prompt. Copy it for later use.

### Step 4: Execute the `curl` Command for Journey History Download

Insert your values into the `curl` command below. Edit the `body` (-d) section for the desired data, and then run it in Command Prompt:

```
curl "https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/journeyhistory/download?columns=ContactKey,ActivityId,ActivityName,ActivityType,ClientStatus,CreatedDate,DefinitionId,DefinitionInstanceId,DefinitionName,EndDate,EntrySource,EpochTimeInMilliseconds,EventId,EventName,Id,Message,OutcomeActivityId,SourceType,StartDate,Status,TransactionTime,Result.Status,Result.Tags,Result.Messages,Result.Outcome" ^  
  -X POST ^  
  -H "Authorization: Bearer [Access Token]" ^  
  -H "accept-encoding: gzip" ^  
  -H "x-direct-pipe: true" ^  
  -H "content-type: application/json" ^  
  -d "{ \"start\": \"2024-01-01T00:00:00Z\", \"end\": \"2029-12-31T23:59:00Z\", \"activityIds\": [\"5133bd26-99a1-42e4-8ae7-23aca002bcce\"], \"statuses\": [\"complete\"] }" ^  
  -o "C:\Users\[USER_NAME]\Desktop\journeyhistory.gz"
```

After running, you should see a `journeyhistory.gz` file on your desktop.

![]()

### Step 5: **Decompress the .gz File**

Use a tool like **7-Zip** to decompress the .gz file. You should then have a CSV file, which you can open in Excel to view your data.

### Additional Notes:

- If the CSV file doesn’t have a `.csv` extension, add it to open in Excel.
- If you encounter an error like “Data is corrupted” when extracting, try downloading and extracting the file on a different PC.

And that’s it!

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
