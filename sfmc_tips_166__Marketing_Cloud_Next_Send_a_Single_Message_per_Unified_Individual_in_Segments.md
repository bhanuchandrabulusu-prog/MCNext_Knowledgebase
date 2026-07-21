# SFMC Tips #166 : Marketing Cloud Next: Send a Single Message per Unified Individual in Segments

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9

---

# SFMC Tips #166 : Marketing Cloud Next: Send a Single Message per Unified Individual in Segments

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ca52aaace7d9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ca52aaace7d9---------------------------------------)

6 min read

·

Sep 1, 2025

--

Photo by [VENUS MAJOR](https://unsplash.com/@venusmajor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, when **Unified Individual** is used in a **Segment-Triggered Flow**, the current behavior is that emails are sent to **all email addresses associated with a single Unified Individual ID**.

In other words, if **one customer is associated with multiple email addresses**, there is a possibility that **multiple emails will be sent to the same person**.

## Typical Cases Where Multiple Email Addresses Are Linked

There are several scenarios where multiple email addresses can be associated with a **Unified Individual ID**, such as the following:

- When different email addresses are entered each time in a **sign-up form**
- When the email address is changed **after converting a Lead to a Contact**
- When email addresses differ **between different data sources**, such as **Marketing Cloud Engagement (MCE)** and **CRM**

In these situations, depending on the configuration of **identity resolution match rules**, multiple emails may be sent to the same customer.

## Spring ’26 Improvement: Send Only One Email per Unified Individual

With the [**Spring ’26 new feature release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb), this behavior has been improved.

It is now possible to configure the system to **send only one email to the primary email address for each Unified Individual ID**.

By using the feature shown on the following screen, duplicate sends to the same customer can be prevented.

> *This feature is enabled by utilizing the* ***“Activation Template”****, which is one of the activation features of Data 360.*

## What this new Activation Template feature enables

With this mechanism, the following three capabilities are now possible:

1. [**Single send in Unified Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9)
2. [**Sending from Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59)
3. [**Sending from Engagement-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-engagement-cf48dd0aa6c2)

In this article, I explain the mechanism and configuration method for **single send in Unified Individual-based segment flows**.

## Check Email Addresses Associated with a Unified Individual

First, let’s check which email addresses are associated with a **Unified Individual ID**.

If you execute the following SQL in the **Query Editor**, you can confirm the email addresses linked to the unified individual.

```
SELECT UnifiedId, Id, FirstName, LastName, Email, DataSource, IRUpdatedDate  
FROM (  
    SELECT  
        b.UnifiedRecordId__c AS UnifiedId,  
        b.SourceRecordId__c AS Id,  
        d.ssot__FirstName__c AS FirstName,  
        d.ssot__LastName__c AS LastName,  
        c.ssot__EmailAddress__c AS Email,  
        b.ssot__DataSourceObjectId__c AS DataSource,  
        b.CreatedDate__c + interval '9 hour' AS IRUpdatedDate,  
        ROW_NUMBER() OVER (  
            PARTITION BY b.SourceRecordId__c, c.ssot__EmailAddress__c  
            ORDER BY c.ssot__LastModifiedDate__c DESC  
        ) AS rn  
    FROM  
        IndividualIdentityLink__dlm a /* ← Change to your Unified Link Individual DMO API name */  
    LEFT OUTER JOIN IndividualIdentityLink__dlm b /* ← Change to your Unified Link Individual DMO API name */  
        ON a.UnifiedRecordId__c = b.UnifiedRecordId__c  
    LEFT OUTER JOIN ssot__ContactPointEmail__dlm c   
        ON b.SourceRecordId__c = c.ssot__PartyId__c  
    LEFT OUTER JOIN UnifiedIndividual__dlm d /* ← Change to your Unified Individual DMO API name */  
        ON a.UnifiedRecordId__c = d.ssot__Id__c  
    WHERE a.SourceRecordId__c = '***' /*Individual Id Filter*/  
) t  
WHERE rn = 1  
ORDER BY Id  
LIMIT 10
```

Please change the following according to your environment.

- **IndividualIdentityLink\_\_dlm → Unified Link Individual DMO**
- **UnifiedIndividual\_\_dlm → Unified Individual DMO**

Also, enter the **Salesforce ID (18 digits)** of the unified individual in the **WHERE clause**.

By executing this query, you can confirm **multiple email addresses associated with one Unified Individual**.

> *If the* ***Spring ’26 improvement feature*** *is not used, emails may be sent to* ***all email addresses displayed here****.*

## Configuration Steps

### Preparation: Configure the Data Graph

This mechanism requires a **Data Graph starting from Unified Individual**.

Please connect the following path:

- **Unified Individual > Unified Link Individual > Individual > Contact Point Email**
- Also, be sure to **select a Data Source**.  
  If this field is not configured, a warning appears when saving the flow. In that case, the priority setting becomes ineffective and behaves the same as selecting **Any**, and the configured priority will not be applied.

### 1. Create an Activation Template

First, move to the **Activation tab** and click **New**.

Next, select the **Template**, which was newly introduced in **Spring ’26**.

### 2. Select the Target Data Model

Configure the following settings.

- **Target Data Model Object:** Unified Individual
- **Platform:** Data Cloud

### 3. Select the Channel

Select the channel.

If **SMS is not purchased**, only **Email** can be selected, so select **Email** here.

### 4. Configure Source Priority

Next, select **Edit Source Priority**.

This is the **most important configuration**.

Email addresses will be used **in the order of priority configured here**.

For example, the following configuration is possible.

- **Form email address**
- **Contact email address**

Of course, depending on the customer, the **form email address may not exist**.

In that case, the **next priority**, the **Contact email address**, will be used.

> *It is also possible to* ***create multiple activation templates for Unified Individual****.*
>
> *In the example in this article, the configuration prioritizes* ***email addresses obtained from forms****, but it is also possible to create a template that prioritizes* ***Contact email addresses****.*

### Additional Note: Detailed Control Using Email Type

Even for the same **Contact**, there may be multiple email addresses such as:

- **Secondary email address**
- **Business email**

In such cases, you can use **Email Type** to perform **more granular priority control**.

After registering the priority, proceed to the next step.

### 5. Next Screen (Attribute Selection)

In normal activations, the next screen is used to **add attributes**, but **activation templates do not include attribute selection**.

Proceed to the next step.

### 6. Set the Template Name

Finally, set the **Activation Template name**.

It is important to use a name that clearly indicates **which source is prioritized**.

> ***Note:*** *If the selection is incorrect, emails may be sent to unintended email addresses.*

Examples:

- **Unified Individual — Form Email Priority** (Form priority)
- **Unified Individual — Contact Email Priority** (Contact priority)

### 7. Use in a Segment-Triggered Flow

Next, create a **Segment-Triggered Flow**.

When **Unified Individual** is selected as the segment target, the **Activation Template configuration screen** appears.

Select the **activation template created earlier**.

> ***Note:*** *For* ***Unified Individual****, this configuration is* ***optional****, not mandatory. However, if it is not configured, emails may be sent to* ***all email addresses associated with the unified individual****.*

### 8. Display Channel Priority

When the template is selected, the **channel priority** will be displayed.

However, since **SMS is not added in this example**, this setting can be ignored.

![]()

After that, simply **activate the flow and send as usual**.

## Conclusion

Until now, **Marketing Cloud Next** had a major concern:

**Emails could be sent to multiple email addresses associated with a Unified Individual in a Segment-Triggered Flow.**

However, with the **Spring ’26 new feature**, it is now possible to **control sending only one email per unified individual**.

With this feature available, it is expected that **marketers will need to use this configuration as a standard practice going forward**.

Of course, if you are certain that:

- **Only one email address will ever exist**

then it may not be necessary to configure it.

However, since the configuration itself is **not very difficult**, enabling it is generally **a safer operational approach**.

That’s it for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
