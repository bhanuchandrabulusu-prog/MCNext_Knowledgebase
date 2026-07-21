# SFMC Tips #197 : Marketing Cloud App for Searching Not Sent Records

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-app-for-searching-not-sent-records-a1b13ed4f196

---

# SFMC Tips #197 : Marketing Cloud App for Searching Not Sent Records

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a1b13ed4f196---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a1b13ed4f196---------------------------------------)

10 min read

·

Oct 24, 2025

--

Photo by [Florencia Viadana](https://unsplash.com/@florenciaviadana?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Some of you might have forgotten that I’m actually a **Marketing Cloud Engagement** expert — not just someone who posts about **Marketing Cloud Next** all the time. No, I haven’t sold my soul. Yes, I’m still here! How have you been? 😎

It’s been quite a while since [I introduced a method to **extract Not Sent records** and store them in a **data extension**](/@marketingcloudtips/automating-extract-not-sent-and-storing-in-a-data-extension-5d88794a7f76).

In response to that article, **Fernando Prates-san** shared a LinkedIn post referencing my work, where he showcased a mechanism that allows users to **search Not Sent data extensions directly on CloudPages**. I found his idea incredibly interesting, so I decided to revisit the topic and share it with all of you.

![]()

Fernando Prates

[## How to Check Email Deliverability in Marketing Cloud | Fernando Prates posted on the topic |…

### Need a quick way to check if an email is still deliverable in Marketing Cloud? Whether for quick diagnosis or support…

www.linkedin.com](https://www.linkedin.com/posts/fernando-prates-crm-salesforce_sfmc-tips-73-automating-extract-not-sent-activity-7352196483439329280-PFqv/?utm_source=share&utm_medium=member_desktop&rcm=ACoAACy9CycBou0Y0TMGTScLWA4i9K-cYqIwypA&source=post_page-----a1b13ed4f196---------------------------------------)

While writing this article, I also reviewed my own implementation and made some improvements to make it more user-friendly. I’ve prepared **two versions** of the app:

- A version **accessible without login**
- A version **restricted with login access**

### **Version Accessible Without Login**

First, follow the steps in the article below to **create the Not Sent data extension**.

[## SFMC Tips #73 : Automating Extract Not Sent and Storing in a Data Extension

### In a previous article, I explored how to use the “Extract Not Sent” feature in Automation Studio to retrieve…

medium.com](/@marketingcloudtips/automating-extract-not-sent-and-storing-in-a-data-extension-5d88794a7f76?source=post_page-----a1b13ed4f196---------------------------------------)

It’s important to set the **Not Sent data extension name** and **field names** exactly as shown.

- **Data Extension Name:** NotSent
- **Subscriber Key Field Name:** SubscriberKey
- **Email Address Field Name:** EmailAddress
- **Triggered Send Key Field Name:** TriggeredSendExternalKey

Once these are correctly configured, simply paste the following code into an **HTML block on CloudPages**, publish it, and you’ll have a public page that allows anyone to **search for Not Sent records**.

The key point in that version is that **it doesn’t require a Client ID or Client Secret** — you simply paste the code, and you’re done.

```
<title>Not Sent Record Search</title>  
<h2>Search Not Sent Records</h2>  
  
<form method="post">  
  <label for="subscriberKey">Subscriber Key:</label><br>  
  <input type="text" id="subscriberKey" name="subscriberKey"><br><br>  
  
  <label for="email">Email Address:</label><br>  
  <input type="text" id="email" name="email"><br><br>  
  
  <label for="triggeredSendExternalKey">Triggered Send Key:</label><br>  
  <input type="text" id="triggeredSendExternalKey" name="triggeredSendExternalKey"><br><br>  
  
  <button type="submit">Search</button>  
</form><br>  
  
※ Multi-field filtering is not supported using the search boxes above.<br>  
※ If multiple fields are entered, priority is given in the following order: Subscriber Key → Email Address → Triggered Send Key.<br>  
※ Records where Reason = Account Level Opt Out are excluded to avoid duplication with Unsubscribed Master records.<br>  
※ Records with Reason Held are displayed duplicately with different batch IDs, so all records with a value other than "0" are excluded.<br>  
※ Search results are displayed in descending order by send date.<br><br>  
  
・Held: Delivery suspended after bounce<br>  
・Unsubscribed Master: Unsubscribed<br>  
・Send Failure: Delivery failed for unknown reason<br>  
・Build Email Error: Error generating email<br>  
・Invalid Email Address: Invalid email address<br>  
・Excluded by Send Time Filter: Excluded by Exclusion Script<br>  
・Domain Exclusion: Excluded by domain filter<br>  
・Suppression List Exclusion: Automatically excluded by suppression list<br>  
・List Detective Exclusion: Excluded by List Detective<br><br>  
  
<hr>  
  
<div id="resultado">  
  <script runat="server">  
    Platform.Load("Core", "1.1.1");  
  
    var email = Request.GetFormField("email");  
    var subscriberKey = Request.GetFormField("subscriberKey");  
    var triggeredSendExternalKey = Request.GetFormField("triggeredSendExternalKey");  
  
    var searchField = "";  
    var searchValue = "";  
    var rows = [];  
  
    var myDE = DataExtension.Init("NotSent");  
  
    if (subscriberKey) {  
      rows = myDE.Rows.Lookup("SubscriberKey", subscriberKey);  
      searchField = "Subscriber Key";  
      searchValue = subscriberKey;  
    } else if (email) {  
      rows = myDE.Rows.Lookup("EmailAddress", email);  
      searchField = "Email Address";  
      searchValue = email;  
    } else if (triggeredSendExternalKey) {  
      rows = myDE.Rows.Lookup("TriggeredSendExternalKey", triggeredSendExternalKey);  
      searchField = "Triggered Send Key";  
      searchValue = triggeredSendExternalKey;  
    }  
  
    if (rows && rows.length > 0) {  
      // Exclude "Account Level Opt Out" records  
      var filteredRows = [];  
      for (var i = 0; i < rows.length; i++) {  
        var row = rows[i];  
        var reason = row.Reason;  
        var batchId = row.BatchID;  
  
        if (reason == "Account Level Opt Out") {  
          continue; // Exclude  
        }  
  
        if (reason == "Held" && batchId != "0") {  
          continue; // Exclude Held with BatchID ≠ 0  
        }  
  
        filteredRows.push(row);  
      }  
  
      // Sort by EventDate in descending order  
      filteredRows.sort(function(a, b) {  
        var dateA = new Date(a.EventDate);  
        var dateB = new Date(b.EventDate);  
        return dateB - dateA;  
      });  
  
      Write("<h3>" + filteredRows.length + " record(s) found:</h3>");  
      Write("<p>Search condition: \"" + searchField + "\" = " + searchValue + "</p><br>");  
  
      for (var j = 0; j < filteredRows.length; j++) {  
        var reasonText = filteredRows[j].Reason;  
        var originalDate = new Date(filteredRows[j].EventDate);  
        originalDate.setHours(originalDate.getHours() + 0);  
  
        function pad(n) {  
          return n < 10 ? '0' + n : n;  
        }  
  
        var formattedDate =  
          originalDate.getFullYear() + '-' +  
          pad(originalDate.getMonth() + 1) + '-' +  
          pad(originalDate.getDate()) + ' ' +  
          pad(originalDate.getHours()) + ':' +  
          pad(originalDate.getMinutes()) + ':' +  
          pad(originalDate.getSeconds());  
  
        Write("<div>");  
        Write("<p><strong>Send ID:</strong> " + filteredRows[j].SendID + "</p>");  
        Write("<p><strong>Subscriber Key:</strong> " + filteredRows[j].SubscriberKey + "</p>");  
        Write("<p><strong>Email Address:</strong> " + filteredRows[j].EmailAddress + "</p>");  
        Write("<p><strong>Triggered Send Key:</strong> " + filteredRows[j].TriggeredSendExternalKey + "</p>");  
        Write("<p><strong>Send Date:</strong> " + formattedDate + "</p>");  
        Write("<p><strong>Reason:</strong> " + reasonText + "</p>");  
        Write("</div><hr />");  
      }  
  
    } else if (email || subscriberKey || triggeredSendExternalKey) {  
      Write("<p>No matching data found.</p>");  
      Write("<p>Search condition: \"" + searchField + "\" = " + searchValue + "</p>");  
    }  
  </script>  
</div>
```

![]()

### **Version with Login Authentication**

The CloudPages version above is accessible to anyone, which poses potential risks such as **data leakage** or **unauthorized access**. To mitigate these risks, it’s essential to implement the technique I previously introduced for **protecting against unauthorized access**.

The approach I introduce was originally developed by **Mateusz Dąbrowski-san**, and it enables you to **embed a login authentication mechanism** directly within CloudPages.

![]()

Mateusz Dąbrowski

Since explaining everything from scratch would make this article quite long, please refer to the detailed steps in the article linked below.

[## Solve with Cloud Page Apps | Mateusz Dąbrowski

### Create micro applications tailored to your organisation needs using only Salesforce Marketing Cloud features.

mateuszdabrowski.pl](https://mateuszdabrowski.pl/docs/salesforce/marketing-cloud-engagement/ssjs/snippets/sfmc-cloud-page-apps/?source=post_page-----a1b13ed4f196---------------------------------------)

Before using this version, make sure to create the following **data extensions**:

- **AUTHENTICATION\_DATA\_EXTENSION** — for storing authentication logs

\*Once the data extension is created, set the default value of **createdDate** to “**Current Date”**.

```
<script runat="server">  
    Platform.Load("Core", "1");  
  
    var dataExtensionConfig = {  
        "CustomerKey": "",  
        "Name": "AUTHENTICATION_DATA_EXTENSION",  
        "Fields": [  
  
{ "Name" : "session", "FieldType" : "Text", "MaxLength" : 50, "IsPrimaryKey" : true, "IsRequired" : true },   
{ "Name" : "appName", "FieldType" : "Text", "MaxLength" : 100, "IsRequired" : false },   
{ "Name" : "createdDate", "FieldType" : "Date", "IsRequired" : false },   
{ "Name" : "token", "FieldType" : "Text", "MaxLength" : 520, "IsRequired" : false },   
{ "Name" : "tokenExpire", "FieldType" : "Date", "IsRequired" : false },   
{ "Name" : "userName", "FieldType" : "Text", "MaxLength" : 100, "IsRequired" : false },   
{ "Name" : "userEmail", "FieldType" : "Text", "MaxLength" : 254, "IsRequired" : false },  
  
        ]  
    };  
  
    var createdDataExtension = DataExtension.Add(dataExtensionConfig);  
</script>
```

![]()

- **ERROR\_DATA\_EXTENSION** — for recording error information

```
<script runat="server">  
    Platform.Load("Core", "1");  
  
    var dataExtensionConfig = {  
        "CustomerKey": "",  
        "Name": "ERROR_DATA_EXTENSION",  
        "Fields": [  
  
{ "Name" : "id", "FieldType" : "Text", "MaxLength" : 36, "IsPrimaryKey" : true, "IsRequired" : true },   
{ "Name" : "errorSource", "FieldType" : "Text", "MaxLength" : 100, "IsRequired" : false },   
{ "Name" : "errorMessage", "FieldType" : "Text", "MaxLength" : 2000, "IsRequired" : false },   
{ "Name" : "errorDescription", "FieldType" : "Text", "MaxLength" : 2000, "IsRequired" : false },   
{ "Name" : "errorDate", "FieldType" : "Date", "IsRequired" : false },   
  
        ]  
    };  
  
    var createdDataExtension = DataExtension.Add(dataExtensionConfig);  
</script>
```

![]()

Additionally, obtain the **Client ID** and **Client Secret** required for authentication in your web app.

A sample code snippet for the **login-protected version** is provided below — you can use it as is.

```
<title>Not Sent Record Search</title>  
<h2>Search Not Sent Records</h2>  
  
<form method="post">  
  <label for="subscriberKey">Subscriber Key:</label><br>  
  <input type="text" id="subscriberKey" name="subscriberKey"><br><br>  
  
  <label for="email">Email Address:</label><br>  
  <input type="text" id="email" name="email"><br><br>  
  
  <label for="triggeredSendExternalKey">Triggered Send Key:</label><br>  
  <input type="text" id="triggeredSendExternalKey" name="triggeredSendExternalKey"><br><br>  
  
  <button type="submit">Search</button>  
</form><br>  
  
※ Multi-field filtering is not supported using the search boxes above.<br>  
※ If multiple fields are entered, priority is given in the following order: Subscriber Key → Email Address → Triggered Send Key.<br>  
※ Records where Reason = Account Level Opt Out are excluded to avoid duplication with Unsubscribed Master records.<br>  
※ Records with Reason Held are displayed duplicately with different batch IDs, so all records with a value other than "0" are excluded.<br>  
※ Search results are displayed in descending order by send date.<br><br>  
  
・Held: Delivery suspended after bounce<br>  
・Unsubscribed Master: Unsubscribed<br>  
・Send Failure: Delivery failed for unknown reason<br>  
・Build Email Error: Error generating email<br>  
・Invalid Email Address: Invalid email address<br>  
・Excluded by Send Time Filter: Excluded by Exclusion Script<br>  
・Domain Exclusion: Excluded by domain filter<br>  
・Suppression List Exclusion: Automatically excluded by suppression list<br>  
・List Detective Exclusion: Excluded by List Detective<br><br>  
  
<hr>  
  
<div id="resultado">  
  <script runat="server">  
    Platform.Load("Core", "1.1.1");  
  
    var email = Request.GetFormField("email");  
    var subscriberKey = Request.GetFormField("subscriberKey");  
    var triggeredSendExternalKey = Request.GetFormField("triggeredSendExternalKey");  
  
    if (!email && !subscriberKey && !triggeredSendExternalKey) {  
      // Initialization  
      var debugging = true;  
      var appName = '*********************'; // App name (saved in audit DE)  
      var appURL = '*********************'; // CloudPages URL  
      var clientID = '*********************'; // WebApp Client ID  
      var clientSecret = '*********************'; // WebApp Client Secret  
      var clientBase = '*********************'; // Account Client Base  
      var authDE = 'AUTHENTICATION_DATA_EXTENSION';  
      var errorDE = 'ERROR_DATA_EXTENSION';  
      var errorURL = 'https://medium.com/@marketingcloudtips';  
  
      var state = Platform.Request.GetQueryStringParameter('state');  
      var errorMessage = Platform.Request.GetQueryStringParameter('error');  
      var errorDescription = Platform.Request.GetQueryStringParameter('error_description');  
  
      function debugValue(description, value) {  
        // Uncomment for debugging  
        // Write(description + ': ' + (typeof value == 'object' ? Stringify(value) : value) + '<br><br>');  
      }  
  
      function handleError(error) {  
        if (debugging) {  
          debugValue('Found error', error);  
        } else {  
          Platform.Function.InsertData(  
            errorDE,  
            ['id', 'appName', 'errorMessage', 'errorDescription'],  
            [GUID(), appName, error.message, error.description]  
          );  
          Platform.Response.Redirect(errorURL + '?error=' + error.message + '&error_description=' + error.description);  
        }  
      }  
  
      if (!state && !errorMessage) {  
        // Initial OAuth redirect  
        state = GUID();  
        Platform.Response.Redirect(  
          'https://' + clientBase + '.auth.marketingcloudapis.com/v2/authorize' +  
          '?response_type=code&client_id=' + clientID +  
          '&redirect_uri=' + appURL +  
          '&state=' + state  
        );  
      } else if (state) {  
        // Handle OAuth response  
        var code = Platform.Request.GetQueryStringParameter('code');  
        var payload = {  
          grant_type: 'authorization_code',  
          code: code,  
          client_id: clientID,  
          client_secret: clientSecret,  
          redirect_uri: appURL  
        };  
  
        var response = HTTP.Post(  
          'https://' + clientBase + '.auth.marketingcloudapis.com/v2/token',  
          'application/json',  
          Stringify(payload)  
        );  
  
        if (response.StatusCode == 200) {  
          var parsedResponse = Platform.Function.ParseJSON(response.Response[0]);  
          var accessToken = parsedResponse.access_token;  
  
          var tokenExpire = Platform.Function.SystemDateToLocalDate(Platform.Function.Now());  
          tokenExpire.setMinutes(tokenExpire.getMinutes() + 18);  
  
          response = HTTP.Get(  
            'https://' + clientBase + '.auth.marketingcloudapis.com/v2/userinfo',  
            ['Authorization'],  
            ['Bearer ' + accessToken]  
          );  
  
          if (debugging) {  
            debugValue('UserInfo Response', response);  
          }  
  
          var userInfo = Platform.Function.ParseJSON(response.Content).user;  
          var userName = userInfo.name;  
          var userEmail = userInfo.email;  
  
          Platform.Function.UpsertData(  
            authDE,  
            ['session'], [state],  
            ['appName', 'token', 'tokenExpire', 'userName', 'userEmail'],  
            [appName, accessToken, tokenExpire, userName, userEmail]  
          );  
  
        } else {  
          handleError({  
            message: 'Authentication Failed',  
            description: 'Status: ' + response.StatusCode  
          });  
        }  
      } else {  
        handleError({  
          message: errorMessage,  
          description: errorDescription  
        });  
      }  
  
    } else {  
      var searchField = "";  
      var searchValue = "";  
      var rows = [];  
  
      var myDE = DataExtension.Init("NotSent");  
  
      if (subscriberKey) {  
        rows = myDE.Rows.Lookup("SubscriberKey", subscriberKey);  
        searchField = "Subscriber Key";  
        searchValue = subscriberKey;  
      } else if (email) {  
        rows = myDE.Rows.Lookup("EmailAddress", email);  
        searchField = "Email Address";  
        searchValue = email;  
      } else if (triggeredSendExternalKey) {  
        rows = myDE.Rows.Lookup("TriggeredSendExternalKey", triggeredSendExternalKey);  
        searchField = "Triggered Send Key";  
        searchValue = triggeredSendExternalKey;  
      }  
  
      if (rows && rows.length > 0) {  
        var filteredRows = [];  
        for (var i = 0; i < rows.length; i++) {  
          var row = rows[i];  
          var reason = row.Reason;  
          var batchId = row.BatchID;  
  
          if (reason == "Account Level Opt Out") {  
            continue;  
          }  
  
          if (reason == "Held" && batchId != "0") {  
            continue;  
          }  
  
          filteredRows.push(row);  
        }  
  
        filteredRows.sort(function(a, b) {  
          var dateA = new Date(a.EventDate);  
          var dateB = new Date(b.EventDate);  
          return dateB - dateA;  
        });  
  
        Write("<h3>" + filteredRows.length + " record(s) found:</h3>");  
        Write("<p>Search condition: \"" + searchField + "\" = " + searchValue + "</p><br>");  
  
        for (var j = 0; j < filteredRows.length; j++) {  
          var reasonText = filteredRows[j].Reason;  
          var originalDate = new Date(filteredRows[j].EventDate);  
          originalDate.setHours(originalDate.getHours() + 0);  
  
          function pad(n) {  
            return n < 10 ? '0' + n : n;  
          }  
  
          var formattedDate =  
            originalDate.getFullYear() + '-' +  
            pad(originalDate.getMonth() + 1) + '-' +  
            pad(originalDate.getDate()) + ' ' +  
            pad(originalDate.getHours()) + ':' +  
            pad(originalDate.getMinutes()) + ':' +  
            pad(originalDate.getSeconds());  
  
          Write("<div>");  
          Write("<p>Send ID: " + filteredRows[j].SendID + "</p>");  
          Write("<p>Subscriber Key: " + filteredRows[j].SubscriberKey + "</p>");  
          Write("<p>Email Address: " + filteredRows[j].EmailAddress + "</p>");  
          Write("<p>Triggered Send Key: " + filteredRows[j].TriggeredSendExternalKey + "</p>");  
          Write("<p>Send Date: " + formattedDate + "</p>");  
          Write("<p>Reason: " + reasonText + "</p>");  
          Write("</div><hr />");  
        }  
  
      } else if (email || subscriberKey || triggeredSendExternalKey) {  
        Write("<p>No matching data found.</p>");  
        Write("<p>Search condition: \"" + searchField + "\" = " + searchValue + "</p>");  
      }  
    }  
  </script>  
</div>
```

In this code, there are **five items** you need to review and update as necessary:

- App name
- CloudPages URL
- WebApp Client ID
- WebApp Client Secret
- Account Client Base

Note: The **Client Base** refers to the section marked with `*****************` in the URL below:

```
https://*****************.auth.marketingcloudapis.com/v2/token
```

### Relationship between the number of Not Sent search results and the “Not Sent” count in email analytics

When using the conditions described above to search by **Triggered Send Key**, the number of search results should generally match the **“Not Sent”** count in Journey Builder email analytics.

There are two main points that make the magic happen — and once you handle both, everything works seamlessly.

- **Records where Reason = Account Level Opt Out are excluded to avoid duplication with Unsubscribed Master records.**
- **Records with Reason Held are displayed duplicately with different batch IDs, so all records with a value other than “0” are excluded.**

![]()

## Conclusion

The technique introduced here is very useful because it makes **troubleshooting Not Sent emails much easier**, and it’s something that could be considered a standard tool in any Marketing Cloud Engagement account.

Moreover, this method is not limited to the Not Sent DE — it can be adapted to search **various other data extensions** as well. Feel free to customize it according to your own use cases and test it out.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
