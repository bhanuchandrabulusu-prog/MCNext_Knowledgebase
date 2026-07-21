# SFMC Tips #18 : Automatically Sending Another Email When Clicking a Link in an Email Sent from…

**Source:** https://medium.com/@marketingcloudtips/automatically-sending-another-email-when-clicking-a-link-in-an-email-sent-from-marketing-cloud-23c62e4799d4

---

# SFMC Tips #18 : Automatically Sending Another Email When Clicking a Link in an Email Sent from Marketing Cloud

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--23c62e4799d4---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--23c62e4799d4---------------------------------------)

8 min read

·

Jan 22, 2024

--

Photo by [Adeyemi Emmanuel Abebayo](https://unsplash.com/@adeyemiemmanuel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article explains the mechanism of automatically sending another email when clicking a link in an email sent from Salesforce Marketing Cloud. Specifically, the scenario considered is as follows:

*Salesforce Marketing Cloud sends an initial email containing a link to a webpage with details about a certain product. However, simply viewing the description on this website is deemed insufficient, and there is a desire to send a follow-up email.*

*Certainly, it is possible to use the “Click” data view and the SQL Query Activity in Automation Studio to extract data from contacts who clicked the link, store it in a data extension, and then send a follow-up email the next morning. However,* ***the plan is to send the follow-up email at the “hot” timing (15 minutes after clicking the link) without letting the customer’s interest cool down****.*

Such post-click tracking scenarios may sometimes evoke discomfort in customers, making them feel like they are being tracked rather than appreciating the follow-up. Therefore, careful attention is required regarding timing and other factors.

Nevertheless, learning how to implement this can broaden the possibilities of what can be done with Salesforce Marketing Cloud, sparking various ideas for the future. Please take this opportunity to at least check the mechanism.

By the way, in terms of “Learning” about Salesforce Marketing Cloud, there are various learning resources available worldwide. However, this time, I will utilize these resources to practice the scenario. Take this chance to join the learning community.

**■ Configuring Cloudpages to Send Another Email (By Cameron Robert)**

**■ Passing AMPscript Variable Values to Server-Side JavaScript (By Zuzanna Jarczynska)**

[## Passing variable values between AMPscript, Server-Side JavaScript and Client-Side JavaScript

### A lot of advanced use cases related to building dynamic, highly personalised CloudPages in Salesforce Marketing Cloud…

sfmarketing.cloud](https://sfmarketing.cloud/2022/09/06/passing-variable-values-between-ampscript-server-side-javascript-and-client-side-javascript/?source=post_page-----23c62e4799d4---------------------------------------)

This time, the scenario is a combination of the above two learning resources.

\*While Cameron Robert’s video explains the main parts of the implementation in order, since the “Subscriber Key” and “Email Address” are fixed values, I have referenced Zuzanna Jarczynska’s article to dynamically retrieve subscriber information.

For this article, we will use REST API.

Prepare the following three items introduced in my past article “How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester” in advance.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----23c62e4799d4---------------------------------------)

**1. Client ID  
2. Client Secret  
3. Authentication Base URL**

In the **Scope** of this API configuration, the following two are required:  
**- Automation > Journeys > Read  
- Contacts > List and Subscribers > Read**

[## Salesforce Developers

### Review the permission ID, the path to the permission in Marketing Cloud, and the Installed Packages scope for each REST…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html?source=post_page-----23c62e4799d4---------------------------------------)

Now let’s get into the explanation.

※ In the following, the email sending 15 minutes later is referred to as “triggered send”.

### Step 1: Create an entry source for triggered send

For this task, please create a sendable data extension as an entry source for triggered send, following the format outlined below.

**- Subscriber Key: Id   
- Email Address: Email   
- Last Name: LastName   
- Record Creation Date: EventDate**

The primary key is not necessary this time. Also, set “Current Date” as the default for EventDate to automatically insert the “Record Creation Date”.

### Step 2: Configure Journey Builder for the triggered send

Select “**API event**” as the entry source. And click on “**create an event**” and set the entry source created earlier.

Prepare the email for the triggered send. Here, %%LastName%% is included as a personalized string.

Set up a 15-minute Wait Activity on the Journey Canvas, followed by an Email Activity.

- To ensure that only one email is sent per customer, set the entry condition to “**No re-entry**” in the journey settings.
- If you prefer not to send the trigger email during the late night hours, configure the “**Delivery Window**”.

Once all these settings are completed, **Activate** the journey.

After activation, click on the entry source, and the “Event Definition Key” will be displayed. Copy this key.

### Step 3: Configure Cloudpages

Create a new landing page in Cloudpages.

Enter the following code into an **HTML block**. If you want to learn how to write this code, use the two learning resources mentioned earlier.

```
%%[  
    var @emailAddress  
    var @subscriberKey  
    var @lastName  
  
    /* Cannot be tested in "Preview & Test" as it uses JB Entry Source attributes */  
    set @emailAddress = AttributeValue("Email")    
    set @subscriberKey = AttributeValue("Id")    
    set @lastName = AttributeValue("LastName")   
]%%  
  
<script runat="server">  
    Platform.Load("Core", "1.1.1");  
  
    try {  
        // Setting up authentication information  
        var payload = {  
            "grant_type": "client_credentials",  
            "client_id": "******************", // Client ID  
            "client_secret": "******************" // Client Secret  
        };  
        var authUrl = "https://******************.auth.marketingcloudapis.com/v2/token"; // Authentication-based URL  
        var result = HTTP.Post(authUrl, 'application/json', Stringify(payload));  
  
        // Obtaining access token  
        if (result.StatusCode == 200) {  
            var responseJson = Platform.Function.ParseJSON(result.Response[0]);  
            var accessToken = responseJson.access_token;  
            var restUrl = responseJson.rest_instance_url;  
        } else {  
            throw new Error("An error occurred while obtaining the access token");  
        }  
  
        var emailAddress = Variable.GetValue("@emailAddress");  
        var subscriberKey = Variable.GetValue("@subscriberKey");  
        var lastName = Variable.GetValue("@lastName");  
  
        // Setting up payload for Journey  
        var journeyPayload = {  
            "ContactKey": subscriberKey,  
            "EventDefinitionKey": "APIEvent-******************", // Entry Source Event Definition Key  
            "Data": {  
                "id": subscriberKey,  
                "email": emailAddress,  
                "lastname": lastName  
            }  
        };  
  
        // Firing the event; in Japan, you need to use "application/json; charset=UTF-8"  
        var fireEvent = HTTP.Post(restUrl + "interaction/v1/events", 'application/json', Stringify(journeyPayload), ["Authorization"], ["Bearer " + accessToken]);  
        Write(Stringify(fireEvent));  
  
    } catch (error) {  
        Write('Message: ' + error);  
    }  
</script>  
  
%%=Redirect('https://www.salesforce.com/ap/products/marketing-personalization/')=%%
```

Please note the following in this code:

\*The four items that need to be modified in this code are:

**- Client ID  
- Client Secret  
- Authentication Base URL  
- Entry source Event Definition Key**

*\*Since we are using the attributes of the Journey Builder entry source this time, testing* ***cannot be done in the “Preview & Test” feature of Email Studio****. Please send an actual email to yourself in Journey Builder and test it.*

*\*****In Japan****, when using* ***interaction/v1/events****, you need to change the Content-Type header to “****application/json; charset=UTF-8****” instead of “application/json” when using this.*

Once these settings are complete, **Publish** Cloudpages. An error message will be displayed during preview, but ignore it.

### Step 4: Create an email containing the link to the Cloudpages

This step is the creation procedure when including a regular Cloudpages link.

In addition to the triggered send email created earlier, include a link to the Cloudpages in a regular email to be sent in advance. I have embedded it in a button as shown below.

**Important Notes**

If you want to ensure that the values are reliably available on the CloudPage, explicitly pass them as arguments to the `CloudPagesURL()` function.

```
%%=RedirectTo(CloudPagesURL(  
  6576,  
  "id", AttributeValue("Id"),  
  "email", AttributeValue("Email"),  
  "lastname", AttributeValue("LastName")  
))=%%
```

This approach ensures that the values are included in the generated CloudPage URL and can be securely retrieved on the CloudPage side.

### Step 5: Send the email created in Step 4 using Journey Builder

This step is omitted, but include the following in the entry source items:

**- Subscriber Key: Id   
- Email Address: Email   
- Last Name: LastName**

### Step 6: Click the Cloudpages link in the received email

Click the link once.

![]()

The destination of this link is a webpage introducing Salesforce Marketing Cloud Personalization, and the email triggered afterwards contains content that follows up on this.

### Step 7: Check the triggered send journey

After clicking the link, check the canvas of the triggered send journey, and you will see that one subscriber has moved to the 15-minute wait activity.

As long as “Re-entry” is set in the journey settings, even if clicked multiple times, it will enter only once.

### Step 8: Check the triggered send entry source DE

Check the sendable data extension created for the entry source, and you will find one record created.

### Step 9: Check the email triggered 15 minutes later

After 15 minutes, you should receive the email. As expected, it should be sent with %%LastName%% containing the “Last Name”.

That concludes the steps.

Javier De Mauri, an email marketing expert, pointed out that it would be better to remind everyone of the concerns about clicks caused by “clickbots”, so I would like to add this. The structure of this article is based on the premise that the fact that the customer clicked to send the message should not be revealed to the customer in the first place, but there is also a concern that the message may be sent without the customer clicking. You should give even more consideration to ensuring that your message does not create any sense of suspiciousness, no matter when or to whom it is delivered. I apologize for not mentioning this point.

**Filter anti-spam software clicks and clickbots from Marketing Cloud Tracking Data**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000381730&type=1&source=post_page-----23c62e4799d4---------------------------------------)

## Conclusion

This mechanism is also possible by combining it with Cloudpages. As mentioned earlier, be careful when choosing the moments to use it, as being too persistent in chasing customers can make them feel uncomfortable.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
