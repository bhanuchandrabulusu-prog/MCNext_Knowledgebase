# SFMC Tips #42 : Marketing Cloud Engagement: Summer ’24 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/summer-24-release-highlights-notable-new-features-in-marketing-cloud-0d9ba139c988

---

# SFMC Tips #42 : Marketing Cloud Engagement: Summer ’24 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0d9ba139c988---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0d9ba139c988---------------------------------------)

15 min read

·

May 30, 2024

--

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The release notes for **Salesforce Marketing Cloud Summer ’24**, focusing on new features, have been published. I would like to write an article highlighting these updates.

*\* Please note that this article is based on information available before the release of Summer ’24, so there may be inaccuracies in the content. Please be aware of this in advance.*

**This release will be available between June 7, 2024, and June 28, 2024**. The Summer ’24 update highlights improvements in Automation Studio. Personally, I am delighted because it’s one of my favorite tools. However, on the flip side, this also means that the competition for resources within the same tenant is becoming more intense. Since it is a multi-tenant system, we are affected by the load from other companies. Therefore, the intention is likely to encourage all companies to strive to reduce the load.

With this release being packed with features, let’s take a look at what new functionalities have been introduced in Summer ‘24.

■ Please also check out the article on the previous Spring ’24 release.

[## SFMC Tips #23 : Spring ’24 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Spring ’24, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/spring-24-release-highlights-notable-new-features-in-marketing-cloud-8c769e8402b6?source=post_page-----0d9ba139c988---------------------------------------)

## ■ Automation Studio — Related features

### ① Introduction of the Automation History Dashboard

Regarding this dashboard, **no screen images have been shared yet, so details are unknown**. However, up to this point, data views such as \_AutomationInstance and \_AutomationActivityInstance have been introduced, and the “Download Automation History” feature, which can be downloaded from the location shown in the figure below, has been successively released. Now, the dashboard is finally making its debut.

Released “Download Automation History” feature

This time, it’s specifically a “History” dashboard, a feature for reviewing already completed automations. According to the release notes, it is meant to “View your automations over time and improve overall automation health”, providing information on “automation status, low success rates, and high skip or error counts”. Hmm… honestly, I wonder if I will use this feature.

Unless you’re in an environment where multiple errors occur daily, it seems unlikely that such an error-prone environment would exist, considering that automation is the lifeline of the entire tool.

For now, I plan to wait until the release goes live to check out what the screen looks like and then review it.

*\*Regarding the data views \_AutomationInstance and \_AutomationActivityInstance, I have previously written an article with usage examples, so please check that out.*

[## SFMC Tips #1 : How to find SQL query activities that take more than 15 minutes processing time on…

### Are you effectively utilizing the new data views, \_AutomationInstance and \_AutomationActivityInstance, released for…

medium.com](/@marketingcloudtips/how-to-find-sql-query-activities-that-take-more-than-15-minutes-processing-time-on-automation-7af2df10efca?source=post_page-----0d9ba139c988---------------------------------------)

### 📌 About the User Experience

Since the dashboard has been released, I tried using it. A History tab has appeared in Automation Studio, and you can access it from there.

The dashboard only displays completed automations. Automations that are currently running or scheduled to run are not included. You can apply filters to narrow down searches by automation name or status. The extraction period is limited to one week.

Personally, I felt that the dashboard is “not very useful” as expected. Perhaps the only superior feature is that you can now check the “DURATION” (the runtime of the automation) all at once.

For users, it would be helpful if the following queries I have presented could be incorporated into the functionality.

[## SFMC Tips #45 : How to Bulk Retrieve Execution Times of Automation Activities in Each Step of…

### Have you ever wanted to find out:

medium.com](/@marketingcloudtips/how-to-bulk-retrieve-execution-times-of-automation-activities-in-each-step-of-automation-studio-16903798fc9a?source=post_page-----0d9ba139c988---------------------------------------)

### ② Introduction of the Data Copy or Import activity

What was previously called the Import File Activity is now becoming the **Data Copy or Import activity**.

Salesforce has always announced that for large-scale data, it is recommended to use “value import” from Contact Builder, which is less burdensome than SQL Query Activity. However, since the use of SQL Query Activity hasn’t decreased, they have finally created an activity within Automation Studio that allows for value imports. (👈️ This is my personal opinion.)

Although there has been an import function using “value import” in Contact Builder, it hasn’t been widely used. The key point seems to be how to minimize the amount of work and efficiently move records between data extensions. **From an operational standpoint, the choice between using an SQL query or this new import activity depends on which method is simpler and requires less work**.

- *By the way, it seems that the release of this new import activity will not affect the existing file import activity.*

### 📌 About the User Experience

![]()

Please see the link below for details.

[## SFMC Tips #48 : New Data Copy or Import Activity Arrives in Automation Studio

### The much-anticipated Data Copy or Import activity, which allows the copying of values in data extensions, has finally…

medium.com](/@marketingcloudtips/new-data-copy-or-import-activity-arrives-in-automation-studio-e941f123f7a5?source=post_page-----0d9ba139c988---------------------------------------)

My primary interest was whether, **like Contact Builder’s import function, “filtered data extensions” could be selected as the source or target data extension**.

So, I checked it out right away and, **unfortunately, only “standard data extensions” are available**.

What this means is that filtered data extensions cannot use SQL’s UNION feature under normal circumstances, limiting the conditions you can set.

If filtered data extensions could be used, it would be highly convenient for users who cannot use SQL, as it would perform operations similar to UNION. However, unfortunately, it is restricted to “standard data extensions” only.

***For more information on the UNION feature with filtered data extensions****, please refer to my previous article. It’s crucial information.*

[## SFMC Tips #31 : How to Add Records to a Filtered Data Extension

### Salesforce Marketing Cloud’s filtered data extensions allow you to set specific criteria and store records that meet…

medium.com](/@marketingcloudtips/how-to-add-records-to-a-filtered-data-extension-64857d3fc4ff?source=post_page-----0d9ba139c988---------------------------------------)

### ③ Recommended Automation Start Time Feature

Although I don’t think this is particularly AI-recommended, it seems to gather statistics on automation across the entire tenant and suggest times when the system is less busy. Screenshots of this feature have been shared.

The choice of hour is quite important when scheduling, **but the specific minute may not matter as much. For such automations, this feature might be useful**.

As you may already know, **it has always been possible to schedule automation in one-minute increments**. As shown in the figure below, after selecting something from the dropdown, you just click on the time part with the mouse and type in the numbers.

Times like on the hour or half past the hour tend to get congested because people who are unaware of this tend to set their schedules that way. Therefore, starting at, for example, 17 minutes past the hour instead of on the hour is already possible. If you’re concerned about automation speed, I recommend trying this.

### 📌 About the User Experience

I looked into how this feature works and found that for all time slots (from 0:00 to 23:00), **selecting times between “26” to “36” minutes and “46” to “06” minutes will result in a red mark and a recommended time will be shown (denoted by ✕ in the table below)**.

On the other hand, **selecting times between “07” to “25” minutes and “37” to “45” minutes will result in a green mark and no recommended time will be displayed (denoted by ◯ in the table below)**.

If the recommended minute slots, as shown in the table above, were not uniformly applied across all time slots (from 0:00 to 23:00), there might be some expectations for this recommendation feature. However, since this logic is common across all time slots, I’m a bit skeptical.

**In essence, it seems like the system is indicating that statistically, the “07” to “25” minute and “37” to “45” minute slots are relatively less busy**.

[## SFMC Tips #49 : Introducing the New Feature: Recommended Automation Start Times

### The Salesforce Marketing Cloud Summer ’24 release is nearing its conclusion. A new feature that recommends automation…

medium.com](/@marketingcloudtips/introducing-the-new-feature-recommended-automation-start-times-259b17962f37?source=post_page-----0d9ba139c988---------------------------------------)

### ④ Running Automations in 15-Minute Intervals

*\*This feature has already been released.*

This feature was suddenly released a while ago and became a topic of discussion on LinkedIn. **Previously, the smallest interval for automations was one hour, but now they can be run in 15-minute intervals**. This feature was gradually rolled out in May 2024.

One trap when using this 15-minute interval feature is that most of you probably have a corporate edition contract, **which has a limit of 45,000 automation runs**. Running an automation every hour for 365 days results in 8,760 runs, which is manageable. However, **increasing this by four times results in 35,040 runs**. Therefore, creating two automations running every 15 minutes would exceed the 45,000 limit.

There have been reports of unexpected invoices being sent due to exceeding limits, so caution is necessary. Especially for consultants providing support, please be mindful of these limits. To prevent unexpected charges for clients, be sure to obtain permission before implementing automation at 15-minute intervals.

### ⑤ Additional Fields in Automation History Download

As mentioned in point 1, fields such as **source, creation date, frequency, and latest execution date will be added** to the automation history download.

## ■ Journey Builder — Related features

### ① Access Useful Information on the Journey Canvas

For troubleshooting purposes, **you will be able to quickly find the total number of activities in a journey and easily obtain the version’s Definition ID on the Journey Canvas**.

Previously, **you could retrieve the Journey ID**, which is a higher-level ID compared to the Version ID, from the screen. **The Journey ID was displayed in the URL, and you could obtain it by copying the part of the URL after “%23”**.

![]()

Additionally, **you could also retrieve the Activity ID**, a lower-level ID compared to the Version ID, from the screen. I’ve previously written a standalone article on this topic, which you can refer to for more details.

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----0d9ba139c988---------------------------------------)

![]()

Now, let’s see where you can find the Version ID. **By clicking the arrow next to the journey name, the Definition ID will be displayed**. This Definition ID is actually the Version ID.

![]()

![]()

To confirm that this Definition ID (e.g., 494bf347–3083–463f-a8b3-f2436542e7a6) is indeed the Version ID, you can query the data view as follows:

```
SELECT JourneyID,  
       VersionNumber,  
       VersionID  
FROM _Journey  
WHERE JourneyID = '7af07913-1dbc-46b8-b8e3-d0dac692bea5'  
AND VersionNumber = '181'
```

![]()

As you can see, this confirms that the Definition ID is the Version ID.

### ② Assign Relative “High” Priority Between Journeys

System priority determines the relative importance of journeys in terms of using system resources (server capacity). **In addition to the existing “Low” and “Standard” system priorities, you can now choose “High” priority between journeys**.

It’s difficult to gauge the actual impact without experiencing it firsthand, but in conjunction with the “High-Throughput Sending” feature launched in the previous release, this aims to achieve faster and more stable deliveries.

To set this up, navigate to the bottom of the “System Optimization” tab where you’ll find a list of journeys. Check the checkbox next to the journey for which you want to change the priority, **enabling the “Change Priority” button**. By default, all are set to “Standard”.

In this settings interface, you can also schedule the validity period of the priority, specifying start and end dates and times.

## ■ API— Related features

### ① Ability to Compress Journey History Downloads

The Journey History Download API, which I have previously written about, used to download files in CSV format, but now it allows for compressed downloads. You can find the article on the Journey History Download API below. It’s extremely useful, so please give it a try.

[## Extracting Contacts Passing Through Wait activities Using Journey Builder REST API

### In the ever-evolving landscape of Salesforce Marketing Cloud, developers often grapple with the challenge of…

medium.com](/@marketingcloudtips/extracting-contacts-passing-through-wait-activities-using-journey-builder-rest-api-8d22ff0048a0?source=post_page-----0d9ba139c988---------------------------------------)

There was a 1 GB limit on downloads, which required reducing the amount of data, but by compressing the files, the capacity has effectively been increased.

You can execute it using cURL or similar tools.

```
curl "https://YOUR_SUBDOMAIN.rest.marketingcloudapis.com/interaction/v1/interactions/journeyhistory/download" \  
  -X POST \  
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \  
  -H "accept-encoding: gzip" \  
  -H "x-direct-pipe: true" \  
  -H "content-type: application/json" \  
  -d '{  
   "start": "2024-06-11T06:00:00Z",  
   "end": "2029-07-11T21:00:00Z",  
   "definitionIds": ["58c2edb1-703e-45d8-9841-9e5d63ed1117"],  
   "statuses": ["failed"]  
}'
```

### ② Manage Data Extensions with the REST API

While the help document briefly mentions this, it’s actually quite significant. Until now, managing Data Extensions with an API meant using the SOAP API. Essentially, it was a legacy feature. Now, it can also be done using the REST API.

[## Salesforce Developers

### Custom Objects

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_objects?meta=Summary&source=post_page-----0d9ba139c988---------------------------------------)

![]()

[## Salesforce Developers

### Data Extension Data

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_object_data?meta=Summary&source=post_page-----0d9ba139c988---------------------------------------)

I immediately tried the most likely to be frequently used feature, “Creating a New Data Extension”.

[## SFMC Tips #44 : Creating a New Data Extension Using the REST API

### In the Summer ’24 release of Salesforce Marketing Cloud, a Custom Object REST API was introduced to manage data…

medium.com](/@marketingcloudtips/creating-a-new-data-extension-using-the-rest-api-e83c38213127?source=post_page-----0d9ba139c988---------------------------------------)

```
{  
  "name": "NewDE_Sendable",  
  "key": "",  
  "isSendable": true,  
  "sendableCustomObjectField": "Text",  
  "sendableSubscriberField": "_SubscriberKey",  
  "categoryId": 93800,  
  "fields": [  
    { "name": "Text", "type": "Text", "length": 50, "ordinal": 1, "IsPrimaryKey": true, "isNullable": false, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "EmailAddress", "type": "EmailAddress", "length": 254, "ordinal": 2, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Number", "type": "Number", "ordinal": 3, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Date", "type": "Date", "ordinal": 4, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Boolean", "type": "Boolean", "ordinal": 5, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Phone", "type": "Phone", "ordinal": 6, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Decimal", "type": "Decimal", "length": 25, "scale": 1, "ordinal": 7, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Locale", "type": "Locale", "ordinal": 8, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false}  
  ]  
}
```

### ③ Release Multiple Contacts Simultaneously from Wait Activities

This is an application of a feature introduced in the Winter ’24 release, which was covered in an article about **the Batch Event API that allows up to 100 contacts to enter a journey simultaneously**.

[## SFMC Tips #15 : Batch Event API Allows Entry of up to 100 Contacts in Journey Builder with a…

### In Salesforce Marketing Cloud’s Journey Builder, when entering contacts via API in commercial emails, previously, only…

medium.com](/@marketingcloudtips/batch-event-api-allows-entry-of-up-to-100-contacts-in-journey-builder-with-a-single-request-9655b12b72dd?source=post_page-----0d9ba139c988---------------------------------------)

It seems that now, from wait activities as well, up to 100 contacts can be forcibly released from waiting. The release notes provide an example: “For example, you can send a shipping confirmation when packages loaded onto a truck are shipped from the warehouse.” Previously, each contact had to be processed individually via API, but now batch processing is possible.

## ■ AMPscript — Related features

### ① Limit of RetrieveSalesforceObjects() Results Increased to 1,000 Rows

This update was announced in Spring ’24 but was postponed to the Summer ’24 launch due to becoming a limiting update.

An alert was also raised on the Trailblazers Community feed, **stating that as of June 21, 2024, the limit for retrieved rows will be restricted to 1,000**.

[## 🔈 Attention Marketing Cloud Admins | Salesforce Trailblazer Community

### 🔈 Attention Marketing Cloud Admins During the Summer '24 release , the AMPscript function RetrieveSalesforceObjects is…

trailhead.salesforce.com](https://trailhead.salesforce.com/trailblazer-community/feed/0D54V00007clRxLSAU?source=post_page-----0d9ba139c988---------------------------------------)

Salesforce advises using synchronized data extensions. While it’s unlikely that many people are using RetrieveSalesforceObjects(), those who are should be cautious of hitting this limit.

### ② Encode JWT Tokens Using RSA Signature

In the GetJWTByKeyName() function, you can now encode JSON Web Tokens using “RSA Signature”. Previously, only encoding using “HMAC Signature” was supported.

***How to:*** *Save a .asc file containing the RSA private key in “Key Management” in Marketing Cloud Setup. Once the key is saved, use the GetJWTByKeyName() function to encode the JWT.*

## ■ Email Studio— Related features

### ① Length Limitation of Selected Fields in Send Relationships

While announced in Spring ’24, this update will be applied in Summer ’24 due to its limiting nature. To improve performance, the length of fields selected in send relationships will be limited to 255 characters. It was initially set to 254 characters in Spring ’24, but it seems it was adjusted to 255 characters based on feedback.

The fields selected in send relationships refer to the following items. Since it’s unlikely that these would exceed 255 characters, it shouldn’t be a problem in your environment.

## ■ Package Manager — Related features

### ① Rapid Deployment of Retail Onboarding Journeys

This is a new deployment in the Package Manager. Although it’s unclear from where this can be deployed, presumably somewhere within the Package Manager, **it seems that packages specific to the “Retail Industry” will now be deployable, featuring journeys, content, automations, and landing pages**.

While there have been journey templates before, this seems like an expanded version. Honestly, I’ve never used journey templates at all.

It might be worth trying out, but be cautious because if it turns out to be unnecessary, it might be difficult to remove.

***Timing:*** *This feature will be available after July 1, 2024.*

### ② Interactive Forms to Collect More Subscriber Information

In addition to the journeys, content, automations, and landing pages described in 1, this update also applies to interactive forms. These are features where forms can be included within emails. It may not be limited to the “Retail Industry” in this case, but details are unclear.

***Timing:*** *This feature will be available after July 1, 2024.*

## ■ Security — Related features

### ① Fine-Tuning Permissions for SFTP Users

Currently, you can create up to 10 SFTP users in Marketing Cloud. **With the new Summer ’24 release, we are enhancing security by allowing various levels of access permissions for these SFTP users**.

![]()

*Note: These permissions are for SFTP users,* ***not individual Marketing Cloud users****.*

With this update, **you can assign specific access rights — viewing, editing, downloading, and uploading — at each top-level directory (down to subdirectories) for each SFTP user**.

![]()

You can also select a “home directory” as the default for each SFTP user. This means **each SFTP user will have access only to the selected directory and its subdirectories**.

*Note: Directories above the selected “home directory” will not be visible.*

![]()

*Release Timing: This feature is being rolled out gradually from May 2024, ahead of the Summer ’24 release period.*

## ■ App— Related features

### ① Complete Discontinuation of Social Studio on November 18, 2024

Social Studio will be discontinued on November 18, 2024. Access to Social Studio will no longer be available either when existing contracts expire or on November 18, 2024, whichever comes earlier. Customer data will be deleted 90 days later.

## Conclusion

Once again, this release will be rolled out between June 7th and June 28th, 2024. Please note that at the time of publishing this article, the features have not been released yet.

Furthermore, I anticipate that Salesforce will host new feature release briefings in the future. Once those are held, I intend to catch up from there and provide additional details.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
