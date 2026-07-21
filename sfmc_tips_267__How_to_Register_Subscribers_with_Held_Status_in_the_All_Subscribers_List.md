# SFMC Tips #267 : How to Register Subscribers with Held Status in the All Subscribers List

**Source:** https://medium.com/@marketingcloudtips/how-to-register-subscribers-with-held-status-in-the-all-subscribers-list-64c8c0823837

---

# SFMC Tips #267 : How to Register Subscribers with Held Status in the All Subscribers List

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--64c8c0823837---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--64c8c0823837---------------------------------------)

3 min read

·

Mar 13, 2026

--

Photo by [Eugene Golovesov](https://unsplash.com/@eugene_golovesov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Engagement**, subscribers with the **Held** status cannot normally be created or updated using the standard import functionality.

> *Note: If* ***Held*** *or* ***Bounced*** *statuses are imported using* ***Automation Studio****, an error occurs because they are treated as* ***invalid context statuses****.*

However, by using the following script, it is possible to register subscribers with the **Held** status in **All Subscribers**.

```
<script runat="server">  
Platform.Load("core", "1");  
  
var dataExtensionExternalKey = "CD3226AE-FA46-4278-AF4C-5B3B1D275803";   // DE external key  
var de = DataExtension.Init(dataExtensionExternalKey);  
var rows = de.Rows.Retrieve();  
  
var prox = new Script.Util.WSProxy();  
  
for (var i = 0; i < rows.length; i++) {  
    var subscriberKey = rows[i]["SubscriberKey"];   // DE field name  
    var emailAddress  = rows[i]["EmailAddress"];    // DE field name  
  
    if (!subscriberKey || !emailAddress) {  
        continue;  
    }  
  
    var subscriberObj = {  
        SubscriberKey: subscriberKey,  
        EmailAddress: emailAddress,  
        Status: "Held"  
    };  
  
    var options = {  
        SaveOptions: [  
            {  
                PropertyName: "*",  
                SaveAction: "UpdateAdd"  
            }  
        ]  
    };  
  
    try {  
        var result = prox.updateItem("Subscriber", subscriberObj, options);  
        Write("<br>OK: " + Stringify(result));  
    } catch (e) {  
        Write("<br>ERROR: " + Stringify(e));  
    }  
}  
</script>
```

The only three items you need to change are the following:

- **DE external key**
- **DE field name: SubscriberKey**
- **DE field name: EmailAddress**

`UpdateAdd` means **Upsert**, which means **update if the record exists, and add if it does not exist**.

Therefore, the processing flow works as follows.

## Processing Logic

Check **All Subscribers** using **SubscriberKey** as the key.

- If the target subscriber exists  
  → **Update**
- If the target subscriber does not exist  
  → **Add**

Note that **SubscriberKey** and **EmailAddress** are required fields.  
Prepare the **Data Extension** in the following format.

When the script is executed, the subscriber will be imported with the **Held** status.

![]()

## Important Notes When Using This Script

If you process a large number of records, this code requires some caution.

First, there is a limit on the number of records that can be retrieved using `Rows.Retrieve()`, which is **up to 2,500 records**.

In addition, since this script processes records by **calling the API one by one**, the processing time increases as the number of records increases.

Therefore, the following risks may occur when processing large volumes of data:

- It may take a long time for the processing to complete.
- It may approach the **Automation Studio 30-minute limit (auto-kill)**.
- The process may stop partway through.

However, because the records are processed **one by one in sequence**, even if the process stops midway, the records that were processed before the stop will already be registered.

In practice, **2,500 records is close to the limit of what can be processed within 30 minutes**.

For this reason, if you have many records, it is recommended to **split the data into smaller batches**, such as executing about **2,000 records at a time** using a random Data Extension or similar approach.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
