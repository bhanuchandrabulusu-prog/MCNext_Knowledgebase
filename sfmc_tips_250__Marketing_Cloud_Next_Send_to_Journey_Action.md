# SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63

---

# SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3a0c77cc2b63---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3a0c77cc2b63---------------------------------------)

5 min read

·

Feb 17, 2026

--

Photo by [sporlab](https://unsplash.com/@sporlab?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In environments using **Marketing Cloud Engagement+**, it is possible to send Marketing Cloud Next contacts from a **Marketing Cloud Next Flow** to **Marketing Cloud Engagement** and send emails.

This integration is achieved by combining the **“Send to Journey” action** in Marketing Cloud Next with an **API Event entry source** configured on the Marketing Cloud Engagement side.

For example, you can use a **Segment Triggered Flow** to send users to different journeys depending on the status of their loyalty program.

If you are familiar with Marketing Cloud Engagement development, you may be able to quickly understand the overall configuration.

However, marketers may not have had many opportunities to use the **API Event entry source** before.

Therefore, in this article, I will explain the **basic mechanism and setup procedure of the “Send to Journey” action** step by step in an easy-to-understand way.

## Setup Method

### ① Create a Sendable Data Extension

1. First, start by creating it from **Template Data Extension**.

2. Select **TriggeredSendDataExtension**.

3. Decide the **Data Extension Name** and set it as **Sendable**.

4. In this example, in addition to the default fields, I prepare name fields for personalization.

- **SubscriberKey (Subscriber Key) ※ Default field (cannot be changed)**
- **EmailAddress (Email Address) ※ Default field (cannot be changed)**
- **FirstName (First Name)**
- **LastName (Last Name)**

### ② Configure API Event in the Journey

1. Next, select **API Event** as the entry source in **Journey Builder**.

2. Click **Create an Event**.

3. Start configuring the Data Extension.

4. Set the Data Extension created earlier as the receiving container for the API Event.

5. After the configuration is complete, **save and activate the journey**.

> *※ If the journey is not activated, it will not appear as an option for the* ***Send to Journey*** *action.*

### ③ Add the Journey to a Campaign

Add the journey configured above to a campaign.  
This will allow it to be selected in the **Send to Journey** action.

### ④ Configure in Marketing Cloud Next Flow

1. Next, open the flow on the **Marketing Cloud Next** side and add the **Send to Journey** element.  
When you click the element, the journey that was activated earlier will appear as an action.

> *※ The name displayed here is the* ***Journey Name****.*

2. When you select the action, the **detail configuration screen** will open.  
After setting the name and API name, fields that were optionally added in the Data Extension (such as first name and last name) will appear in addition to ID and Email.

3. Map the fields with the fields on the **Marketing Cloud Next** side.

### ⑤ When Adding Fields

1. If you feel that the fields required for personalization are insufficient, add new fields to the **Data Extension**.

2. After that, refresh the flow screen and the new fields will be automatically loaded.  
Do not forget to map the newly added fields.

> *Note: Even if fields are added or removed in the Data Extension, the changes may not be immediately reflected in the flow.  
> In that case, create a* ***new version*** *of the journey and* ***reconfigure (replace) the API Event entry source****.  
> This will correctly reflect the latest Data Extension definition.*

### ⑥ Save and Activate

1. After completing all configurations, **save and activate the flow**.

> *Notes During Execution: If the* ***journey status is “Paused”****, records will not be processed immediately and will be held in a queue.  
>  When the journey is resumed, the records accumulated in the queue will be sent to the journey sequentially.*

2. As shown below, the data was sent to **Marketing Cloud Engagement**.

3. The **SubscriberKey** that is synchronized is the **Individual ID**.

> *※ Please note that it is* ***not the Unified Individual ID****.*

## Conclusion

In simple terms, **Send to Journey executes an API from the flow and sends contacts to the journey**.

Previously, similar behavior could be achieved using “**Data Actions**” **in Data 360**.

However, compared to Data Actions, **Send to Journey is overwhelmingly easier to use**.

- Configuration completed within the familiar Flow UI
- Natural integration with various types of flows

> *Note: The* ***Send to Journey action is not supported in Event Triggered Flows triggered by “Form Submission” events****.*

As the integration between **Marketing Cloud Engagement and Marketing Cloud Next** continues to expand, the opportunities to use this action will certainly increase.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
