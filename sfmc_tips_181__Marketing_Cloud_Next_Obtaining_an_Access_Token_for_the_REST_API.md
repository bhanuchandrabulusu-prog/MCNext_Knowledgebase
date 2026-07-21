# SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584

---

# SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--156eca392584---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--156eca392584---------------------------------------)

8 min read

·

Oct 5, 2025

--

Photo by [Louis Droege](https://unsplash.com/@lois184?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

I previously wrote an article explaining how to obtain an access token when using the REST API in Marketing Cloud Engagement.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----156eca392584---------------------------------------)

This time, I will explain how to configure the Client Credentials Flow on the Salesforce Platform to use the REST APIs for Data Cloud and Marketing Cloud Next.

As with Marketing Cloud Engagement, you need to obtain an access token to use the REST APIs. However, on the Salesforce Platform, authentication is performed by creating an OAuth Client (External Client Application).

> *💡 What is an External Client Application?  
>  If you have used Marketing Cloud Engagement before, you can think of it as similar to an Installed Package. Both are mechanisms for registering an application that uses APIs and issuing a Client ID and Client Secret. The difference is that an External Client Application on the Salesforce Platform is specifically designed for OAuth authentication configuration.*

I usually use Talend API Tester (a Chrome extension) instead of Postman, so this article uses Talend API Tester. Of course, if you prefer Postman, you can follow exactly the same steps.

The configuration consists of the following four steps. In this article, I will cover Steps 1 through 3. The REST API call in Step 4 will be explained in a separate article.

1. Create an External Client Application for API integration.
2. Install Talend API Tester.
3. Obtain an access token using the Client Credentials Flow.
4. Execute a REST API.

## ① Configure the API Integration Interface

1. Prepare a user that will connect to the API (an Integration User).  
*\*For demonstration purposes, you may temporarily use a System Administrator account.*

> *💡 What is an Integration User?  
>  An Integration User is a Salesforce user dedicated to REST APIs and external system integrations. It is not intended for interactive user logins. Instead, it represents the user permissions under which API operations are executed in Salesforce.*

- **Last Name:** Marketing Cloud Next Integration
- **Alias:** MCN-API
- **Email:** Your administrator’s actual email address
- **Username:** mcnext.integration@~
- **Nickname:** mcnext.integration
- **User License:** Salesforce Integration
- **Profile:** Minimum Access — API Only Integrations  
  *\*This profile is the minimum-privilege profile intended exclusively for API users.*

> *Tips: If you select the* ***Minimum Access — API Only Integrations*** *profile, logging into the Salesforce UI with this user will display* ***“Access Restricted for API Only Users”****. This is expected behavior. Because this profile is designed exclusively for API users, browser-based UI access is not permitted. Do not manage the Integration User by logging in as that user. Instead, a System Administrator should manage the Integration User using their own administrator account.*

![]()

2. Assign the following two permission sets to the Integration User you created.

- Data Cloud Architect
- Marketing Cloud Admin

*For this article, relatively broad permissions are granted for demonstration purposes. In a production environment, grant only the minimum permissions required for your specific use case.*

3. Next, search for **External Client Application** in **Setup**. Click the displayed setup page and enable **Allow access to consumer secrets for external client applications using the REST API**.

4. Then, select **External Client App Manager** and click “**New External Client App**”.

5. Fill in the required fields under **Basic Information**.

- **External Client App Name**  
  Enter a name that clearly identifies the application’s purpose. Once entered, the **API Name** is generated automatically. Since both are used for internal management, any meaningful name is acceptable.
- **Contact Email**  
  Enter a valid email address. Normal API usage notifications are not sent to this email address. It is simply registered as the administrator contact information for the application.
- **Distribution State**  
  Since this application will only be used within the current Salesforce org, you can leave it as **Local**.

6. Next, open the **API (Enable OAuth Settings)** section and Enable OAuth.

7. Although a Callback URL is required, it is not actually used in this scenario. You can enter any placeholder value such as:

```
https://localhost:3000/oauth/callback
```

For the OAuth Scopes, select the following two scopes:

1. Manage user data via APIs (api)
2. Perform requests at any time (refresh\_token, offline\_access)

> *Tips: The Callback URL is not used because the Client Credentials Flow does not involve browser-based user authentication. Since the server obtains the access token directly, there is no redirect destination after authentication.*

8. Scroll down slightly, enable **Client Credentials Flow**, and click **Create**.

> *Tips: The security settings shown further down the page can be left at their default values. Since the Client Credentials Flow does not use Refresh Tokens or the Authorization Code Flow, these settings do not affect access token retrieval.*

9. Next, go to the **Policies** tab and click **Edit**.

10. Open the OAuth Policies section, enable **Client Credentials Flow**, enter the username of the Integration User you created earlier in **Run As**, and click **Save**.

*\*You may temporarily specify a System Administrator account, but as a best practice, you should ultimately specify the least-privileged Integration User.*

> *Note: If you click* ***Save*** *with a nonexistent username or an invalid user, an error will occur.*

11. Next, move to the **Settings** tab and open the **OAuth Settings** section.

12. Click **Consumer Key and Secret**.

13. Authenticate using either mobile verification or passcode verification.

14. The **Consumer Key** and **Consumer Secret** will be displayed. Copy them and save them for later use, or simply leave this page open for reference.

> *Tips: The Client Secret is not automatically rotated on a scheduled basis. It remains valid until an administrator explicitly regenerates (rotates) it.*

## ② Install Talend API Tester

Next, install the **Talend API Tester** Chrome extension from the Google Chrome Web Store.

*Before installing, check with your company’s IT department to make sure it’s acceptable to install this extension on your computer.*

1. Search for **“Talend API Tester”** in the Chrome Web Store.

2. Install **“Talend API Tester — Free Edition”.**

3. Once the installation is complete, open **Talend API Tester**.

## ③ Request an Access Token

Now let’s go ahead and obtain the **access token**!  
Before you begin, make sure you have the following three items prepared:

- Your **My Domain**, if you are using it
- The **Consumer Key**
- The **Consumer Secret**

1. Open a new request in the **Request** tab, and set the method to **POST**.

2. Next, enter the endpoint URL. This depends on whether or not you are using **My Domain**.

a. If you are using **My Domain**, enter the following. (Note: SDO, the Partner Demo Org, also uses My Domain, so use this option in that case.)

```
https://[My Domain Name].my.salesforce.com/services/oauth2/token
```

*You can find your My Domain by searching for* ***My Domain*** *in Setup.*

b. If you are **not** using My Domain, enter the following:

```
https://login.salesforce.com/services/oauth2/token
```

3. Next, configure the headers. Enter the following:

```
Content-Type: application/x-www-form-urlencoded
```

4. In the Body section, switch the tab on the right from **Text** to **Form**.

5. Click **Add form parameter** three times so that you can enter three parameters.

6. In the **name** field, enter the following three parameters:

- grant\_type
- client\_id
- client\_secret

7. For **grant\_type**, enter the fixed value: **client\_credentials**

8. For **client\_id** and **client\_secret**, copy and paste the values you obtained earlier.

9. Once everything is filled in, click the **Send** button.

***Note:*** *In a production environment, the best practice is to use an* ***Integration User*** *with only the minimum required permissions.*

10. After sending, scroll down. If the request is successful, the **access token** will be displayed. That’s it!

11. Finally, save this request with a name so you can reuse it later.

## Conclusion

You now have your **access token** to access Data Cloud and Marketing Cloud Next via the REST API.

In the next article, I’ll immediately try using this token to experiment with the new “**On-Demand Flow**” feature introduced in Marketing Cloud Next Winter ’26.

That wraps up this part.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
