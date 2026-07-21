# SFMC Tips #57 : Marketing Cloud App to Release Contacts from Wait Activity via API

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-app-to-release-contacts-from-wait-activity-via-api-d5c787070819

---

# SFMC Tips #57 : Marketing Cloud App to Release Contacts from Wait Activity via API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d5c787070819---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d5c787070819---------------------------------------)

9 min read

·

Sep 23, 2024

--

Photo by [Joe Roberts](https://unsplash.com/@iamjoeroberts?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Journey Builder, there is a type of wait activity called “**Wait Until Event**”. This activity holds contacts in a waiting state, and by using the REST API to send a signal, you can release them from the wait and allow them to move to the next step. 🏃

The wait period on this activity can be set as follows:

- **1 to 10 days**
- **1 to 10 weeks**
- **1 to 10 months**

The minimum wait time is 1 day, and the maximum is 10 months. If no signal is received within the set period, the contact will proceed down the No Event path.

Based on the mechanism of this wait activity, I wanted to experiment with whether it would be possible to trigger this REST API easily by just entering a contact key.

While Marketing Cloud is typically seen as a bulk email delivery tool that uses send lists, if you can trigger sends by simply entering a contact key, it opens up the possibility for more personalized, timely email sends.

So, I created an **“Experimental” Marketing Cloud app** and would like to share it with you. It’s easy for anyone to create, so please give it a try!

![]()

Let’s go through the details below.

## Security Considerations

This Marketing Cloud app, which I will introduce this time, is created using Cloudpages. By publishing Cloudpages, the app becomes publicly accessible, so **please limit the users who can access this app**.

Even if the URL of Cloudpages leaks externally, you can redirect to the Marketing Cloud login page when someone accesses that URL.

Regarding the authentication mechanism to limit these users, this article does not specifically touch on it, but **Mateusz Dąbrowski, a Salesforce MVP, has explained it meticulously and perfectly in his blog articles and videos**. It is truly wonderful content, and I also use this mechanism.

Please refer to it and try implementing it. Since some adjustments may be necessary for the code I am introducing, please work with someone who understands the code.

[## SFMC Cloud Page Apps | Mateusz Dąbrowski

### Learn how and when to create a custom application for your SFMC users using Cloud Pages, Code Resources and Installed…

mateuszdabrowski.pl](https://mateuszdabrowski.pl/docs/webinars/sfmc-webinar-cloud-page-apps/?source=post_page-----d5c787070819---------------------------------------)

## Setting the Stage

For this article, we will use REST API.

Prepare the following three items introduced in my past article “How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester” in advance.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----d5c787070819---------------------------------------)

**1. Client ID  
2. Client Secret  
3. Authentication Base URL**

In the **Scope** of this API configuration, the following is required:

- **AUTOMATION — Journeys — Read**
- **CONTACTS — List and Subscribers — Read**

[## Salesforce Developers

### REST API Permission IDs and Scopes

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_rest_permission_scopes/rest-permissions-and-scopes.html?source=post_page-----d5c787070819---------------------------------------)

Before we dive into building the app, we need to create a data extension in Email Studio and set up the “Wait Until Event” activity in Journey Builder. I’ll walk you through the process here.

## **Creating the Data Extension**

1. First, let’s create the data extension that will receive the REST API data. Create a “**Standard**” data extension and name it “**WaitUntilEvent**”. Set it to “**Sendable**”.

2. For the fields, having just an “**Id**” field is sufficient. **Don’t set it as a “Primary Key”** so that duplicate entries are allowed.

## **Setting Up Journey Builder**

Next, let’s configure Journey Builder.

1. I’ll skip the detailed setup of Journey Builder, but after placing the entry source and email activity, add the “**Wait Until Event**” activity and click on it.

2. Click the “**Create New**” button.

3. Give the API event a name that’s easy to recognize and make a note of the “**Event Definition Key**” that appears. You’ll need it later when setting up CloudPages. The part from “**APIEvent-\*\*\*\*\*\*\*\*\*\*\*\*\*\***” onward is required.

4. Next, in the data extension selection screen, choose the sendable data extension you created earlier.

5. After selecting the data extension, set the maximum wait period. As mentioned earlier, the maximum wait period for the “Wait Until Event” activity can be chosen from the following options. If no signal is received via the REST API during this period, the contact will proceed down the lower path in the flow.

- **1 to 10 days**
- **1 to 10 weeks**
- **1 to 10 months**

6. For this example, I set it to **the maximum period of 10 months**. This means you will need to perform some action within 10 months. After setting the wait period, complete the activity setup.

7. After confirming that all settings, including the email activity, are complete, activate the journey.

8. Once the journey is activated, you should see contacts flowing into the “Wait Until Event” activity and entering a waiting state.

9. At this point, the contacts are in a wait state for up to 10 months, as if they are “**ready to launch**” their emails.

*\* Some of you may be wondering, “The data extension we created this time only has an ‘Id’ field, so how should we handle the ‘Default Email Address’ in the journey settings?” However, this data extension was created solely for the purpose of ending the wait, so it doesn’t matter whether you use the email address from the entry source or the email address of all subscribers. That said, considering the 10-month time span, it’s generally better to use the email address of all subscribers.*

## **Setting Up CloudPages**

Next, let’s set up CloudPages.

1. Create a new CloudPages landing page, and copy the following code into an HTML block. You don’t need any content blocks other than the HTML block.

```
<h3>Enter Contact Key to Trigger Wait Activity</h3>  
  
%%[  
  SET @submittedContactKey = RequestParameter('contactKey')  
    
  IF NOT EMPTY(@submittedContactKey) THEN  
    SET @lookupValue = Lookup("WaitUntilEvent", "Id", "Id", @submittedContactKey) /* Data extension name, Contact Key field name */  
    
    IF NOT EMPTY(@lookupValue) THEN  
      SET @apiTriggerMessage = "Already processed"  
    ELSE  
      SET @apiTriggerMessage = "Process completed"  
    ENDIF  
  ELSE  
    SET @apiTriggerMessage = "" /* Set to empty initially */  
  ENDIF  
]%%  
  
<script runat="server">  
  Platform.Load("Core", "1");  
  var submittedContactKey = Variable.GetValue("@submittedContactKey");  
  
  var authPayload = {  
    "grant_type": "client_credentials",  
    "client_id": "************************", // Client ID  
    "client_secret": "************************" // Client Secret  
  };  
  
  var authUrl = "https://************************.auth.marketingcloudapis.com/v2/token"; // Auth Base URL  
  var authResult = HTTP.Post(authUrl, 'application/json', Stringify(authPayload));  
  
  if (authResult.StatusCode == 200) {  
    var authResponse = Platform.Function.ParseJSON(authResult.Response[0]);  
    var accessToken = authResponse.access_token;  
    var restUrl = authResponse.rest_instance_url;  
  } else {  
    throw new Error("Error obtaining access token.");  
  }  
  
  var apiTriggerMessage = Variable.GetValue("@apiTriggerMessage");  
  
  // Call API only if ContactKey is not already in the data extension  
  if (submittedContactKey && apiTriggerMessage == "Process completed") {  
    var validateContactKeyUrl = restUrl + '/interaction/v1/events';  
    var validateContactKeyPayload = {  
      "ContactKey": submittedContactKey,  
      "EventDefinitionKey": "APIEvent-************************", // Event Definition Key  
      "Data": { "id": submittedContactKey } // Contact Key field name  
    };  
    var validateContactKeyHeaders = ["Authorization"];  
    var validateContactKeyHeaderValues = ["Bearer " + accessToken];  
    var validateContactKeyResult = HTTP.Post(validateContactKeyUrl, 'application/json', Stringify(validateContactKeyPayload), validateContactKeyHeaders, validateContactKeyHeaderValues);  
  }  
</script>  
  
<br>  
  
<form method="post">  
  <label for="contactKey">Contact Key:</label>  
  <input type="text" id="contactKey" name="contactKey" value="%%=v(@submittedContactKey)=%%">  
  <br><br>  
  <input type="submit" value="Submit">  
</form>  
  
<br>  
<p>%%=v(@apiTriggerMessage)=%%</p>  
<br>
```

### **Key points to adjust in the code:**

- **Data extension name (if changed)**
- **Contact Key field name in the data extension (if changed)**
- **Client ID**
- **Client Secret**
- **Auth Base URL**
- **Event Definition Key (APIEvent-\*\*\*\*\*\*\*\*\*\*\*\*\*\*)**

2. Once the **HTML block** is set up, save and publish it.

3. After publishing, copy and save the CloudPages URL. You’ll need this later when setting up the installed package.

4. That’s it for setting up CloudPages. The app should now be functional, so click on the CloudPages URL.

5. Enter the contact key currently in the wait state and click “**Submit**”.

![]()

6. If you see the message “**Process completed**”, the trigger was successful.

![]()

7. When you check the journey, you should see that one contact has progressed to the email activity.

8. Let’s also check the data extension. As shown below, you can confirm that one contact has been stored.

9. If the process has already been completed, the message “**Already processed**” will be displayed, and no duplicate processing will occur. This prevents the API from being called multiple times for the same contact.

![]()

## **Setting Up Installed Packages**

Lastly, let’s configure the installed package. By doing this, you can display it under the AppExchange tab, similar to Query Studio.

1. In Marketing Cloud Setup, select “**Installed Packages**” and click the “**New**” button.

2. Define a name for the new package. This is not the name that will be displayed. After that, click “**Save**”.

3. Click “**Add Component**”.

4. On the component type selection screen, choose “**Marketing Cloud App**” and click “Next”.

![]()

5. Finally, decide on the “Display Name”. Then, enter the CloudPages URL you copied earlier in both the “Login Endpoint” and “Logout Endpoint”. It’s fine to use the same URL for both. Afterward, click “Save”.

*\** ***After saving, log out and then log back in****.*

![]()

6. After logging in, check the AppExchange tab to confirm that the display name appears. Click on the display name.

7. In this case, I named it “**Wait Until Event**”, and the screen to trigger contacts appeared with the logo displayed.

![]()

And that’s it!

As I mentioned earlier, the CloudPages we created here is publicly accessible, meaning anyone can view it. If you’re just testing, this might be fine temporarily, but for production use, make sure to implement authentication to restrict access to specific users only.

That concludes this guide!

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
