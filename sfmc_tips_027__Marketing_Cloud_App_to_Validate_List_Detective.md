# SFMC Tips #27 : Marketing Cloud App to Validate List Detective

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-app-to-validate-list-detective-ab299d318492

---

# SFMC Tips #27 : Marketing Cloud App to Validate List Detective

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ab299d318492---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ab299d318492---------------------------------------)

7 min read

·

Feb 19, 2024

--

Photo by [Josh Hild](https://unsplash.com/@joshhild?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

I previously wrote an article about **the mechanism to validate email addresses using the List Detective API**.

[## SFMC Tips #25 : Self-Searching for Email Addresses Targeted by List Detective

### The List Detective feature enables Salesforce Marketing Cloud to proactively exclude email addresses identified as…

medium.com](/@marketingcloudtips/self-searching-for-email-addresses-targeted-by-list-detective-1689c90ec1b7?source=post_page-----ab299d318492---------------------------------------)

This time, I have replicated that mechanism as a **Marketing Cloud App**, and I would like to introduce it to you.

1. **When sending emails using Data Extensions.**
2. **When importing into Lists such as all subscriber lists.   
   (\* Importing into Data Extensions is not included.)**

This feature allows avoiding sending to email addresses that may potentially cause delivery issues and helps mitigate the risk of IP reputation degradation.

Typically, marketers or IT departments would need to manually exclude these email addresses at the front end. However, when using Salesforce Marketing Cloud for email sending, **it automatically handles the exclusion in the backend**, making it a very convenient feature.

However, since the target list of this List Detective is not publicly disclosed, and the logic is not revealed, there is a need for a mechanism to investigate whether the email addresses unintentionally fall under List Detective scrutiny.

Normally, you can inquire with Salesforce Technical Support to investigate if an email address is a List Detective target. However, **the app introduced this time allows you to perform this investigation on your own**.

📝 This Marketing Cloud app, which I will introduce this time, is created using Cloudpages. By publishing Cloudpages, the app becomes publicly accessible, so **please limit the users who can access this app**.

Even if the URL of Cloudpages leaks externally, you can redirect to the Marketing Cloud login page when someone accesses that URL.

Regarding the authentication mechanism to limit these users, this article does not specifically touch on it, but **Mateusz Dąbrowski, a Salesforce MVP, has explained it meticulously and perfectly in his blog articles and videos**. It is truly wonderful content, and I also use this mechanism.

Please refer to it and try implementing it. Since some adjustments may be necessary for the code I am introducing, please work with someone who understands the code.

[## SFMC Cloud Page Apps | Mateusz Dąbrowski

### Learn how and when to create a custom application for your SFMC users using Cloud Pages, Code Resources and Installed…

mateuszdabrowski.pl](https://mateuszdabrowski.pl/docs/webinars/sfmc-webinar-cloud-page-apps/?source=post_page-----ab299d318492---------------------------------------)

For this article, we will use REST API.

Prepare the following three items introduced in my past article “How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester” in advance.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----ab299d318492---------------------------------------)

**1. Client ID  
2. Client Secret  
3. Authentication Base URL**

In the **Scope** of this API configuration, the following is required:  
**- CHANNELS — Email — Read**

[## Salesforce Developers

### Review the permission ID, the path to the permission in Marketing Cloud, and the Installed Packages scope for each REST…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html?source=post_page-----ab299d318492---------------------------------------)

Now let’s get into the explanation.

## 🚀 Cloudpages Setup

Let’s proceed with the setup for Cloudpages.

1. After creating a new landing page in Cloudpages, insert the following code into an **HTML block**. For this case, content blocks other than HTML blocks do not require any configuration.

```
<br><br><b>Email Validation</b> (Syntax Validation, MX Validation, List Detective Validation)<br><br>  
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
  // REST endpoint for obtaining access token  
  var authUrl = "https://******************.auth.marketingcloudapis.com/v2/token";  
  var authResult = HTTP.Post(authUrl, 'application/json', Stringify(authPayload));  
  if (authResult.StatusCode == 200) {  
    var authResponse = Platform.Function.ParseJSON(authResult.Response[0]);  
    var accessToken = authResponse.access_token;  
    var restUrl = authResponse.rest_instance_url;  
  }  
  else {  
    // Throw exception in case of access token retrieval error  
    throw new Error("Error occurred while obtaining access token.");  
  }  
  var submittedEmail = Variable.GetValue("@submittedEmail");  
  if (submittedEmail) {  
    // Execute only if the email address exists  
    // REST API endpoint for validating email address  
    var validateEmailUrl = restUrl + 'address/v1/validateEmail';  
    var validateEmailPayload = {  
      "email": submittedEmail,  
      "validators": ["SyntaxValidator", "MXValidator", "ListDetectiveValidator"]  
    };  
    var validateEmailHeaders = ["Authorization"];  
    var validateEmailHeaderValues = ["Bearer " + accessToken];  
    var validateEmailResult = HTTP.Post(validateEmailUrl, 'application/json', Stringify(validateEmailPayload), validateEmailHeaders, validateEmailHeaderValues);  
    var responseEntities = Platform.Function.ParseJSON(validateEmailResult.Response[0]);  
    Write("Email Address: " + Stringify(responseEntities.email) + "<br>");  
    if (responseEntities.valid) {  
      Write("Validation Result: Valid<br>");  
    }  
    else {  
      Write("Validation Result: Invalid<br>");  
      Write("Validation Type: " + Stringify(responseEntities.failedValidation) + "<br>");  
    }  
    Write("<br>");  
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
Reference:  
<a href="https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/validateEmail.html">POST /address/v1/validateEmail</a><br>  
<br>  
List Detective Examples:<br><br>  
- info<br>  
- default<br>  
- support<br>  
- webmaster<br>  
- subscribe<br>  
- unsubscribe<br>  
- null<br>  
- noreply<br>  
- privacy<br>  
- postmaster<br>  
- mailerdaemon<br>  
- nobody<br>  
- none<br>  
- www<br>  
- remove<br>  
- root<br>  
- invalid<br>  
- junk<br>  
- junkmail<br>  
- junkemail<br>  
- noc<br>  
- noemail<br>  
- listserv<br>  
- usenet<br>  
- abuse<br>  
- uucp<br>
```

■ Within this code, there are three items that require modification:

- **Client ID**
- **Client Secret**
- **Authentication-based URL**

2. Once the configuration of the HTML block is complete, please save and publish.

3. After the publishing is complete, copy the URL from Cloudpages.

4. As for the Cloudpages configuration, the steps above are sufficient. Following this, you will proceed to configure the installed package. Since the app is already running, let’s try clicking on the Cloudpages URL.

5. When the page appears, for example, enter an email address starting with info@ and click the ‘Send’ button.

![]()

6. As a result, it will display ‘ListDetectiveValidator,’ indicating that the corresponding email address is identified as a List Detective target.

![]()

*\*If, for instance, the ‘info@’ is excluded from the List Detective target using the Custom List Detective feature, validating an email address starting with ‘info@’ within this account will no longer trigger validation. This validation is specific to each account.*

Furthermore, with this REST API, in addition to List Detective validation, syntax validation and MX validation are also performed simultaneously. Therefore, if you validate an email address with two ‘@’ symbols, it will display ‘SyntaxValidator’ as shown below, for reference.

![]()

## 🚀 Installed Package Configuration

Next is the configuration of the installed package. By doing this, it will be visible on the AppExchange tab, similar to Query Studio.

1. In Marketing Cloud Setup, select **“Installed Packages”** and click the “New” button.

2. Decide on the name for the new package definition. This won’t be the displayed name. Afterward, click “Save”.

3. Click **“Add Component”**.

4. In the component type selection screen, choose **“Marketing Cloud App”** and click “Next”.

![]()

5. Finally, determine the “Display Name”. **Input the copied Cloudpages URL into both “Login Endpoint” and “Logout Endpoint”**. It’s acceptable for both URLs to be the same. After that, click “Save”.

*\* Once the save is complete,* ***log out and log back in****.*

![]()

6. After logging in, check AppExchange for display confirmation, and click on the display name.

7. In this case, the display name I assigned, ‘Email Validation’, becomes the logo, and the validation screen is displayed.

With this, the process is complete. 🎉

## Conclusion

As mentioned earlier, the Cloudpages created this time will be publicly accessible, making them viewable by anyone. Except for creating them temporarily for testing purposes, **when using them in production, be sure to implement an authentication mechanism to restrict access to specific users only**. 🚨

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
