# SFMC Tips #26 : How to Disable List Detective: Enabling the ‘Custom List Detective’ Feature

**Source:** https://medium.com/@marketingcloudtips/how-to-disable-list-detective-enabling-the-custom-list-detective-feature-1e3dd4426add

---

# *SFMC Tips #26 : How to Disable List Detective: Enabling the ‘Custom List Detective’ Feature*

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1e3dd4426add---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1e3dd4426add---------------------------------------)

3 min read

·

Feb 16, 2024

--

*Photo by* [*Clément Falize*](https://unsplash.com/@centelm?utm_source=medium&utm_medium=referral) *on* [*Unsplash*](https://unsplash.com/?utm_source=medium&utm_medium=referral)

I previously wrote an article about what List Detective is.

[## SFMC Tips #25 : Self-Searching for Email Addresses Targeted by List Detective

### The List Detective feature enables Salesforce Marketing Cloud to proactively exclude email addresses identified as…

medium.com](/@marketingcloudtips/self-searching-for-email-addresses-targeted-by-list-detective-1689c90ec1b7?source=post_page-----1e3dd4426add---------------------------------------)

## What is List Detective?

List Detective is a feature that automatically detects email addresses that may negatively impact deliverability and excludes them from send audiences. This helps prevent a decline in IP reputation. Note that this feature cannot be completely disabled at the account level.

For example, email addresses containing the following usernames (account names) are automatically excluded from sends:

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

## Using Custom List Detective

In some cases, you may want to override List Detective for specific addresses, such as allowing sends to **info@**.

In such cases, you can use **Custom List Detective**.

To enable this feature, you need to open a case with the Salesforce Support team. Once enabled, a configuration screen will appear under the **Admin** tab in Email Studio, where you can control filtering at both the username (account name) and domain levels.

## Important Notes

- **Only the Salesforce Support team** can register usernames or domains to be exempted from List Detective.
- Although the interface may appear to allow you to add new entries, adding them yourself will **not** disable List Detective.
- On the contrary, any email address containing the registered username or domain will actually become subject to List Detective and be excluded from sends.

## How to Check List Detective Matches in a Data Extension

If you want to see how many email addresses in a data extension fall under List Detective criteria, you can use the following SQL query:

```
SELECT TOP 100  
    SUBSTRING([Email], 0, CHARINDEX('@', [Email])) AS User_Name,  
    COUNT(SUBSTRING([Email], 0, CHARINDEX('@', [Email]))) AS Count  
FROM [Data_Extension_Name]  
WHERE SUBSTRING([Email], 0, CHARINDEX('@', [Email])) IN (  
    'info', 'default', 'support', 'webmaster', 'subscribe', 'unsubscribe',  
    'null', 'noreply', 'privacy', 'postmaster', 'mailerdaemon', 'nobody',  
    'none', 'www', 'remove', 'root', 'invalid', 'junk', 'junkemail',  
    'junkmail', 'noc', 'noemail', 'listserv', 'usenet', 'abuse', 'uucp'  
)  
GROUP BY SUBSTRING([Email], 0, CHARINDEX('@', [Email]))  
ORDER BY COUNT(SUBSTRING([Email], 0, CHARINDEX('@', [Email]))) DESC
```

Replace the following values as needed:

- `[Data_Extension_Name]` → The name of your target data extension
- `[Email]` → The field name storing email addresses

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
