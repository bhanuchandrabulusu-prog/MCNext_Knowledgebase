# SFMC Tips #264 : Marketing Cloud Next: Journey Event-Triggered Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-journey-event-triggered-flow-cf36d7d50642

---

# SFMC Tips #264 : Marketing Cloud Next: Journey Event-Triggered Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cf36d7d50642---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cf36d7d50642---------------------------------------)

5 min read

·

Mar 9, 2026

--

Photo by [Yana](https://unsplash.com/@yana_bjorn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In organizations using Marketing Cloud Engagement+, a new feature called **“Journey Event-Triggered Flow”** was added in the Winter ’26 release as one of the orchestration capabilities that link flows and journeys.

![]()

With this feature, it is now possible to trigger a Flow from Journey Builder. This makes it possible to design marketing initiatives and customer experience scenarios more flexibly than before.

## Types of Journey Event Triggers

As of Winter ’26, the following three types of Journey event triggers are available.

### ① Journey Builder Contact Entered

Triggers a flow when a contact enters a journey.

### ② Journey Builder Contact Exited

Triggers a flow when a contact exits a journey.

### ③ Journey Builder Contact Met Goal

Triggers a flow when a contact achieves a goal set within a journey.

With these triggers, flows can be executed when specific events occur within a journey, making it possible to connect the entire marketing process more smoothly.

## Configuration Method

For example, you can trigger a flow when a contact achieves a journey goal, execute the necessary processing within the flow, and then send the contact to another new journey for entry.

### 1. Configure the Event-Triggered Flow

First, select **“Blank Event”** from Campaign Flow and create an event-triggered flow.

Then select **“Journey Builder Contact Met Goal”** as the new Journey event trigger.

### 2. Select the Journey Goal

Next, select **MCE Journey**.  
The target journey can be searched by **Journey Name** or **Journey ID**.  
※ You must enter at least **three characters**.

When searching, note the following points.

### Journey Name

- Only the **latest version of the journey name** can be used when searching by name.

### Journey ID

- What can be specified here is **not the Journey Version ID, but the Journey ID**.
- You cannot search using the latest Version ID.  
  However, the **Version ID of Version 1 matches the Journey ID**.

### Tips:

In addition, the journeys that can be selected here are **only those that have already been synchronized to Data 360 through the SFMC Starter data bundle “SFMC Journey”.**

Therefore, immediately after creating a journey, it may not yet be synchronized to Data 360 and may not appear in the search results.

If you want to use a newly created journey, **start creating the flow after the synchronization to Data 360 is complete.**

You can check this in the **Data Stream history**. The synchronization frequency is **every 15 minutes**.

### 3. Configure the Send to Journey Action

Next, after executing the necessary processing within the flow, implement the **Send to Journey action** introduced in the following article in order to send the contact to a new journey.

[## SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

### In environments using Marketing Cloud Engagement+, it is possible to send Marketing Cloud Next contacts from a…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63?source=post_page-----cf36d7d50642---------------------------------------)

Once the configuration is completed as shown in the following diagram, activate the flow.

- If you branch using **Data Graph attributes**, a **wait of more than 24 hours is required**.
- If you do not set a wait, the following error will occur and the flow cannot be activated.

![]()

### 4. Achieve the Goal on the Journey Side

Next, configure the journey so that the target contact achieves the goal.

### 5. Confirm That the Flow Was Triggered

Finally, confirm that the flow was correctly triggered as a result of the goal achievement.

## Personal View

This event-triggered flow does not appear to be a mechanism that is directly launched in real time by an API.

It is highly likely that it is triggered based on records with **Status = GoalCriteriaMet** in **“SFMC Journey Activity Run”** of the SFMC Starter Data Bundle, which is synchronized at **15-minute intervals**.

Therefore, please understand that the flow is **not executed immediately** after the goal determination occurs on the Engagement side.

From this perspective, **“**[**SFMC Starter Data Bundle**](/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0)**” is a very important component for understanding how this feature operates.**

## Conclusion

This type of orchestration was often difficult to implement using Journey Builder alone.

For example, scenarios in which the next action is executed according to a change in the state of a contact, or processing is handed off to a flow or another journey, often required manual handling or complex configurations.

However, by using this **Journey Event-Triggered Flow**, it becomes possible to link **Journey Builder and Flow** more naturally.

As a result, the scope of Marketing Cloud Engagement can be expanded further, enabling the design of more advanced and seamless customer experiences.

Please try using this feature and challenge yourself to design customer experiences that extend Marketing Cloud Engagement to the next level.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
