# SFMC Tips #288 : Marketing Cloud Next: Segment-Triggered Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-39957ec68f06

---

# SFMC Tips #288 : Marketing Cloud Next: **Segment-Triggered Flow**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--39957ec68f06---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--39957ec68f06---------------------------------------)

13 min read

·

May 7, 2026

--

Photo by [Osarugue Igbinoba](https://unsplash.com/@osarugue?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article explains the basic email delivery flow using the most fundamental **“Segment-Triggered Flow”** in Marketing Cloud Next Growth & Advanced Edition.

This article assumes that the following initial setup has already been completed either by your implementation partner or through your own configuration.

- **Basic setup** has been completed
- **Data Graphs** have already been configured

[**What is a Data Graph?**](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026)  
A Data Graph is a data structure used to store and reference customer profile information and behavioral data. In most cases, it is generally updated at least once per day.

## Configuration Steps

In this article, we will proceed with the following common flow.

1. **Segment configuration and publish schedule**
2. **Campaign configuration**
3. **Flow configuration**
4. **Flow debugging**
5. **Flow activation and email delivery**

This article is intended for users who are just starting to use Marketing Cloud Next, and we will go through the setup using the simplest possible configuration.

## 1. Segment Configuration and Publish Schedule

1. Open the **“Segments”** tab and click the **“New”** button in the upper-right corner.

2. Select **“Use Visual Builder”** and create a **“Standard Segment”.**

3. Enter the segment name and select **“Unified Individual”** as the segment target.

4. Select **“Standard Publish”** and configure the publish schedule.  
In Marketing Cloud Next, **published segments** are required in order to use them in flows and similar processes.

***Tips:*** *Credits are consumed when publishing segments, so for testing or trial purposes, it is recommended to select* ***“Don’t Schedule”.***

If you want to retrieve the latest audience every day, configure a **“Schedule”.**  
In this example, we will configure a schedule.

5. When configuring a schedule, set the following items in order.

- **Execution frequency** (Daily, Weekly, Monthly)
- **Refresh interval** (Every 12 hours / Every 24 hours, etc.)
- **Start date and time**
- **Execution days**

*If you want the segment to run every day, select* ***all days of the week*** *as shown below.*

Finally, configure the **schedule “End” condition**.  
In this example, select **“Never (Never Ends)”.**

6. The **“Lookback Window”** is a setting that determines how many days of historical data from related objects (such as sales data) are used during segment evaluation.  
By default, it is set to **90 days**.

*For example, when using sales data, if it is set to* ***90 days****, only sales data within the past 90 days from the segment publish date will be evaluated.  
Sales data older than four months will therefore be ignored.*

This period can be extended up to **two years**. However, the longer the period, the more credits are consumed during segment processing.

It is recommended to keep the period as short as necessary rather than configuring an unnecessarily long duration.  
In this example, we will save it using the default setting.

7. Once the property configuration is complete, the initial audience population (**all target records before conditions are applied**) will be displayed.

*However, please note that whether* ***opt-out users*** *are included in this audience depends on the configuration implemented by your implementation partner.*

Next, open **“Attributes”** from the left menu.

8. Select any attribute and drag & drop it onto the **“Include”** tab.

9. In this example, select **“Has Value”** as the operator and click **“Done”.**  
 For details regarding segment operators, please refer to [**this article**](/@marketingcloudtips/data-cloud-explanation-of-segment-operators-9dce94e06322).

10. Simply configuring conditions does not immediately update the audience count.  
If you want to check the updated count, click the **“Save”** button.

11. Once the save is complete, the audience population will be recalculated according to the configured conditions, and the target count will be updated.

12. In Marketing Cloud Next segments, **“Exclude”** conditions can also be configured.  
If you want to use exclusion conditions, select the **“Exclude”** tab.  
In this article, the explanation of exclusions is omitted.

13. With this, the segment will now be automatically published according to the configured schedule (for example, every morning at **9:00 AM**).

However, in order to make the audience easier to use during the upcoming **flow debugging** process, manually publish it once first.

From the **Segment Detail** screen displayed after clicking the **“Done”** button on the segment canvas, execute the following **“Publish Now”.**

14. When manually publishing the segment, the following warning message may appear.  
However, in Marketing Cloud Next, the **“Activation”** process is not required.  
Please ignore it.

## 2. Campaign Configuration

1. To start a flow in Marketing Cloud Next, first open the **“Campaigns”** tab.  
Click the **“New”** button or create a flow from an existing campaign.

2. Enter only the **campaign name** and click **“Save”.**  
Other fields do not need to be configured in this example.

3. There are two ways to create a flow.

- **“Quick Start”** to begin from a template
- **“Build Your Own”** to create from scratch

For a simple email delivery flow, it is easiest to start from **“Blank Email”.**  
Click it.

4. Next, click **“Open Flow”.**

## 3. Flow Configuration

1. When the flow opens in **Flow Builder**, errors will appear because the required configuration has not yet been completed.  
This is normal during the initial setup stage, so ignore the errors for now and continue with the configuration.

You can hide the error messages by clicking the **“×”** icon.

2. In the **Start** element, click **“Set Schedule”.**

Here, you can select one of the following:

- **Run Once**
- **Recurring**

If you select **“Run Once”,** you can further choose one of the following options:

- **Schedule a one-time run** (start at a specific date and time)
- **Run once immediately upon activation** (start immediately after activation)

3. If you select **“Recurring”,** configure the start date/time and the recurring schedule.

4. For the **Re-entry Criteria**, you can select one of the following three options.

- **Always**  
  The same contact can re-enter the flow again regardless of the situation.
- **After Completion**  
  Even if a contact has previously entered the flow, re-entry is allowed once the contact has already exited the flow.  
  However, if the contact is still within any step of the flow, re-entry is not allowed.
- **Never**  
  Once a contact enters the flow, the same contact can never re-enter that flow again.  
  Select this option if you want contacts to enter the scenario only once in their lifetime.

In this example, we will select **“Always”.**

5. Please note that the configuration screen for each element does not have a dedicated save button.

After configuring an element, either click the flow-level **“Save”** button or close the configuration screen using the **“×”** icon.

6. Next, configure the segment.

Search using the name of the segment you created earlier and select the target segment.

7. In the segment options, you can select one of the following two settings.

- **Do not republish the segment when the flow runs** (upper option)  
   → Displayed as **“Based on the segment publish schedule”**
- **Republish the segment when the flow runs** (lower option)  
   → Displayed as **“Immediately before this flow runs”**

If you select the lower option, the segment will be republished immediately before the flow executes so that the latest audience is used.

Therefore, when designing a flow that republishes the segment at runtime, there is no need to configure a publish schedule on the segment itself.

However, please note that republishing a segment during flow execution may introduce a delay of approximately **10–15 minutes** due to the publish process.

In this example, we assume that the segment already has a publish schedule configured, so we will select **“Do not republish the segment”** (upper option).

8. If you would like to learn more about the following **“Configure Contact Point Selection”** option, please refer to [**this article**](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9).

In simple terms, this setting determines which email address should be used when a single audience record is associated with multiple email addresses.

If this setting is not configured, emails will be sent to all email addresses associated with the audience.

If multiple email addresses do not exist, you can safely ignore this setting.

9. Close the element configuration screen using the **“×”** icon.

10. Next, before configuring the email settings, let’s create a branch using a **“Decision”** element.

To add an element, click the **“＋”** icon on the path.

![]()

11. Select the **“Decision”** element.

![]()

12. Configure the name of the decision element and the name of the path.

These names do not affect the actual behavior of the implementation, so feel free to use any names that are easy to understand.

13. Next, select the resource.

The available resources here are items that have been pre-registered in the **Data Graph**.

14. In this example, we will use the **Engagement Score** from a **Calculated Insight** and create a branch that sends emails only to people with a score of **90 or higher**.

Using Calculated Insights in branch conditions has some unique behavior, so please refer to [**this article**](/@marketingcloudtips/marketing-cloud-next-how-to-use-calculated-insights-in-flows-a83a3eb48909) for details.

15. Next, move the email element to the **“High Score”** path.

From the email element menu, select **“Cut Element”.**

16. After cutting the element, click the **“＋”** icon on the target path where you want to paste it.

17. This allows you to move the email element easily.

18. Next, click the email element and configure the email name.

19. Select the email to send.

Here, select **“Published Email”.**

20. The following **Einstein Send Time Optimization (STO)** setting is optional.

Configure it as needed.

However, this feature has some unique behavior that may be difficult for beginners, so caution is recommended when using it.  
For details, please refer to [**this article**](/@marketingcloudtips/marketing-cloud-on-core-einstein-send-time-optimization-sto-3cd4c104b162).

21. Select the **Sender Address** used for sending.

Also confirm that **Open Tracking** and **Click Tracking** are enabled.

22. Finally, select which **Communication Subscription**, meaning consent / opt-in setting, should be used for sending.

The basic concept is as follows.

- **Promotional Emails**: Configuration is required
- **Transactional Emails**: Configuration is optional

In other words, only when the email type is **“Transactional”** can the flow be activated even if this setting is left blank.

Since this example uses a promotional email, a communication subscription has been selected.

*These communication subscription and consent / opt-in settings are generally expected to be configured responsibly by the implementation partner.*

23. As an additional configuration, you can also set **Exit Rules**.

This setting is used to remove contacts from the flow when certain conditions are met.  
For details, please refer to [**this article**](/@marketingcloudtips/marketing-cloud-next-behavior-of-exit-criteria-7f55f708ecea).

24. Finally, save the flow.

If the error alerts disappear and the **“Activate”** button becomes clickable, the configuration has been completed successfully.

Typical errors that commonly occur during save include the following.

- **The content selected in the email element has not yet been published**
- **No sender address has been selected in the email element**
- **No communication subscription has been selected in the email element**

If an error appears, return to the relevant element, resolve the issue, and click **“Save”** again to validate the flow.

## 4. Flow Debugging

1. Once the flow can be saved without errors, the **“Debug”** function becomes available.

Click the **“Debug”** button in the upper-right corner.

***Tips:*** *Debugging is mainly necessary when using* ***“Decision”*** *elements or* ***“Exit Rules”.*** *For simple flows that only send emails, debugging is generally not mandatory.*

2. First, select the records that will be used for debugging.

3. You can select and debug up to **10 individuals simultaneously**.

4. After selecting the target individuals, execute **“Debug”.**

5. During debugging, it is important to verify both of the following:

- A **“success path”** where the conditions are met and the flow proceeds correctly
- A **“failure path”** where the conditions are not met and the flow does not proceed

First, confirm at least one successful path.

6. Next, confirm at least one failure path as well.

7. If you open the details of the **Start** element, you can confirm each individual’s **“Unified Individual ID”.**  
Make note of them.

- Successful path: **494938044c3dd4c56ad6032bc0de9282**
- Failure path: **55ca6b96a518011304a94dce278bd00f**

8. Next, verify what data these individuals currently have.

Open the **“Data Explorer”** tab and select the Data Graph being used.

9. Open the target Data Graph.

10. Select **“Filter”** and search using:

- **Unified Individual Id = 494938044c3dd4c56ad6032bc0de9282**

11. Click the **“View”** link in the search result’s **Json Blob**.

12. You can then confirm that the successful individual has a score of **“92”.**

13. On the other hand, the failed individual had a score of **“42”.**

By validating the data in this way, you can confirm that the branch conditions are functioning correctly.

## 5. Flow Activation and Email Delivery

1. Once everything has been verified, activate the flow.

Return to the flow screen and click **“Activate”.**

2. On the confirmation screen, also select **“Activate”.**

3. The flow is now scheduled.

4. Once execution is complete, you can confirm that two individuals proceeded through the successful path and that emails were sent successfully.

The setup is complete.

1. Please note that created flows can also be **deactivated** later.

There are two deactivation options.

**① “Deactivate and Finish Work”**

The flow status becomes **“Completed”.**

- New recipients will no longer enter the flow after deactivation
- Recipients who have already entered the flow will continue processing
- In-progress recipients will continue through the flow until the end

**② “Deactivate and Cancel Work”**

The flow status becomes **“Canceled”.**

- New recipients will no longer enter the flow after deactivation
- Processing for recipients who have already entered the flow will also stop completely
- Recipients currently in progress will stop at that point

Even in this case, the recipients are not forcibly deleted.  
 They simply remain at the point where processing stopped.

How was it?

In this article, I summarized the basic procedure for creating a **Segment-Triggered Flow** for users who are just starting to use Marketing Cloud Next.

I hope this can serve as a practical guide for new administrators.

In addition, I have also compiled related articles that may be useful when working with Segment-Triggered Flows, so please take a look at them whenever you have time.

- [Basics of Segment](/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d)
- [New Segment Preview Feature](/@marketingcloudtips/marketing-cloud-next-new-segment-preview-feature-be716460c70f)
- [Explanation of Segment Operators](/@marketingcloudtips/data-cloud-explanation-of-segment-operators-9dce94e06322)
- [Grouping, Ranking, and Limit Functions (GRL)](/@marketingcloudtips/data-cloud-grouping-ranking-and-limit-functions-grl-9c8445541eb7)
- [How to Configure Data Graphs](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026)
- [Basic Features of Marketing Flow](/@marketingcloudtips/marketing-cloud-on-core-introduction-to-flow-builder-features-fd65d9ea0b97)
- [Basic Elements of Marketing Flow](/@marketingcloudtips/marketing-cloud-on-core-understanding-the-basic-elements-of-flow-builder-1a749ecf92fa)
- [Send a Single Message per Unified Individual in Segments](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9)
- [More Flexible Scheduling for Segment-Triggered Flows](/@marketingcloudtips/marketing-cloud-next-more-flexible-scheduling-for-segment-triggered-flows-b49477a93001)
- [Debugging Segment Trigger Flows](/@marketingcloudtips/marketing-cloud-next-debugging-segment-trigger-flows-80efef3c4e7a)
- [Behavior of Exit Rules](/@marketingcloudtips/marketing-cloud-next-behavior-of-exit-criteria-7f55f708ecea)
- [Troubleshooting Decision Splits](/@marketingcloudtips/marketing-cloud-next-troubleshooting-decision-splits-73e2ab3ac40f)
- [How to Use Calculated Insights in Flows](/@marketingcloudtips/marketing-cloud-next-how-to-use-calculated-insights-in-flows-a83a3eb48909)
- [A/B Testing with the “Path Experiment” Element](/@marketingcloudtips/marketing-cloud-next-a-b-testing-with-the-path-experiment-element-5e39af4e0210)
- [Einstein Send Time Optimization (STO)](/@marketingcloudtips/marketing-cloud-on-core-einstein-send-time-optimization-sto-3cd4c104b162)
- [Einstein Engagement Frequency & Engagement Scoring](/@marketingcloudtips/marketing-cloud-on-core-einstein-engagement-frequency-and-scoring-a8c75c105b47)
- [Einstein-Powered Decision Element in Flow Builder](/@marketingcloudtips/marketing-cloud-on-core-einstein-powered-decision-element-in-flow-builder-26c34372b92c)
- [Exploring Standard Reports and Dashboards](/@marketingcloudtips/marketing-cloud-on-core-exploring-standard-reports-and-dashboards-3fdd7ec3194c)
- [How to Check Engagement Data](/@marketingcloudtips/marketing-cloud-on-core-how-to-check-engagement-data-5452bfbc1ae3)
- [How to Utilize Engagement Data](/@marketingcloudtips/marketing-cloud-on-core-how-to-utilize-engagement-data-a9b1f492b7d6)
- [Troubleshooting When Emails Are Not Sent](/@marketingcloudtips/marketing-cloud-next-troubleshooting-when-emails-are-not-sent-647e5ccb2d40)
- [Hard Bounce vs. Soft Bounce](/@marketingcloudtips/8106419bb008)

That’s it for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
