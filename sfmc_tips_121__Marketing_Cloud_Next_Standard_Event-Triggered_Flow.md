# SFMC Tips #121 : Marketing Cloud Next: Standard Event-Triggered Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-how-to-use-event-trigger-flows-803e1b41f007

---

# SFMC Tips #121 : Marketing Cloud Next: Standard Event-Triggered Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--803e1b41f007---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--803e1b41f007---------------------------------------)

4 min read

·

May 26, 2025

--

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Editions, you can start flows based on engagement events such as form submissions, email opens, and clicks by selecting “**Blank Event**” from the standard campaign flow templates.

This article briefly explains the basic setup procedure.

In this example, we will implement an event-triggered flow scenario that sends another email when a specific URL link is clicked.

## Setup Procedure

### Creating a Segment Triggered Flow

1. First, create a Segment Triggered Flow that sends the email used to generate the event.

2. In this example, we will trigger another flow when a specific URL link in the email is clicked, so prepare the target link in advance within the email content.

### Create an Event Triggered Flow Using “Blank Event”

3. Next, select “Blank Event” from the campaign flow creation screen.

*\*It is also possible to directly create a new Event Triggered Flow.*

4. In the “**Event Library**” displayed in the Start element, you can select predefined events provided by Salesforce.

![]()

### Standard Event Library List

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=ja&id=platform.automate_flow_ref_event_library.htm&type=5&source=post_page-----803e1b41f007---------------------------------------)

5. This time, select the “**Email Link Click**” **event** and specify the target “Email” and “Link”.

At that time, you can choose either:

- Target all links
- Restrict to only specific links

### Important Notes When Using the “Send Email” Element

**6-a. When Data Graph fields are NOT used**

If only event data is used during content creation, or if Data Graph fields are not referenced:

✅ There is no need to place a wait element of 24 hours or longer before the “Send Email” element.

**6-b. When Data Graph fields ARE used**

On the other hand, if Data Graph fields are referenced:

⚠️ A wait element of 24 hours or longer must be placed before the “Send Email” element. If this wait is not configured, **an error occurs when saving the flow**.

*Today, Data Graph merge fields are no longer the only option. By leveraging* [***Apex Class Data Provider***](/@marketingcloudtips/marketing-cloud-next-run-event-triggered-flows-when-crm-records-change-a3a05691b427) *and* [***Content Variables***](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911)*, personalization can now be implemented* ***without adding a wait element of 24 hours or longer****.*

### Verification

7. After activating both flows, we confirmed that when the target URL was clicked, the recipient proceeded to the wait activity.

The event trigger executed successfully.

### Considerations

After a click occurs, it may **take approximately 2 to 5 minutes** before the flow is triggered and the contact progression is reflected on the screen.

This example scenario does not consider multiple re-entries, so add controls as necessary depending on your requirements.

↓ ↓ ↓

### More Detailed Event Trigger Configuration Available (Summer ’26 ～)

In the Summer ’26 release, it became possible to **configure more detailed trigger conditions using fields from the primary DMO**.

To configure trigger conditions, select “Add Condition” in the “Additional Criteria” section of the Start element.

In addition, by defining re-entry conditions, it is now possible to flexibly control whether the same user can re-enter the flow.

The following controls are available:

- **Always** : Allow re-entry every time the event occurs
- **After completion** : Allow re-entry only after the flow is completed
- **Never** : Execute only once (re-entry disabled)

## Advanced Use Cases and Scenarios

By leveraging this mechanism, various automation scenarios can be implemented.

- **Resending Through Alternative Channels**  
   When an email bounces, switch delivery to SMS or WhatsApp.
- **Sending Welcome Emails Upon Consent Acquisition**  
   Automatically send a welcome email when consent is obtained.
- **Automatic Campaign Member Registration**  
   Automatically add campaign members when a specific URL is clicked.

How was it?

This time, I introduced Event Triggered Flows using standard predefined Salesforce events.

On the other hand, it is also possible to build custom event triggers using “Engagement Signals”. I explain this in detail in another article, so please check that out as well.

[## SFMC Tips #150 : Marketing Cloud Next: Custom Event-Triggered Flow

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), with the Summer ’25 new feature release, you can…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-event-triggered-flow-7ae54b7798b5?source=post_page-----803e1b41f007---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
