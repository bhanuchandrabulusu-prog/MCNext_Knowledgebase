# SFMC Tips #260 : Marketing Cloud Next: Distributed Marketing & Alerts

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-distributed-marketing-alerts-9182444afd2f

---

# SFMC Tips #260 : Marketing Cloud Next: Distributed Marketing & Alerts

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9182444afd2f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9182444afd2f---------------------------------------)

5 min read

·

Feb 27, 2026

--

Photo by [Hristina Šatalova](https://unsplash.com/@hristinash?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Distributed Marketing & Alerts** has been released as a new feature in the [Spring ’26 release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition.

*Note: This feature is a* ***paid feature*** *(from $50 per user/month).*

**Distributed Marketing** is a mechanism that allows sales representatives, instead of sending individually designed emails with their own layouts, to use “**brand-governed personalized email templates**” pre-created by the marketing department and deliver them through flows from customer record pages in CRM (Service Cloud or Sales Cloud).

This enables field sales representatives to easily execute communications optimized for each individual customer while adhering to brand guidelines.

In this article, I will explain the setup procedure for Distributed Marketing & Alerts.

## Setup Steps

### 1. Enable Distributed Marketing

1. Go to [Setup] > [**Distributed Marketing and Alerts**] and enable the feature.

### 2. Grant Permissions to Users

1. Assign the following permission sets to users who will actually send emails (such as sales representatives):

- **Marketing Cloud Manager**
- **Send Distributed Marketing Messages**

### 3. Add Component to Record Pages

1. Open [Setup] > [**Lightning App Builder**], and add the **“Distributed Messages” component** to each of the following record pages:

- Contact
- Lead
- Prospect

2. After saving, the **Send Distributed Messages button** will appear on each record page.

### 4. Create an Email Template

1. Create an “**Email Template**”.

2. If you use merge fields,  
select [**Data Source**] tab > [**Event Data Provider**] > “**Distributed Marketing and Alerts Message**”.

> ***⚠ Note*** *Although the message will be sent later using an Event-Triggered Flow, due to flow specifications,* ***if you use merge fields from Data Graph, a wait element of more than 24 hours is required immediately before sending the email****.  
> If this is not configured, an error like the following will occur and activation will not be possible.*

3. Place “merge fields” using the configured data source.

4. If necessary, you can unlock specific content blocks and define the editable range for sales representatives.

> *In this example, only the name in the footer is allowed to be edited.*

5. Once the template is complete, save and publish it.

### 5. Create an Event-Triggered Flow

1. On the new campaign flow screen, select “**Blank Event**” to start creating a trigger flow.

2. As the first event, select “**Distributed Marketing and Alerts Message**”.

3. Next, add “**Send Email Message**”.

4. Because “**Distributed Marketing and Alerts Message**” is set as the event source, the **“Email Template” becomes selectable**.  
Select the template created earlier.

5. Save and activate the flow.

### 6. Actual Sending

1. Return to the Contact record page and click the **Send Distributed Messages button**.

2. The configured email template will be displayed. Select and open it.

3. In this configuration, only the name in the footer is editable. All other content is locked and cannot be edited.

4. Enter your name and proceed.

5. After final confirmation, send the message.

6. A **brand-governed personalized email** has been sent.

The setup is now complete.

## Conclusion

This feature is particularly effective for organizations that place strong emphasis on brand guidelines. On the other hand, it is not something that every company is required to use. In fact, even in Marketing Cloud Engagement, it has not necessarily been a feature that was widely or actively adopted in practice.

I encourage you to explore how it can be applied within your own real-world use cases and consider leveraging it where it adds value.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
