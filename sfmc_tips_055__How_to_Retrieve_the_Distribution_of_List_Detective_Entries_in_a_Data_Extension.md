# SFMC Tips #55 : How to Retrieve the Distribution of List Detective Entries in a Data Extension

**Source:** https://medium.com/@marketingcloudtips/how-to-retrieve-the-distribution-of-list-detective-entries-in-a-data-extension-98c35be50a12

---

# SFMC Tips #55 : How to Retrieve the Distribution of List Detective Entries in a Data Extension

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--98c35be50a12---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--98c35be50a12---------------------------------------)

2 min read

·

Sep 12, 2024

--

Photo by [Mohammad Alizade](https://unsplash.com/@mohamadaz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I wrote about how to retrieve the distribution of List Detective entries in a data extension within Salesforce Marketing Cloud. Although it’s a very handy technique, it has become somewhat buried and hard to find on Medium. Therefore, I’ve decided to publish it again as a standalone article.

[## SFMC Tips #26 : How to Disable List Detective: Enabling the ‘Custom List Detective’ Feature

### Photo by Clément Falize on Unsplash

medium.com](/@marketingcloudtips/how-to-disable-list-detective-enabling-the-custom-list-detective-feature-1e3dd4426add?source=post_page-----98c35be50a12---------------------------------------)

By running the following SQL in Query Studio, you can investigate how usernames (the part before the ‘@’ symbol) classified as List Detective are distributed within a specific data extension.

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

*Please replace* `[Data_Extension_Name]` *and* `[Email]` *with the appropriate values from your environment before executing the query.*

For an explanation of List Detective, refer to the article linked below:

[## SFMC Tips #25 : Self-Searching for Email Addresses Targeted by List Detective

### The List Detective feature enables Salesforce Marketing Cloud to proactively exclude email addresses identified as…

medium.com](/@marketingcloudtips/self-searching-for-email-addresses-targeted-by-list-detective-1689c90ec1b7?source=post_page-----98c35be50a12---------------------------------------)

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
