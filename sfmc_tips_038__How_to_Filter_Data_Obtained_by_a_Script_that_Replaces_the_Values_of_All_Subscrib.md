# SFMC Tips #38 : How to Filter Data Obtained by a Script that Replaces the Values of All Subscribers

**Source:** https://medium.com/@marketingcloudtips/how-to-filter-data-obtained-by-a-script-that-replaces-the-values-of-all-subscribers-45300f420840

---

# SFMC Tips #38 : How to Filter Data Obtained by a Script that Replaces the Values of All Subscribers

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--45300f420840---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--45300f420840---------------------------------------)

3 min read

·

Apr 8, 2024

--

Photo by [Yusheng Deng](https://unsplash.com/@akiradeng?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I introduced a script to replace the values of “All Subscribers” in Salesforce Marketing Cloud (Subscriber Status, HTML Preferences, etc.). However, there were inquiries about **how to filter and replace only some of the data within a Data Extension**, so I will describe that in this article.

[## SFMC Tips #37 : Bulk Replacement of “Subscriber Status” for All Subscribers using SSJS

### Do you have a need to bulk replace all subscribers’ “Subscriber Status” with another status?

medium.com](/@marketingcloudtips/bulk-replacement-of-subscriber-status-for-all-subscribers-using-ssjs-1fe46b3bf4f5?source=post_page-----45300f420840---------------------------------------)

First, let’s prepare a Data Extension.

The values are stored in the Data Extension as shown below.

This time, **let’s try converting the “HTML Preference” to “Text” only when the value of the “HTML” item is “False”**. Currently, both “HTML Preferences” are “HTML” as shown below.

Left: AOR501 | Right: AOR502

**To create a filter based on the condition where the value of the “HTML” item is “False”**, set the filter as follows:

```
{Property:"HTML", SimpleOperator:"equals", Value:"False"}
```

**Insert this into** `"var data = dataExtension.Rows.Retrieve();"` . The entire script would look like this:

```
<script runat="server">  
Platform.Load("core", "1");  
  
// Specify the external key of the Data Extension  
var dataExtensionExternalKey = "1C99315A-F4A7-4F48-B06D-EAE9BD0A0FDF";  
  
// Initialize the Data Extension  
var dataExtension = DataExtension.Init(dataExtensionExternalKey)  
  
// Retrieve records by filtering the Data Extension  
var data = dataExtension.Rows.Retrieve({Property:"HTML", SimpleOperator:"equals", Value:"False"});  
  
// Loop through the records and change the subscriber status  
for (var i = 0; i < data.length; i++) {  
    var subscriberKey = data[i].Subscriberkey; // Get the SubscriberKey  
  
    var subscriber = {  
        SubscriberKey: subscriberKey,  
        EmailTypePreference: "Text" // Specify the HTML Preference (HTML/Text)  
    };  
  
    // Initialize the Subscriber object and update the subscriber status  
    var subObj = Subscriber.Init(subscriberKey);  
    var updateStatus = subObj.Update(subscriber);  
  
}  
</script>
```

*By the way, for* ***SimpleOperators*** *used in filters, there are the following:*

[## Salesforce Developers

### The SimpleOperators object contains operators to use when filtering data.

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/simpleoperators.html?source=post_page-----45300f420840---------------------------------------)

You can configure and execute this in the Automation Studio’s Script Activity to **convert the “HTML Preference” to “Text” only when the “HTML” item is “False”**.

![]()

Left: AOR501 (HTML: True) | Right: AOR502 (HTML: False)

*By the way, if you want to create conditions such as “any of multiple values” rather than a single condition, you can use* ***“IN” in SimpleOperators****, but you need to use an* ***“Array” for the Value****.*

```
{Property:"field", SimpleOperator:"IN", Value: ["A","B","C"]}
```

That’s all for this time.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
