# SFMC Tips #20 : Extracting Subscribers Who Haven’t Opened Emails in the Last 180 Days Using…

**Source:** https://medium.com/@marketingcloudtips/extracting-subscribers-who-havent-opened-emails-in-the-last-180-days-using-automation-studio-27c0d1c9bb80

---

# SFMC Tips #20 : Extracting Subscribers Who Haven’t Opened Emails in the Last 180 Days Using Automation Studio

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--27c0d1c9bb80---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--27c0d1c9bb80---------------------------------------)

11 min read

·

Jan 31, 2024

--

Photo by [Fernando Hernandez](https://unsplash.com/@_ferh97?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In your organization, is there a possibility that subscribers who have not opened any emails in the past 180 days might still open emails in the future? Have you seriously considered how to handle such subscribers?

**With the joint statement from Google and Yahoo in October 2023**, now is the time for us marketers to seriously consider this matter.

**The enforcement schedule for sender guidelines is planned to be implemented gradually as follows:**

***■ February 2024*** *bulk senders who don’t meet sender requirements will start getting temporary errors (with error codes) on a small percentage of their non-compliant email traffic. These temporary errors are meant to help senders identify email traffic that doesn’t meet our guidelines so that senders can resolve issues that result in non-compliance.*

***■ April 2024*** *Refusal of a certain percentage of non-compliant email traffic will commence. Subsequently, the refusal rate will gradually increase. For example, if 75% of a sender’s email traffic meets the requirements, the remaining 25% of non-compliant email traffic will start to be refused.*

***■ June 2024*** *By June 1, 2024, One-Click Unsubscribe suspension must be implemented for all commercial and promotional messages.*

It is not advisable to solely attribute the reasons for this email not being opened to the recipient’s side. The reason recipients may not open the email could be attributed to a potential issue with the sender-created “subject” and “preheader” not meeting the criteria. It is the responsibility of the sender to improve the content by using the A/B testing feature in Salesforce Marketing Cloud’s standard functionality for trial and error, as well as leveraging the recently released AI-generated ‘subject’ feature.

While making these improvements, **Salesforce has introduced sending guidelines for so-called ‘bulk senders’ in response to the joint statement from Google and Yahoo**. According to these guidelines, sending more than 5,000 messages to an individual Google account within 24 hours falls under the category of bulk sending. **Adhering to these guidelines is likely to become a best practice for future email communications**, so take the time to review them carefully.

### 📌 “Bulk Sender Guidelines” for Marketing Cloud Engagement

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_es_bulk_sender_guidelines.htm&type=5&source=post_page-----27c0d1c9bb80---------------------------------------)

\* Senders who have conducted 5,000 or more transmissions even once will be considered bulk senders permanently. (There is no expiration date; it is permanent.)

\* When calculating the number, all messages sent from the same primary domain will be included. For example, if 2,500 messages are sent from a subdomain (e.g., @mail.nac.co.jp) and another 2,500 messages are sent from the primary domain (e.g., @nac.co.jp), the sender will be treated as a bulk sender.

## ■ Sender Domain Authentication:

To ensure user security and protection, emails must be appropriately signed and authenticated, meeting the following authentication standards:

- Sender Policy Framework (SPF)
- DomainKeys Identified Mail (DKIM)
- Domain Message Authentication Reporting & Conformation (DMARC)

💡 Proposal from Salesforce:

- Purchase Salesforce Marketing Cloud Private Domain and Sender Authentication Package (SAP), and configure it accordingly.
- Verify the sending domain and ensure it is properly authenticated.

While most companies using Salesforce Marketing Cloud may have already purchased the Sender Authentication Package (SAP), it is suggested to verify that these configurations are correctly set up, even if already purchased.

## ■ One-Click Unsubscribe:

All commercial and promotional messages are required to implement a one-click unsubscribe mechanism that complies with RFC 8058 requirements.

💡 Proposal from Salesforce:

- All commercial and promotional messages sent from Salesforce Marketing Cloud include the List-Unsubscribe header by default, providing a one-click unsubscribe feature.

Google has explicitly advised to include the List-Unsubscribe header when implementing one-click unsubscribe in accordance with RFC 8058 requirements. And Salesforce explains that they have already implemented this feature in their commercial and promotional messages.

Google states that the following types of unsubscribe methods do not meet the requirements for the one-click unsubscribe specified in RFC 8058:

- Email recipient links, such as unsubscribe via mailto
- URL unsubscribe links, like opting out through %%unsub\_center\_url%% or redirecting to a specified website for opt-out

Transaction emails are exempt from these requirements. Transactional emails, including password reset messages, reservation confirmations, and purchase completion confirmations, are excluded from these requirements. It is advisable not to include unsubscribe links in such emails as they are considered necessary for recipients and could lead to confusion.

Google states that it does not automatically reject messages that do not meet the one-click unsubscribe requirements, nor does it mark such messages as spam. However, if the number of messages marked as spam by recipients increases, there is a higher likelihood that future messages from the sender will be classified as spam, so caution is advised.

## ■ Maintaining Spam Rate Below 0.3%:

“Bulk senders”, who send more than 5,000 messages per day, are required to maintain a spam rate below 0.3%.

💡 Proposal from Salesforce:

- Send relevant content only to engaged segments.
- Remove inactive Google accounts from the subscriber list, as sending messages to inactive accounts can increase bounce rates.

Google requests that the reported spam rate in Postmaster Tools be kept below 0.1%, and even if it is higher, it should not exceed 0.3%. For example, for 10,000 recipients, this corresponds to 10–29 individuals.

Now, what happens if these rules regarding the spam rate are not followed? There is some room for discussion on this. Google phrases it as follows:

To ensure messages are delivered as expected, bulk senders should comply with our Email sender guidelines. If senders don’t meet these requirements, messages might be rejected or delivered to recipients’ spam folders.

While it is stated that senders “should comply” with the guidelines, the possibility of messages being rejected or placed in the spam folder is mentioned with a somewhat ambiguous tone. Whether one perceives this as a warning or not, it is likely that stricter judgments will be applied in the future. From a recipient’s perspective, spam mail is undesirable, and Google’s stance on this matter is reasonable. If senders genuinely act in the interest of recipients, some efforts for improvement may be necessary.

## So, finally getting to the main point:

As a suggestion to reduce the likelihood of emails being placed in the spam folder, how about excluding individuals who haven’t opened emails for 180 days? Those who haven’t engaged with emails for such a period are at a higher risk of being marked as spam in the future.

The choice of 180 days is not explicitly mentioned in the guidelines linked in the previous help document. However, this timeframe is referenced based on a recommendation by Knox Henry from Salesforce within the Trailblazer Community, so we are using that as a reference.

Whether the 180-day period feels long or short may vary by company, so adjusting the duration based on individual preferences might be a good idea.

Additionally, the decision to exclude only “individual Google accounts” or extend it to all domains may vary by company. However, the criteria set by Google and Yahoo in this instance are likely to **become a “De Facto Standard” for future email sending**. Considering this opportunity, it might be advisable to implement it for all domains. This is my opinion for your consideration.

Now, let’s try to extract “subscribers who haven’t opened an email in 180 days.” This SQL query uses the “Sent” and “Open” data views, which only retain data for the past 6 months. Therefore, if these data views has not been accumulated until now, extracting subscribers who haven’t opened an email in the last 180 days will essentially result in “0” or a value close to “0”.

\* If you wish to test this immediately, **consider changing it to “subscribers who haven’t opened an email in 90 days”** or a similar timeframe for testing.

\* **The scenario described in this article may not be suitable for businesses engaged in large-scale email sendings**. As the volume of data related to email sending and opening histories increases, managing such data becomes challenging, and there is also a risk of potential timeouts in SQL query activities.

## 1. Accumulation of “Sent” History Data

Referring to the help document of the **“Sent data view”** below, obtain the item names, data types, and data lengths to create a data extension for storage.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=ja&id=sf.mc_as_data_view_sent.htm&type=5&source=post_page-----27c0d1c9bb80---------------------------------------)

The data extension name will be **“Sent”**.

Set the **primary key** as follows. Other items can allow NULL.

- JobID  
- ListID  
- BatchID  
- SubscriberID  
- SubscriberKey  
- EventDate

Using the following SQL, store all the sent data for the past 6 months by **“run once”**.

If no specific conditions are specified, the system will automatically store data for the last 6 months. However, for businesses engaged in large-scale email sends, it may not be possible to store all the data at once. In such cases, please use the EventDate to divide the time period and insert the data in multiple batches.

```
SELECT * FROM _sent
```

After inserting data for the past 6 months, only the incremental data is required. Use the following SQL to **“update” (add/update) data for the current day and the previous day**.

**Please configure the following SQL query activity later in Automation Studio**.

```
SELECT * FROM _sent  
WHERE CONVERT(Date,Dateadd(hh,15,EventDate),111) = CONVERT(Date,Dateadd(hh,15,Getdate()),111)  
OR CONVERT(Date,Dateadd(hh,15,EventDate),111) = CONVERT(Date,Dateadd(hh,-9,Getdate()),111)
```

\* In my country, Japan, the timezone is JST (Japan Standard Time), and there is a 15-hour time difference with CST. Therefore, for the current day, 15 hours are added, and for the previous day, 9 hours are subtracted. Please adjust these according to the timezone in your country.

## 2. Accumulation of “Open” History Data

Referring to the help document of the **“Open data view”** below, obtain the item names, data types, and data lengths to create a data extension for storage.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_as_data_view_open.htm&type=5&source=post_page-----27c0d1c9bb80---------------------------------------)

The data extension name will be **“Open”**.

Set the **primary key** as follows. Other items can allow NULL.

- JobID  
- ListID  
- BatchID  
- SubscriberID  
- SubscriberKey  
- EventDate

Using the following SQL, store all the open data for the past 6 months by **“run once”**.

If no specific conditions are specified, the system will automatically store data for the last 6 months. However, for businesses engaged in large-scale email sends, it may not be possible to store all the data at once. In such cases, please use the EventDate to divide the time period and insert the data in multiple batches.

```
SELECT * FROM _open
```

After inserting data for the past 6 months, only the incremental data is required. Use the following SQL to **“update” (add/update) data for the current day and the previous day**.

**Please configure the following SQL query activity later in Automation Studio**.

```
SELECT * FROM _open  
WHERE CONVERT(Date,Dateadd(hh,15,EventDate),111) = CONVERT(Date,Dateadd(hh,15,Getdate()),111)  
OR CONVERT(Date,Dateadd(hh,15,EventDate),111) = CONVERT(Date,Dateadd(hh,-9,Getdate()),111)
```

\* In my country, Japan, the timezone is JST (Japan Standard Time), and there is a 15-hour time difference with CST. Therefore, for the current day, 15 hours are added, and for the previous day, 9 hours are subtracted. Please adjust these according to the timezone in your country.

## 3. Extracting Subscribers Who Haven’t Opened Emails in 180 Days

With this, the mechanism to accumulate the history data of sent and opened emails has been established. Now, you just need to execute the following SQL for these history data. First, let’s prepare a data extension to store subscribers who haven’t opened emails in 180 days.

- **Id** … Subscriber key will be stored here.
- **First\_Sent\_Date** … Stores the initial sending date within the sent history data.
- **First\_Sent\_Date\_Plus** … Stores the date obtained by adding 180 days to the above initial sending date.
- **Last\_Open\_Date** … Stores the last opened date.

Now, let’s input the data using the following SQL. If the data extension name and item names are the same as those I created, you can simply copy and paste.

```
SELECT  
    sentInfo.Id,  
    sentInfo.First_Sent_Date,  
    sentInfo.First_Sent_Date_Plus,  
    openInfo.Last_Open_Date  
FROM (  
    SELECT  
        sent.Subscriberkey as Id,  
        CONVERT(DATE, DATEADD(HOUR, 15, sent.Eventdate), 111) as First_Sent_Date,  
        CONVERT(DATE, DATEADD(DAY, 180, DATEADD(HOUR, 15, sent.Eventdate)), 111) as First_Sent_Date_Plus  
    FROM (  
        SELECT  
            *,  
            ROW_NUMBER() OVER (PARTITION BY s.Subscriberkey ORDER BY s.Eventdate ASC) as ROW_NUMBER  
        FROM [Sent] s  
    ) as sent  
    WHERE sent.ROW_NUMBER = 1  
) sentInfo  
LEFT OUTER JOIN (  
    SELECT  
        openEvent.Subscriberkey as Id,  
        CONVERT(DATE, DATEADD(HOUR, 15, openEvent.Eventdate), 111) as Last_Open_Date  
    FROM (  
        SELECT  
            *,  
            ROW_NUMBER() OVER (PARTITION BY oEvent.Subscriberkey ORDER BY oEvent.Eventdate DESC) as ROW_NUMBER  
        FROM [Open] oEvent  
    ) as openEvent  
    WHERE openEvent.ROW_NUMBER = 1  
) openInfo ON sentInfo.Id = openInfo.Id  
WHERE  
    sentInfo.Id NOT IN (  
        SELECT DISTINCT notOpened.Id  
        FROM (  
            SELECT  
                openNotSubscriber.Subscriberkey as Id,  
                CONVERT(DATE, DATEADD(HOUR, 15, openNotSubscriber.Eventdate), 111) as Last_Open_Date  
            FROM (  
                SELECT  
                    *,  
                    ROW_NUMBER() OVER (PARTITION BY oNotSubscriber.Subscriberkey ORDER BY oNotSubscriber.Eventdate DESC) as ROW_NUMBER  
                FROM [Open] oNotSubscriber  
            ) as openNotSubscriber  
            WHERE openNotSubscriber.ROW_NUMBER = 1  
        ) notOpened  
        WHERE DATEDIFF(DAY, notOpened.Last_Open_Date, CONVERT(DATE, DATEADD(HOUR, 15, GETDATE()), 111)) <= 180  
    )  
    AND sentInfo.First_Sent_Date_Plus <= CONVERT(DATE, DATEADD(HOUR, 15, GETDATE()), 111)
```

\* In my country, Japan, the timezone is JST (Japan Standard Time), and there is a 15-hour time difference with CST. Therefore, 15 hours are added to the system time. Please adjust these according to the timezone in your country.

\* As mentioned earlier, if you haven’t accumulated history data so far, running this SQL will generally result in “0” records. This is because it targets subscribers whose first sending date from the accumulated sent data has passed 180 days. If you want to check any results immediately, you can change the number “180” in the SQL to, for example, “90”.

\* In the case of large-scale senders, if the number of records is too high, SQL may not be able to execute within the allotted time.

In the future, if the accumulation of history data proceeds smoothly, you can extract the relevant subscribers as follows:

Finally, once these three SQL query activities are ready, set up automation in Automation Studio as shown below to complete the process:

After that, whether to exclude these subscriber data from the delivery master or import it into the Auto-Suppression List depends on your company’s operation.

And since this entire discussion is related to email sending, if Salesforce Marketing Cloud is also used for cross-channel utilization, such as LINE or SMS, please be careful about how you exclude this subscriber data, ensuring that you don’t exclude more than just email-related data.

## **As a final remark…**

This is quite important, but it’s worth noting that tracking the opening of emails for recipients using Apple’s standard Mail app or the Gmail app may not be accurate. I have already addressed this in an article on my end, so please review it again for further details.

[## Apple’s Mail Privacy Protection (MPP) — A Overview of the September 2021 Release

### The “Mail Privacy Protection” feature released in September 2021 by Apple holds significant importance in the realm of…

medium.com](/@marketingcloudtips/apples-mail-privacy-protection-mpp-a-overview-of-the-september-2021-release-1054a719f8cd?source=post_page-----27c0d1c9bb80---------------------------------------)

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
