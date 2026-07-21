# SFMC Tips #37 : Bulk Replacement of “Subscriber Status” for All Subscribers using SSJS

**Source:** https://medium.com/@marketingcloudtips/bulk-replacement-of-subscriber-status-for-all-subscribers-using-ssjs-1fe46b3bf4f5

---

# SFMC Tips #37 : Bulk Replacement of “Subscriber Status” for All Subscribers using SSJS

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1fe46b3bf4f5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1fe46b3bf4f5---------------------------------------)

4 min read

·

Apr 4, 2024

--

Photo by [Spencer Davis](https://unsplash.com/@spencerdavis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Do you have a need to bulk replace all subscribers’ “Subscriber Status” with another status?

For instance, I previously wrote an article about subscribers with a “Held” status. As explained there, you might encounter cases **where upon changing a subscriber’s email address, you’d want to switch their “Hold” status to “Active” in bulk**.

[## SFMC Tips #34 : Verification of Actions After Email Address Change and Relationship with “Held”…

### In Salesforce Marketing Cloud, the “Held” status refers to a status where, after one or several bounces resulting from…

medium.com](/@marketingcloudtips/verification-of-actions-after-email-address-change-and-relationship-with-held-status-7b25d282a9cb?source=post_page-----1fe46b3bf4f5---------------------------------------)

## ■ Bulk Replacement of “Subscriber Status”

In such scenarios, while you could handle this by importing to all subscriber lists, **you can easily achieve this through the following script configured within Automation Studio’s Script Activity**.

![]()

```
<script runat="server">  
Platform.Load("core", "1");  
  
// Specify the "External Key" of the Data Extension  
var dataExtensionExternalKey = "1C99315A-F4A7-4F48-B06D-EAE9BD0A0FDF";  
  
// Initialize the Data Extension  
var dataExtension = DataExtension.Init(dataExtensionExternalKey);  
  
// Retrieve all records from the Data Extension (without any filters)  
var data = dataExtension.Rows.Retrieve();  
  
// Loop through records to change subscriber status  
for (var i = 0; i < data.length; i++) {  
    var subscriberKey = data[i].Subscriberkey; // Get "SubscriberKey"  
  
    var subscriber = {  
        SubscriberKey: subscriberKey,  
        Status: "Active" // Specify the status (e.g., to replace with "Active")  
    };  
  
    // Initialize Subscriber object and update subscriber status  
    var subObj = Subscriber.Init(subscriberKey);  
    var updateStatus = subObj.Update(subscriber);  
  
}  
</script>
```

The only things you need to modify within this code are:

**■ “External Key” of the Data Extension   
■ “Name of the subscriber key field” in the Data Extension**

- The above assumes that the subscriber key field name is “Subscriberkey”. In the part “var subscriberKey = data[i].XXXXX”, please change “XXXXX” to match the field name in your data extension.

*\*Note that* ***the subscriber key field name is case-sensitive****. Even if there is a mistake in the description, a script error will not occur.*

- The above example replaces the status with “Active”. If you want to replace it with “Unsubscribed”, change “Active” to “Unsubscribed”. If you forget the final “d” and write “Unsubscribe”, the script will result in an error.
- The script will succeed with “Bounced” as well, but the status will be set to “Active” instead of “Bounced”. On the other hand, **if you use “Held”, the status will change to held**. As an example of using “Held”, if you are switching from another MA tool and have hard bounce subscribers, you can replace their status with this.
- **Since the upper limit of Rows.Retrieve() is 2,500 records**, when processing a large amount of data, please either use a random data extension to reduce it to around 2,000 records and process it in batches, or use the import activity to replace the status in bulk.
- As a guideline for the script processing time, **it takes about 1 to 2 minutes for 100 records**. Although the processing method is simpler compared to import, there is a possibility of a timeout (30 minutes) when processing a large amount of data.
- This example retrieves **“all” records** from the Data Extension without using any filters. I have created an example of using filters in a separate article. Please refer to the following.

[## SFMC Tips #38 : How to Filter Data Obtained by a Script that Replaces the Values of All Subscribers

### In the previous article, I introduced a script to replace the values of “All Subscribers” in Salesforce Marketing Cloud…

medium.com](/@marketingcloudtips/how-to-filter-data-obtained-by-a-script-that-replaces-the-values-of-all-subscribers-45300f420840?source=post_page-----1fe46b3bf4f5---------------------------------------)

You can obtain the “External Key” of the Data Extension from the following location:

With this script, **you can replace the status of all subscribers without the need for SFTP**.

*When working with such Script Activities, it’s recommended to initially perform testing with a small amount of test data to ensure proper functionality before executing with live data.*

## ■ Bulk Replacement of “HTML Preference”

Additionally, it’s possible to **bulk replace the “HTML Preference” of multiple subscribers stored in a Data Extension from default “HTML” to “TEXT” or vice versa**.

*In this case, you’ll use “****EmailTypePreference****” instead of “Status”.*

```
<script runat="server">  
Platform.Load("core", "1");  
  
// Specify the External Key of the Data Extension  
var dataExtensionExternalKey = "1C99315A-F4A7-4F48-B06D-EAE9BD0A0FDF";  
  
// Initialize the Data Extension  
var dataExtension = DataExtension.Init(dataExtensionExternalKey);  
  
// Retrieve all records from the Data Extension  
var data = dataExtension.Rows.Retrieve();  
  
// Loop through records to change subscriber preference  
for (var i = 0; i < data.length; i++) {  
    var subscriberKey = data[i].Subscriberkey; // Get SubscriberKey  
  
    var subscriber = {  
        SubscriberKey: subscriberKey,  
        EmailTypePreference: "Text" // Specify HTML Preference (HTML/Text)  
    };  
  
    // Initialize Subscriber object and update preference  
    var subObj = Subscriber.Init(subscriberKey);  
    var updateStatus = subObj.Update(subscriber);  
  
}  
</script>
```

*By the way, switching the “HTML Preference” to text means that henceforth, those subscribers will* ***only receive the “Plain Text” version of messages during transmission as Multi-part MIME****.*

If you want to update both “Status” and “HTML Preference” simultaneously, set it up like this (for “Active” and “HTML”):

```
var subscriber = {  
    SubscriberKey: subscriberKey,  
    Status: "Active", // 👈️ Don't forget this comma!  
    EmailTypePreference: "HTML"   
};
```

If updates aren’t reflected throughout, ensure the following two things are correct:

**■ “External Key” of the Data Extension   
■ “Name of the subscriber key field” in the Data Extension**

That concludes this explanation.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
