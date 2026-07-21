# SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911

---

# SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--18ebb6764911---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--18ebb6764911---------------------------------------)

6 min read

·

May 11, 2026

--

Photo by [Zhang Yi](https://unsplash.com/@mianmian1997?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for **Marketing Cloud Next Growth & Advanced Editions**, it became possible to add merge fields to messages based on a new data source called **“Content Variables”.**

When marketers hear the term **“Content Variables”,** it may sound a little unfamiliar at first. However, in my understanding, it is easier to imagine them as something similar to **“Personalization Strings”** in **Marketing Cloud Engagement** that are defined and used as needed.

Of course, Marketing Cloud Next also supports personalization through **Data Graphs**, but one of the key characteristics of **Content Variables** is that values can be retrieved and utilized in a more real-time manner.

In a previous article, when testing the scenario **“Case Closed ⇒ Immediately Send a Personalized Email to the Contact”,** I adopted a structure where an **“Apex-Defined” variable** was created, and values were passed to the content side using an **Apex Class Data Provider**.

However, this method was a **developer-centric approach**, which made it somewhat difficult for marketers to handle.

[## SFMC Tips #245 : Marketing Cloud Next: Run Event-Triggered Flows When CRM Records Change

### In the Spring ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, it is now possible to start an…

medium.com](/@marketingcloudtips/marketing-cloud-next-run-event-triggered-flows-when-crm-records-change-a3a05691b427?source=post_page-----18ebb6764911---------------------------------------)

With the **“Content Variables”** feature added in the **Summer ’26** new feature release, this entire process can now be implemented **without Apex**, enabling **low-code personalization**.

As a result, marketers themselves can utilize customer data and control messages in a more flexible and proactive manner.

This time, I will test this new feature using exactly the same **“Case Completion Notification Email”** scenario as in the previous article.

## Setup Procedure

## Content Setup

1. In the previous article, preparation started from the flow side first, but with this feature, configuration begins from the content side.

This time as well, the following email template will be used.

**Subject:**  
**[Completed] Your Inquiry Has Been Resolved ({{CaseNumber}})**

**Body:**  
{{LastName}} {{FirstName}},

Thank you very much for your continued support.  
We would like to inform you that the inquiry you submitted has now been resolved.

━━━━━━━━━━━━━━━━━━━  
 ■ **Case Number** : {{CaseNumber}}  
 ■ **Subject** : {{CaseSubject}}  
 ■ **Completion Date** : {{ClosedDate}}  
 ━━━━━━━━━━━━━━━━━━━

If you have any questions or additional inquiries regarding this matter,  
please feel free to reply to this email or contact our support desk.

We will continue striving to provide even better support in the future,  
and we appreciate your continued support.

2. After entering the content into the paragraph component, open the **“Data Source”** tab.

3. In the **“Add Content Variable”** section, click the **“Add”** button.

4. The following five **“Content Variables”** will be used this time. Create each one from the screen.

- **Case Number** : `CaseNumber` (**Text Type**)
- **Case Subject** : `CaseSubject` (**Text Type**)
- **Completion Date** : `ClosedDate` (**Text Type**)
- **Last Name** : `LastName` (**Text Type**)
- **First Name** : `FirstName` (**Text Type**)

※ For **Completion Date**, using a **text type** instead of a **date type** allows flexible control over the display format.

5. Once **Content Variables** are configured, they become available as merge fields within the email message.

![]()

6. After insertion, it will look like the following.

*In cases like this, instead of inserting them from the merge field picker, they can also be used directly by writing* ***“$content.”*** *manually.*

![]()

7. Once the message is complete, **save and publish** it.

## Flow Setup

1. From the **“Build Your Own”** tab, open **“Event Triggered Flow”.**

2. Open **Flow Builder**.

3. Click the **start element** and select **“Prospect, Lead, Contact or Related Record Change”** from the event library.

4. This time as well, select the **“Case”** object, and under it specify **“Contact ID”.**

5. Then configure the **entry conditions** so that the flow starts when the case becomes **“Closed”.**

***Tips:*** *Fields from the triggered record itself are automatically generated as variables and can be directly referenced in subsequent actions. They are displayed as* ***“{!$Input.****\*}”\*\*.*

*※ In this flow type,* ***fields from related objects cannot be used.***

6. Next, since this flow cannot directly access **Contact information**, place a **“Get Records”** element and retrieve the Contact information using the **Contact ID** associated with the Case.

7. Next, configure the **Marketing Cloud email action**.  
Set the display name and select the email message created earlier.

8. When selecting an email configured with **“Content Variables”,** an input area for **“Content Variables”** appears at the bottom.

Assign resources to each variable here.

**Description of Each Resource**

① **CaseNumber**  
 Use **“Case Number”** from the **Case object**

② **CaseSubject**  
 Use **“Subject”** from the **Case object**

③ **ClosedDate**  
 **Formula Resource**  
 ※ Japanese format (**yyyy/MM/dd HH:mm**)

- **API Name:** `fxCompletedDateTimeJp` (arbitrary)
- **Data Type:** `Text`

```
TEXT(YEAR(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))) & "/" &  
RIGHT("0" & TEXT(MONTH(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & "/" &  
RIGHT("0" & TEXT(DAY(DATEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & " " &  
RIGHT("0" & TEXT(HOUR(TIMEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2) & ":" &  
RIGHT("0" & TEXT(MINUTE(TIMEVALUE({!$Input.LastModifiedDate} + (9/24)))), 2)
```

④ **FirstName**  
 Use **“First Name”** retrieved by **“Get Records”** above

⑤ **LastName**  
 Use **“Last Name”** retrieved by **“Get Records”** above

![]()

9. Once the **“Content Variables”** assignment is complete, select the **“From Address”** and configure **“Communication Subscription”** if necessary.

10. Finally, **save and activate** the flow.

## Complete the Case and Send the Email

1. After activating the flow, change the case status to **“Closed”.**As shown below, the flow will be triggered.

![]()

2. The email was actually sent successfully, and I was able to confirm that the content was personalized correctly. **Success!!**

![]()

## Conclusion

My personal impression is that the implementation effort itself does not feel dramatically different compared to using **Apex**. However, for marketers who feel resistance toward Apex, being able to build personalized emails **without code development** is a very significant advantage.

Also, this mechanism can be used across various flow types, but the types of resources available and their behavior have unique characteristics depending on the flow. Therefore, I recommend testing thoroughly while confirming which resources and send conditions are actually available.

Furthermore, by combining this kind of notification email with **“Conversational Email”,** it becomes possible to automatically handle additional questions and inquiries via replies.

I explain **Conversational Email** in detail in the following article.

[## SFMC Tips #281 : Marketing Cloud Next: How to Set Up Conversational Email

### Conversational Email has been introduced as a Spring ’26 new feature of Marketing Cloud Next Advanced Edition (\*this…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-set-up-conversational-email-0ef29d7fd113?source=post_page-----18ebb6764911---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
