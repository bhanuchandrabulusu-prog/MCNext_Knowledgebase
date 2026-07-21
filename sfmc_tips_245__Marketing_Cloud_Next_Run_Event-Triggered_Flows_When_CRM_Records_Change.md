# SFMC Tips #245 : Marketing Cloud Next: Run Event-Triggered Flows When CRM Records Change

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-run-event-triggered-flows-when-crm-records-change-a3a05691b427

---

# SFMC Tips #245 : Marketing Cloud Next: Run Event-Triggered Flows When CRM Records Change

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a3a05691b427---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a3a05691b427---------------------------------------)

6 min read

·

Feb 6, 2026

--

Photo by [Nasrin Pakari](https://unsplash.com/@nasrinpakari?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition, **it is now possible to start an event-triggered flow when records of Contacts, Leads, or Prospects are changed, or when objects related to them are updated**.

This enables real-time detection of actions in the CRM and allows marketing initiatives to be executed at that very moment.

## Usage Image

For example, the following scenarios can be realized:

- **Case closed** ⇒ Immediately send a personalized email to the Contact
- **Opportunity stage updated** ⇒ Send a follow-up notification to the Lead owner
- **Specific field value changed** ⇒ Automatically create tasks or send messages

In this way, actions can be executed immediately after important business events occur for customers or owners, enabling timely and highly personalized communication.

Therefore, in this article, I would like to try the scenario:  
**“Case closed ⇒ Immediately send a personalized email to the Contact.”**

## Configuration Steps

### 1. Create an Event-Triggered Flow

Select **Event-Triggered Flow** in a new flow.

### 2. Select the Trigger Type

From the event library, select **“Prospect, Lead, Contact or Related Record Change”.**

### 3. Specify the Target Object

Select Contact, Lead, Prospect, or objects related to them.  
This time, select the **Case** object. Also select the related **Contact ID**.

### 4. Set Entry Conditions

Set the entry condition so that the flow is triggered when the case becomes **Closed**.

> ***Tips:*** *Triggered records are automatically generated as variables in the flow resources and can be referenced directly in subsequent actions using* `{!$Input.***}`*.*

At this point, save the flow to configure the email.

### 5. Configure Apex Class

Next, we would like to begin creating an email that includes case information.  
However, currently, start event data cannot be used directly as the email data source, so we use **Apex Class Data Provider**.

This time, prepare the following Apex code. It acts like a “container”.

```
public without sharing class CaseMailPayload {  
    @AuraEnabled public String CaseNumber { get; set; }  
    @AuraEnabled public String CaseSubject { get; set; }  
    @AuraEnabled public String LastName { get; set; }  
    @AuraEnabled public String FirstName { get; set; }  
    @AuraEnabled public String CompletedDateJp { get; set; }  
    @AuraEnabled public String CompletedDateSlash { get; set; }  
}
```

Register this code as an Apex class.

### 6. Configure the Data Source

After registering the Apex class, open a new email and click **Add Data Source**.

### 7. Select Apex Class

Choose **Apex Class Data Provider** and select the Apex class configured earlier.

### 8. Create the Email

Use the following email template.

```
--- Subject  
[Completed] Your Support Case Has Been Resolved ({{CaseNumber}})  
  
--- Body  
Dear {{FirstName}} {{LastName}},  
  
Thank you for contacting our support team.  
We’re pleased to inform you that your case has now been successfully resolved.  
  
━━━━━━━━━━━━━━━━━━━  
Case Number: {{CaseNumber}}  
Subject: {{CaseSubject}}  
Completed At: {{ClosedDate}}  
━━━━━━━━━━━━━━━━━━━  
  
If you have any additional questions or need further assistance, please feel free to reply to this email or contact our support team at any time.  
  
We appreciate your continued trust and look forward to assisting you again.  
  
Best regards,  
Customer Support Team
```

### 9. Replace Placeholders with Apex Class Data Provider Fields

Replace the placeholders in the template with the fields obtained from Apex Class Data Provider.  
Change the email to **Transactional Email**, then **Save** and **Publish**.

### 10. Create a “Variable” Resource in Flow

After publishing the email, reopen the flow and create an **Apex-Defined** variable.

- API Name: varPayload (any name)
- Data Type: **Apex-Defined**
- Apex Class: the one created above
- Check “**Available for input**”

### 11. Create Formulas

Create the following as **Formula** resources.  
These display the case last modified date (case closed date) in slash format and Japanese format.

**a. Slash format (yyyy/MM/dd HH:mm)**

- API Name: fxCompletedDateTimeSlash
- Data Type: Text

```
TEXT(YEAR(DATEVALUE({!$Input.LastModifiedDate}))) & "/" &  
RIGHT("0" & TEXT(MONTH(DATEVALUE({!$Input.LastModifiedDate}))), 2) & "/" &  
RIGHT("0" & TEXT(DAY(DATEVALUE({!$Input.LastModifiedDate}))), 2) & " " &  
RIGHT("0" & TEXT(HOUR(TIMEVALUE({!$Input.LastModifiedDate}))), 2) & ":" &  
RIGHT("0" & TEXT(MINUTE(TIMEVALUE({!$Input.LastModifiedDate}))), 2)
```

**b. Japanese format (yyyy年MM月dd日 HH:mm)**

- API Name: fxCompletedDateTimeJp
- Data Type: Text

```
TEXT(YEAR(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))) & "年" &  
RIGHT("0" & TEXT(MONTH(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & "月" &  
RIGHT("0" & TEXT(DAY(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & "日 " &  
RIGHT("0" & TEXT(HOUR(TIMEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & ":" &  
RIGHT("0" & TEXT(MINUTE(TIMEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2)
```

> *※ Only the Japanese format includes a conversion from UTC to JST. (+ 9h)*

### 12. Assign Values in Assignment Element

Place an **Assignment** element and assign:

- Information obtained from the flow
- The formulas above

to each variable defined in the Apex class.

> *※ As mentioned earlier, you can use the triggered case record without configuring “Get Records”.*

### 13. Place Marketing Cloud Email

After assignment, place **Marketing Cloud Email** in the next path, then **Save** and **Activate**.

### 14. Update the Case to Trigger the Flow

After activating the flow, change the case status to **Closed**.  
The flow will be triggered as shown below.

### 15. Check the Received Email

The email is received simultaneously.  
Personalization also worked correctly. Success!!

![]()

## Conclusion

Until now, record triggers mainly included:

- Email engagement
- Engagement signals
- Real-time data graph events
- Journey Builder events

With this update, being able to directly use **“CRM changes themselves”** as triggers is a very significant evolution.

Conceptually, it feels similar to the “**Salesforce entry source**” in Journey Builder of Marketing Cloud Engagement.

Marketing Cloud Next is a marketing platform designed with strong affinity to CRM, so this feature fits perfectly.

Please try using it for daily automation and real-time initiatives.

I explain the “automation of consent” using this mechanism in the following article.

[## SFMC Tips #142 : Marketing Cloud Next : Automating Consent Creation

### In the Summer ’25 new feature release for Marketing Cloud Next Growth & Advanced Editions, the “Create Consent”…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-custom-unsubscribe-links-78649b12da0e?source=post_page-----a3a05691b427---------------------------------------)

In addition, the Summer ’26 new feature release introduced the **Content Variables** feature, which makes it possible to implement similar use cases without using Apex. As a result, marketers can now build these implementations with a much simpler configuration.

For more details, please refer to the following.

[## SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it became possible to add…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911?source=post_page-----a3a05691b427---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
