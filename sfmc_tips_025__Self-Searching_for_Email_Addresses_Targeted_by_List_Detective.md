# SFMC Tips #25 : Self-Searching for Email Addresses Targeted by List Detective

**Source:** https://medium.com/@marketingcloudtips/self-searching-for-email-addresses-targeted-by-list-detective-1689c90ec1b7

---

# SFMC Tips #25 : Self-Searching for Email Addresses Targeted by List Detective

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1689c90ec1b7---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1689c90ec1b7---------------------------------------)

4 min read

·

Feb 15, 2024

--

Photo by [Marek Szturc](https://unsplash.com/@marxgall?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The List Detective feature enables Salesforce Marketing Cloud to proactively exclude email addresses identified as “BAD” from being sent at the following times:

- **During email sending using Data Extensions.**
- **When importing into lists such as All Subscriber lists.**

This feature helps avoid sending to email addresses that could potentially cause delivery issues and helps mitigate the risk of a decrease in IP reputation.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000387004&type=1&source=post_page-----1689c90ec1b7---------------------------------------)

This database includes the following:

- Email spam traps  
- Blocklisted addresses  
- Non-existent domains (e.g., @gmai.com instead of @gmail.com)  
- Retired email companies or webmail providers  
- Global unsubscribes  
- Mistypes  
and more.

The database containing email addresses and logic corresponding to List Detective is generally not disclosed. According to Salesforce Support guidance, they will explain the reasons why individual email addresses are included in the List Detective database, but raising a case with support is necessary. However, submitting a support case for each instance can be cumbersome.

Therefore, this time, we would like to inform you of a method to search on your own.

It’s worth noting that typical usernames (account names) that trigger List Detective include:

```
- info  
- default  
- support  
- webmaster  
- subscribe  
- unsubscribe  
- null  
- noreply  
- privacy  
- postmaster  
- mailerdaemon  
- nobody  
- none  
- www  
- remove  
- root  
- invalid  
- junk  
- junkmail  
- junkemail  
- noc  
- noemail  
- listserv  
- usenet  
- abuse  
- uucp
```

*\*Additionally, email addresses containing words like spam, blacklist, blocklist are also excluded in advance.*

## ■ Setting the Stage

Before embarking on this journey, ensure you have the following essentials from a previous guide: the **REST Base URL** and the all-important **Access Token**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----1689c90ec1b7---------------------------------------)

```
--- METHOD   
POST  
  
--- ENDPOINT  
https://[Authentication Base URL].auth.marketingcloudapis.com/v2/token  
  
--- HEADERS   
Content-Type：application/json  
  
--- BODY  
{  
 "grant_type": "client_credentials",  
 "client_id": "[Client Id]",  
 "client_secret": "[Client Secret]",  
 "account_id": "[MID]"  
}
```

In the **Scope** of this API configuration, the following is required:

- **CHANNELS — Email — Read**

[## Salesforce Developers

### Review the permission ID, the path to the permission in Marketing Cloud, and the Installed Packages scope for each REST…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html?source=post_page-----1689c90ec1b7---------------------------------------)

Now, let’s validate two scenarios using REST API in this article:

1. “info@gmail.com” → Assumed to be targeted by List Detective.
2. “info2@gmail.com” → Assumed not to be targeted by List Detective.

## ■ Email Validation

1. Open “Talend API Tester”, and input the following for the search of “info@gmail.com”:

```
--- Method  
POST  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/address/v1/validateEmail  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Body (Sample)  
{  
"email": "info@gmail.com",  
"validators": ["SyntaxValidator", "MXValidator", "ListDetectiveValidator"]  
}
```

2. Press the “Send” button.

3. “info@gmail.com” is identified as List Detective.

4. Now, let’s check for “info2@gmail.com.” Press the “Send” button.

5. Here, “info2@gmail.com” does not appear to be flagged by List Detective.

That’s all for the explanation.

*Note: This API (address/v1/validateEmail) can also check for “syntax errors” in email addresses like “info@@gmail.com” (double @).*

## ■ Conclusion

A drawback of this API is that it can only check one record at a time. It would be convenient if it could perform bulk checks for email addresses within Data Extensions.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
