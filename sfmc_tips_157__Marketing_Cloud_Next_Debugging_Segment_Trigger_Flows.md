# SFMC Tips #157 : Marketing Cloud Next: Debugging Segment Trigger Flows

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-debugging-segment-trigger-flows-80efef3c4e7a

---

# SFMC Tips #157 : Marketing Cloud Next: Debugging Segment Trigger Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--80efef3c4e7a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--80efef3c4e7a---------------------------------------)

5 min read

·

Aug 11, 2025

--

Photo by [michele marchesi](https://unsplash.com/@michelemarchesi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), the flow debugging feature is equivalent to the “Journey Test” function in Marketing Cloud Engagement.

In this article, I’ll focus on the debugging feature for **segment trigger flows** and explain how it works.

> ***Tips:*** *In the* ***Spring ’26 new feature release****, you can now select* ***up to 10 Unified Individuals for testing****.*

**Before Spring ’26**, only **one person** could be selected using a radio button.

**Starting with Spring ’26**, you can now select **up to 10 people**.

## Debugging Segment Trigger Flows

In the debug mode of a Segment-Triggered Flow, you can select a test Unified Individual and verify how that individual progresses through the flow path. If the flow contains an “Send Email Message” element, you can also choose whether to actually send a test email.

> *This debugging feature offers functionality similar to* [*the “Preview and Test Send” feature in Content Builder*](/p/a91b0f6a1ecf)*, specifically the test send part.*

### Behavior of Non-Send Email Message Elements

- **Wait for Amount of Time:** Debugging pauses midway, and you choose whether to continue.
- **Wait Until Date:** Debugging pauses midway, and you choose whether to continue.
- **Wait Until Event:** Debugging pauses midway, and you choose whether to follow the event path or the timeout path.
- **Decision:** Debugging does not pause. Branching happens automatically based on subscriber attributes.
- **Path Experiment:** With the new feature release in Spring ’26, Path Experiment debugging has also been enhanced. You can now pause the debug process midway and choose whether to proceed with random selection or manually select which path to follow.

[## SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

### In the Spring ’26 new feature release of Marketing Cloud Next, several important enhancements have been made to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961?source=post_page-----80efef3c4e7a---------------------------------------)

## Debug Setup Procedure

1. Click **Select Data Cloud Record**.

2. From the segment configured in the flow, **select up to 10 Unified Individuals for testing**. You can test multiple individuals at once. (Available from Spring ’26 onward).

3. Next, check **Send Email Message** to send a test email to up to five email addresses. If you leave it unchecked, the flow will be tested without sending any emails.

## Test Send Logs for Flows

When a test send is performed, tracking data is stored in the **Email Engagement** DMO.

In this case, the **Individual ID** recorded is **not** the Unified Individual ID selected in the debug setup screen, but rather linked to **“test-send-individual-id”**, meaning it is not associated with any specific individual.

### Open and Click Tracking

For tracking “Opens” and “Clicks”, the behavior depends on the settings applied in the **Send Email Message** element of the flow:

- **Track Clicks:** On / Off
- **Track Opens:** On / Off

If these are set to **On**, the tracking is recorded against **test-send-individual-id**. Again, this means the tracking is not tied to any actual individual.

![]()

> *“Sent” and “Unsubscribe” actions are automatically tracked.*

### Unsubscribe Link

If you click the **unsubscribe link** in a test email sent from a flow, the **Communication Subscription Consent** DMO (which manages consent data) will store it under **Communication Subscription Channel Type** as a dummy entry `"dummyCsctToken"`.

This ensures that **no actual individual’s subscription preferences are opted out**.

### Preference Center

On the other hand, if you unsubscribe via the **Preference Center** from a test email, the **first email address** in the list of test send recipients will actually be opted out.

Note: Previously, the email address of the previewed customer would be opted out. This behavior has since been improved so that **only the first email address used as the test send recipient** is updated.

As shown below, the email address that will be updated is displayed in advance — so be sure to confirm it before proceeding.

### About Rollback Mode

As a debugging option, you can choose whether to run the debug with rollback mode enabled or without it. Either way, this will **not** result in any emails being sent to the selected customers.

> *If you run the debug* ***without*** *applying rollback mode (unchecked), there is a possibility that Salesforce CRM data will actually be updated, so please take caution.*

## Conclusion

This time, I covered Segment Trigger Flows, but you can also debug Event Trigger Flows and Data Cloud Trigger Flows in a similar way, so feel free to give it a try.

Additionally, the list displayed when configuring debugging corresponds to the **segment preview feature**. You can choose which fields to display (selectable from Unified Individual fields) and also apply filtering, so be sure to make use of it. **You can display up to 25 users at a time**.

> *For the* ***External Record Id****, the field contains the* ***Individual Id*** *determined by the ID resolution reconciliation rules. For anonymous individual records, this field will be blank.*

That’s all for now.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
