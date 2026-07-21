# SFMC Tips #22 : Searching for Contact Key from Email Address in the Marketing Cloud App

**Source:** https://medium.com/@marketingcloudtips/searching-for-contact-key-from-email-address-in-the-marketing-cloud-app-0f026db10e4a

---

# SFMC Tips #22 : Searching for Contact Key from Email Address in the Marketing Cloud App

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0f026db10e4a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0f026db10e4a---------------------------------------)

7 min read

·

Feb 5, 2024

--

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

😏 Sudden, but marketers, have you ever faced such a dilemma?

*You are a marketer. One day, a complaint about the email delivery you are responsible for comes to customer service. The customer service representative, not well-versed in the operation of Salesforce Marketing Cloud, hands over only the email address to you and requests an investigation into the delivery content. Upon receiving it, you lament, “It would be easier to investigate if we knew the contact key, why start the investigation from the email address…”*

In Salesforce Marketing Cloud tools, **it is often more common to search using the contact key than the email address**.

To search for the contact key from the email address using standard features, you can start the search either from the “Search” button in the “All Subscribers” list in Email Studio or start the search from the search box in the “All Contacts” list in Contact Builder. However, it requires pressing the button several times to get to the contact key, causing a lot of stress.

Being able to quickly search for the contact key from the email address in such situations would expedite the handling of subsequent complaints.

This time, to solve such a problem, **I created a Marketing Cloud app that searches for the contact key from the email address**, and I would like to share it with you.

![]()

📝 This Marketing Cloud app, which I will introduce this time, is created using Cloudpages. By publishing Cloudpages, the app becomes publicly accessible, so **please limit the users who can access this app**.

Even if the URL of Cloudpages leaks externally, you can redirect to the Marketing Cloud login page when someone accesses that URL.

Regarding the authentication mechanism to limit these users, this article does not specifically touch on it, but **Mateusz Dąbrowski, a Salesforce MVP, has explained it meticulously and perfectly in his blog articles and videos**. It is truly wonderful content, and I also use this mechanism.

Please refer to it and try implementing it. Since some adjustments may be necessary for the code I am introducing, please work with someone who understands the code.

[## SFMC Cloud Page Apps | Mateusz Dąbrowski

### Learn how and when to create a custom application for your SFMC users using Cloud Pages, Code Resources and Installed…

mateuszdabrowski.pl](https://mateuszdabrowski.pl/docs/webinars/sfmc-webinar-cloud-page-apps/?source=post_page-----0f026db10e4a---------------------------------------)

For this article, we will use REST API.

Prepare the following three items introduced in my past article “How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester” in advance.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----0f026db10e4a---------------------------------------)

**1. Client ID  
2. Client Secret  
3. Authentication Base URL**

In the **Scope** of this API configuration, the following is required:  
**- Contacts > List and Subscribers > Read**

[## Salesforce Developers

### Review the permission ID, the path to the permission in Marketing Cloud, and the Installed Packages scope for each REST…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html?source=post_page-----0f026db10e4a---------------------------------------)

Now let’s get into the explanation.

## 🚀 Cloudpages Setup

Let’s proceed with the setup for Cloudpages.

1. After creating a new landing page in Cloudpages, insert the following code into an **HTML block**. For this case, content blocks other than HTML blocks do not require any configuration.

```
<br><br><b>Search for Contact Key from Email Address</b><br><br>  
  
%%[  
  SET @submittedEmail = RequestParameter('email')  
]%%  
  
<script runat="server">  
  Platform.Load("Core", "1");  
  
  // Authentication information required for accessing Salesforce Marketing Cloud REST API  
  var authPayload = {  
    "grant_type": "client_credentials",  
    "client_id": "******************", // Client ID  
    "client_secret": "******************" // Client Secret  
  };  
  
  // REST endpoint for obtaining the access token  
  var authUrl = "https://******************.auth.marketingcloudapis.com/v2/token"; // Authentication-based URL  
  var authResult = HTTP.Post(authUrl, 'application/json', Stringify(authPayload));  
  
  if (authResult.StatusCode == 200) {  
    var authResponse = Platform.Function.ParseJSON(authResult.Response[0]);  
    var accessToken = authResponse.access_token;  
    var restUrl = authResponse.rest_instance_url;  
  }  
  else {  
    // Throw an exception if an error occurs during access token retrieval  
    throw new Error("Error occurred while obtaining the access token.");  
  }  
  
  var submittedEmail = Variable.GetValue("@submittedEmail");  
  
  // REST API endpoint to search for contact key from the email address  
  var contactSearchUrl = restUrl + 'contacts/v1/addresses/email/search';  
  var contactSearchPayload = {  
    "ChannelAddressList": [submittedEmail],  
    "MaximumCount": 5  
  };  
  
  var contactSearchHeaders = ["Authorization"];  
  var contactSearchHeaderValues = ["Bearer " + accessToken];  
  var contactSearchResult = HTTP.Post(contactSearchUrl, 'application/json', Stringify(contactSearchPayload), contactSearchHeaders, contactSearchHeaderValues);  
  
  var responseEntities = Platform.Function.ParseJSON(contactSearchResult.Response[0]).channelAddressResponseEntities;  
  
  if (responseEntities && responseEntities.length > 0) {  
    for (var i = 0; i < responseEntities[0].contactKeyDetails.length; i++) {  
      var contactKey = responseEntities[0].contactKeyDetails[i].contactKey;  
      var createDate = responseEntities[0].contactKeyDetails[i].createDate;  
      Write("Contact Key: " + Stringify(contactKey) + "<br>");  
      Write("Creation Date: " + Stringify(createDate) + "<br><br>");  
    }  
  }  
  else {  
    // Message when no relevant data is found  
    Write("No matching data found.<br>");  
  }  
</script>  
  
<br>  
<form method="post">  
  <label for="email">Email Address:</label>  
  <input type="text" id="email" name="email" value="%%=v(@submittedEmail)=%%">  
  <br>  
  <input type="submit" value="Submit">    
</form>  
<br>  
<br>  
Reference: <a href="https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_contacts/retrieveContactKey.html">POST /contacts/v1/addresses/email/search</a>
```

*\* Modifications required in this code:*

***- Client ID  
- Client Secret  
- Authentication Base URL***

2. After completing the HTML block configuration, **“Save” and “Publish”**.

3. Once the publishing is complete, copy the URL of the Cloudpages.

4. This concludes the Cloudpages setup. After this, you will move on to the configuration of the installed package, but as the app is already launched, try clicking on the Cloudpages URL.

5. Enter an existing email address and click the “Submit” button.

![]()

6. **Up to 5 contact keys with the same email address will be displayed**.

*\* In the code, you can determine the maximum number of displayed contacts (MaximumCount), choosing between 1 and 5. Even if set to 100, the maximum is still 5. The display order is from the most recently created to the oldest.*

![]()

## 🚀 Configuration of Installed Package

Next is the configuration of the installed package. By doing this, it will be visible on the AppExchange tab, similar to Query Studio.

1. In Marketing Cloud Setup, select **“Installed Packages”** and click the “New” button.

2. Decide on the name for the new package definition. This won’t be the displayed name. Afterward, click “Save”.

![]()

3.. Click **“Add Component”**.

4. In the component type selection screen, choose **“Marketing Cloud App”** and click “Next”.

![]()

5. Finally, determine the “Display Name”. **Input the copied Cloudpages URL into both “Login Endpoint” and “Logout Endpoint”**. It’s acceptable for both URLs to be the same. After that, click “Save”.

*\* Once the save is complete,* ***log out and log back in****.*

![]()

6. After logging in, check AppExchange for display confirmation, and click on the display name.

![]()

7. In this case, the display name I assigned, “Contact Search”, becomes the logo, and the search screen is displayed.

![]()

With this, the process is complete. 🎉

## Conclusion

As mentioned earlier, the Cloudpages created this time will be publicly accessible, making them viewable by anyone. Except for creating them temporarily for testing purposes, **when using them in production, be sure to implement an authentication mechanism to restrict access to specific users only**. 🚨

Additionally, **Zuzanna Jarczynska, a Salesforce MVP, provides a convenient tool called “DE Search” that allows for easy searching of data extension folder paths**. It is introduced in the following blog, so give it a try. This tool is also very handy.

[## Simple Marketing Cloud App hosted on a CloudPage

### DISCLAIMER: The Marketing Cloud App component has been designed for use with externally hosted apps. Use any…

sfmarketing.cloud](https://sfmarketing.cloud/2020/04/15/simple-marketing-cloud-app-hosted-on-a-cloudpage/?source=post_page-----0f026db10e4a---------------------------------------)

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
