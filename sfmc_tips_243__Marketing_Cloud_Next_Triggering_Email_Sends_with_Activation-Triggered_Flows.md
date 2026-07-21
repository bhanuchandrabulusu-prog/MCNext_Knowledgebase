# SFMC Tips #243 : Marketing Cloud Next: Triggering Email Sends with Activation-Triggered Flows

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-triggering-email-sends-with-activation-triggered-flows-6a2ad381713b

---

# SFMC Tips #243 : Marketing Cloud Next: Triggering Email Sends with Activation-Triggered Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6a2ad381713b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6a2ad381713b---------------------------------------)

6 min read

·

Jan 31, 2026

--

Photo by [VIKTORIIA YUSKEVYCH](https://unsplash.com/@viktoriiayuskevych?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With **Marketing Cloud Next Growth / Advanced Edition**, it is now possible to send emails at the moment a segment is published and activated by using the new **Activation-Triggered Flow**.

An Activation-Triggered Flow is a mechanism that immediately executes a flow using segment activation in Data Cloud as a trigger, and automatically integrates with various **API-based systems and applications**.  
A key characteristic is that integrations can be implemented without writing code, using mainly **no-code / low-code** configuration.

The following two main options are available for integration with external systems:

- **① Named Credential + External Service (HTTP Callout)**
- **② MuleSoft Integration Connector within Flow**

Both can be configured primarily through click-based operations, enabling flexible system integrations.

With this mechanism, Data Cloud evolves from being merely “a place to analyze and view data” into Salesforce’s activation hub that serves as the starting point for driving all kinds of systems.

As part of this, it is also possible to send emails from Marketing Cloud Next to segment members at the same time as external system integration.

Although Activation-Triggered Flow is originally a feature designed for system integration, it can also be used solely to send emails triggered by segment activation, without performing any external integration.

This article explains the procedure.

### Important Points When Using

There are two major points to note:

- The attributes that can be used in email content and flow decision branches **include the attributes added at the time of activation**
- Emails can be sent not only to **Unified Individual** segments, but also to **Individual** segments

## Configuration Steps

## 1. Create an Activation Target

To use this feature, first create an **Activation Target**.  
From **Activation Targets**, click **New**.

Next, **to use an Activation-Triggered Flow, select Data Cloud**.

Enter the activation target name and save.

## 2. Create a Segment

Next, create a segment.  
At this point, the selectable segment targets are either **Individual** or **Unified Individual**. Since email delivery is possible even with **Individual**, select **Individual** for this example.

Save the segment **without setting a publish schedule**.  
In Data Cloud, it is a best practice not to set a schedule immediately.

## 3. Create an Activation

Simply creating a segment does not allow it to be selected in subsequent content creation or flows.  
Therefore, be sure to complete the **Activation** setup targeting Data Cloud.

For the activation target, select the **Data Cloud activation target** created earlier.  
Use the default **Individual** for activation membership.

Next, configure the email address.  
When targeting **Individual**, there is only one email address, so priority does not matter.  
When targeting **Unified Individual**, define the conditions for the **primary email address** here.

Next, select **Add Attributes**.  
The attributes specified here can be used later as **data sources for content** and **conditions for decision elements**.

Set a name and save the activation.

## 4. Create Content

If you want to use the attributes specified at activation time within the content, you need to configure the **data source**.

From the data source type, select “**Activation Data Provider**”.

Select the **activation record** saved earlier and save.

This makes the attributes specified at activation time available within the content.

## 5. Create an Activation-Triggered Flow

When creating a new flow, select **Activation-Triggered Flow**.

In the start source, specify the target **activation record**.

In the **Decision** element, you can branch logic using the items added at activation time as conditions.

In addition, Activation-Triggered Flow allows **email sending from Marketing Cloud Next**.

![]()

After completing the configuration, save and **activate** the flow.  
At this point, no emails are sent.  
**The flow is executed when the segment is published and the activation process is completed**.

## 6. Publish the Segment

Finally, publish the segment.  
In this example, the segment contains **3 members**.

Normally, automatic execution by schedule is used, but here **manual publish** is performed.

Once segment publication is complete and activation succeeds, the flow is **triggered**.

By checking the flow execution results, you can confirm that branching is performed using the items added at activation time, and that **personalized emails using those attributes are sent**.

## Notes

- **Preview and Test Send** cannot be used  
  - This is because attributes added at activation time are used without using a data graph  
  - Also, **Preview and Test Send** is a feature exclusively for Unified Individuals
- Since both segments and activations are used, be mindful of **Data Service Credit consumption**
- Email sending does not occur immediately after segment publication, but **when the activation process is fully completed**
- In the case of manual execution, note that **it may take several tens of minutes**

## Conclusion

In this article, I introduced that email sending from Marketing Cloud Next is also possible with Activation-Triggered Flow.

One possible use case is when you want to send an email only once using attributes that are not included in the data graph.  
If you find your own use cases, please try leveraging it.

Now, the original purpose of Activation-Triggered Flow is to immediately communicate changes in audience status to the required systems.

Based on that, here are some representative examples of performing **external integration + customer notification** at the same time.

### ① Customers with Increased Churn Risk

**Activation Destinations**

- Service Cloud: High-priority response (case creation)
- Call center platform: Outbound response

**Marketing Cloud Next (customer-facing)**

- **Follow-up email** (support guidance, FAQ, chat guidance)  
  Example subject: “It looks like you haven’t been using our service recently — can we help?”

### ② Customers with Decreased Activity

**Activation Destinations**

- Advertising platforms (Google / Meta / TikTok)
- Push notification platforms (Firebase / Braze, etc.)

**Marketing Cloud Next (customer-facing)**

- **Recommendation / re-engagement email**  
  Example subject: “Here are some recent recommendations for you”

### ③ Customers Promoted to VIP Rank

**Activation Destinations**

- Membership platform / CRM / stores / POS (VIP treatment company-wide)

**Marketing Cloud Next (customer-facing)**

- **VIP promotion notification and benefits email**  
  Example subject: “Welcome to VIP Rank”

### ④ Customers Who Reached Gold Status

**Activation Destinations**

- Loyalty management system (points and benefit control)
- DWH / MDM (analysis and integration with other systems)

**Marketing Cloud Next (customer-facing)**

- **Status achievement notification and conditions explanation email**  
  Example subject: “You have reached Gold Status”

I hope this is helpful.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
