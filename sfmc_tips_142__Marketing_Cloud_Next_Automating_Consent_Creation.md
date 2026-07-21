# SFMC Tips #142 : Marketing Cloud Next : Automating Consent Creation

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-leveraging-custom-unsubscribe-links-78649b12da0e

---

# SFMC Tips #142 : Marketing Cloud Next : Automating Consent Creation

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--78649b12da0e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--78649b12da0e---------------------------------------)

11 min read

·

Jun 19, 2025

--

Photo by [Sasha Kaunas](https://unsplash.com/@akaunas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth and Advanced Editions, when you want to automatically create **Consent** records based on record creation or updates, using the **Prospect, Lead, Contact or Related Record Change** event-triggered flow is the simplest and easiest-to-understand approach.

On the other hand, the same functionality can also be implemented by using a **Data Cloud Triggered Flow**. Both approaches can automatically create and update consent records, but they differ in their trigger mechanisms, available capabilities, and design considerations.

In this article, using **Contact creation** and **email address changes** as examples, I will primarily explain how to implement this using an event-triggered flow, while also comparing it with a Data Cloud Triggered Flow and discussing the characteristics of each approach.

## Unsupported Methods for Creating Consent Records

Salesforce provides an [official Help document](https://help.salesforce.com/s/articleView?id=005316463&type=1) for creating consent records and warns against using unsupported methods.

Currently, the following two approaches are officially supported:

1. **Event-Triggered Flow**
2. **Data Cloud Triggered Flow**

In contrast, creating consent records by using the following Flow Actions is **not supported**:

- `MessagingConsent.MessagingConsent`
- `MessagingConsentV2.MessagingConsent`

If you use these unofficial actions, the consent records may appear to be created successfully, but the actual email sending behavior may become inconsistent with the consent status.

For example, situations like the following may occur:

- The consent record is **Opt In**, but emails cannot actually be sent.
- The consent record is **Opt Out**, but emails can still be sent.

To avoid these inconsistencies, it is recommended that consent records be created only by using methods officially supported by Salesforce.

## The Option to Disable Consent Management

Marketing Cloud Next also provides an option to disable the standard consent management feature itself.

[## SFMC Tips #168 : Marketing Cloud Next: Disabling Consent Management

### Marketing Cloud Next Growth & Advanced Edition comes with a built-in Consent Management mechanism as standard. For…

medium.com](/@marketingcloudtips/marketing-cloud-next-disabling-consent-management-41d58a4acbef?source=post_page-----78649b12da0e---------------------------------------)

Of course, it is technically possible to disable this setting and operate without creating any consent records.

However, if you do so, Marketing Cloud Next can no longer properly process unsubscribe requests submitted through **List Unsubscribe**. In other words, even if recipients unsubscribe from their email client, that information is not reflected in consent management and is effectively ignored.

Therefore, even if you do not use the standard unsubscribe link or Preference Center, it is still recommended to create **Opt In** consent records for at least the email addresses that will receive your email communications.

Personally, I believe that, in an environment where promotional emails are sent, completely avoiding Marketing Cloud Next’s standard consent management is not a very practical option at this time. 🤔

## ① Configuring an Event-Triggered Flow

The configuration introduced in this section is a simple implementation example that automatically creates an **Opt In** consent record for a new email address.

> ***Note:***Event-Triggered Flows do not support **$Record\_\_Prior** or **Is Changed**, which are available in Record-Triggered Flows. Therefore, they cannot implement logic based on comparing the current value with the previous value.

1. Create a new Event-Triggered Flow.

2. Select **Prospect, Lead, Contact or Related Record Change** as the event.

3. Configure the Contact object as follows.

- **Object:** Contact
- **Trigger Condition:** When a record is created or updated

- **Entry Condition:** Email (Field) · is Null (Operator) · False (Value)

> To ensure that consent records can also be created or updated when the email address changes, select **Every time a record is updated and meets the condition requirements**.
>
> If you select **Only when a record is updated to meet the condition requirements**, the flow won’t run again because the record continues to meet the condition even after the email address changes.

4. Next, add a **Get Records** element and search the **Communication Subscription Consent** DMO by using the email address of the triggered Contact.

- **Element Name (Example)**Get Consent Records
- **Data Source**Data Cloud Object
- **Data Cloud Object**Communication Subscription Consent
- **Search Condition**Communication Subscription Consent > Contact Point Value  
   Equals  
  {!$Input.Email}

> Since this is an implementation example for an Event-Triggered Flow, it assumes that there is only one Communication Subscription. For scenarios where multiple Communication Subscriptions are managed, refer to the Data Cloud Triggered Flow implementation example introduced later in this article.

The following settings can remain at their default values.

- Sort Records
- How Many Records to Store
- How to Store Record Data

5. Next, add a **Decision** element to determine whether the consent record already exists.

- **Element Name (Example)**Has Existing Consent Record
- **Outcome Name (Example)**Has Existing Consent Record
- **Condition**{!Get\_Consent\_Records.ssot\_\_ContactPointValueText\_\_c}  
   Equals  
  {!$Input.Email}

6. Add a **Create Consent** element to the default path of the Decision element (when no existing record is found).

7. Configure the required fields. (Adjust the configuration according to your organization’s consent policy.)

After completing the configuration, save and activate the flow.

### Error When Saving the Flow

You may see the following error when saving the flow:

- **Complete required fields.**
- If this error occurs even though the configuration is correct, reopening the **Create Consent** element and configuring it again may resolve the issue. In particular, verify that the **Communication Subscription** setting has not been removed during the save process.
- If the issue still persists, save the flow, close it, reopen it, and configure it again. In some cases, the flow can then be saved successfully.

## ② Configuring a Data Cloud Triggered Flow

There are two major advantages to using a Data Cloud Triggered Flow.

### 1. You do not need to create a flow for each data source

With an Event-Triggered Flow, you must create a separate flow for each data source that acts as the trigger, such as Contact or Lead.

In contrast, a Data Cloud Triggered Flow executes processing based on the Unified Data Model, allowing you to implement common logic in a single flow without having to consider differences between Contacts, Leads, Person Accounts, and other record types.

As a result, this provides a significant maintenance advantage in environments that handle multiple data sources or use Person Accounts.

### 2. You can use $Record\_\_Prior

Another major advantage is that Data Cloud Triggered Flow supports **$Record\_\_Prior** (the record before the change), which is not available in Event-Triggered Flow.

This is a very important feature for consent management when an email address is changed.

For example, if the Communication Subscription associated with the previous email address was **Opt Out**, it is not appropriate to automatically create an **Opt In** consent record for the new email address.

By using **$Record\_\_Prior**, you can branch the processing while referencing the previous email address and its consent status, preventing this type of unintended re-opt-in.

In this article, I take advantage of this feature and explain a configuration example in which an Opt In consent record is **not** created for the new email address when the previous email address was Opt Out.

> **Note: $Record\_\_Prior** is always **NULL** during debug execution. Therefore, this decision logic cannot be validated correctly in the Flow Debug screen.
>
> To verify the behavior, update an actual record to execute the flow, and perform testing in a production environment or a test environment that closely resembles production.

The configuration introduced in this article is an implementation example designed to create an **Opt In** consent record for the new email address only when the previous email address was **not** Opt Out.

Of course, consent management rules vary from company to company, so this logic is not the only correct solution. Adjust the conditions and processing according to your actual requirements and operational policies.

1. Create a new Data Cloud Triggered Flow.

2. Configure the Start element as follows.

- **Object:** Contact Point Email DMO
- **Trigger Condition:** When a record is created or updated
- **Entry Conditions:** None

> **Important: Data Cloud Triggered Flow Behavior**
>
> The important point is that the trigger does **not** fire simply because records are added to or removed from this DMO. What is actually monitored is whether the source profile data (such as Contact or Lead) that feeds the data stream has been created or updated. What matters is whether there is a difference between the current data and the previous data in the data stream.
>
> Although you can add or remove records from the DMO by using Data Space Filters, doing so does not create any differences in the data stream. Therefore, the flow is not triggered in this case. If you want to trigger the flow, create or update the target record in CRM.

3. First, add a **Get Records** element to retrieve the consent record associated with the previous email address.

- **Element Label (Example)**Get Previous Consent Record
- **Data Source**Data Cloud Object
- **Data Cloud Object**Communication Subscription Consent
- **Filter Conditions**① Communication Subscription Consent > **Contact Point Value**  
   Equals  
  {!$Record\_\_Prior.ssot\_\_EmailAddress\_\_c} (Previous Email Address)  
   AND  
  ② Communication Subscription Consent > **Communication Subscription Channel Type**  
   Equals  
  0eBdL0000001xpFUAQ (18-character Communication Subscription ID beginning with 0eB)

In this example, multiple Communication Subscriptions are assumed to exist, so **Communication Subscription Channel Type** is also included in the filter conditions.

The following settings can remain at their default values.

- Sort Records
- How Many Records to Store
- How to Store Record Data

4. Next, add a **Decision** element to determine whether the previous consent record is **OPT\_OUT**.

- **Element Label (Example)**Has Previous Consent Record
- **Outcome Names (Example)**Consent Record Found (Left Path)  
  No Consent Record (Right Path)
- **Condition**Get Previous Consent Record > **Consent Status**  
   Equals  
  OPT\_OUT

The flow now looks like this.

![]()

5. Next, add a **Get Records** element to the **No Consent Record** path on the right to retrieve the consent record for the current (updated or new) email address.

![]()

- **Element Label (Example)**Get Current Consent Record
- **Data Source**Data Cloud Object
- **Data Cloud Object**Communication Subscription Consent
- **Filter Conditions**① Communication Subscription Consent > **Contact Point Value**  
   Equals  
  {!$Record.ssot\_\_EmailAddress\_\_c} (Updated or New Email Address)  
   AND  
  ② Communication Subscription Consent > **Communication Subscription Channel Type**  
   Equals  
  0eBdL0000001xpFUAQ (18-character Communication Subscription ID beginning with 0eB)

The following settings can also remain at their default values.

- Sort Records
- How Many Records to Store
- How to Store Record Data

6. Next, add a **Decision** element to determine whether a consent record already exists for the current email address.

- **Element Label (Example)**Has Current Consent Record
- **Outcome Names (Example)**Consent Record Found (Left Path)  
  No Consent Record (Right Path)
- **Condition**Get Current Consent Record > **Communication Subscription Consent Id**  
   Is Blank  
  False

The flow now looks like this.

![]()

7. Add a **Create Consent** action to the **No Consent Record** path on the right.

8. Configure it as follows.

- **Element Label (Example)**Opt In (0eBdL0000001xpFUAQ)
- **Consent Status**Opt In
- **Contact**{!$Record.ssot\_\_EmailAddress\_\_c} (Updated or New Email Address)
- **Channel**Email
- **Communication Subscription**Select the Communication Subscription that matches the 18-character ID selected above.

9. Next, add a **Create Consent** action to the left (**Consent Record Found**) path. This action creates an **Opt Out** record.

- **Element Label (Example)**Opt Out (0eBdL0000001xpFUAQ)
- **Consent Status**Opt Out
- **Contact**{!$Record.ssot\_\_EmailAddress\_\_c} (Updated or New Email Address)
- **Channel**Email
- **Communication Subscription**Select the Communication Subscription that matches the 18-character ID selected above.

> **Note:** Do not omit this Opt Out process. If this process is omitted, when the email address is changed again (the second change or later), the previous Opt Out status cannot be carried over, and the processing may incorrectly proceed to the Opt In path.

10. Once you have completed the configuration up to this point, save the flow.

11. The series of processes created here applies to a single Communication Subscription.

If you use multiple Communication Subscriptions, simply copy the process inside the red box and configure it for each Communication Subscription ID.

12. For example, if you use three Communication Subscriptions, arrange the same process in sequence as shown below.

> **Note:** Copying the elements alone does not completely carry over all settings.
>
> In particular, the **Decision** elements must be reconfigured so that they reference the preceding **Get Records** element. After copying, always verify the references for each element.

![]()

The configuration is now complete.

### Error When Saving the Flow

You may see the following error when saving the flow:

- **Complete required fields.**
- If this error occurs even though the configuration is correct, reopening the **Create Consent** element and configuring it again may resolve the issue. In particular, verify that the **Communication Subscription** setting has not been removed during the save process.
- If the issue still persists, save the flow, close it, reopen it, and configure it again. In some cases, the flow can then be saved successfully.

## Conclusion

Creating consent records is one of the most widely discussed topics in Marketing Cloud Next. In reality, there is no single correct solution that applies to every situation. The optimal design and implementation should be selected based on each company’s consent management policy, data model, and operational requirements.

For that reason, I hope you will use the content introduced in this article not as the **only best practice**, but as **one example of an implementation pattern**.

Personally, if flexibility is your priority, I find that using a Data Cloud Triggered Flow is easier to work with. In particular, the ability to use **$Record\_\_Prior** is a significant advantage, as it enables safer control, such as carrying over the consent status when an email address is changed.

On the other hand, if your requirement is simple — for example, you only want to create a consent record when a new record is created — an Event-Triggered Flow based on CRM records may be easier to implement. This is especially true if you are already familiar with CRM Flows, as you will likely find this approach more intuitive.

In other words, it is not a matter of one approach being better than the other. The important thing is to choose the method that best fits your requirements and operational needs. I encourage you to understand the characteristics of each approach and select the one that is most suitable for your environment.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
