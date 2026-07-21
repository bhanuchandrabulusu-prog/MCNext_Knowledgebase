# SFMC Tips #91 : Marketing Cloud Next: Einstein Send Time Optimization (STO)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-einstein-send-time-optimization-sto-3cd4c104b162

---

# SFMC Tips #91 : Marketing Cloud Next: Einstein Send Time Optimization (STO)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3cd4c104b162---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3cd4c104b162---------------------------------------)

6 min read

·

Mar 24, 2025

--

Photo by [Steven Erixon](https://unsplash.com/@stevenerixon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) enables you to execute various marketing scenarios using Flow Builder. This article provides a detailed explanation of Einstein Send Time Optimization (STO) within the Flow Builder for Marketing Cloud Growth & Advanced Edition.

### Editions Supporting Einstein Send Time Optimization (STO)

Einstein Send Time Optimization (STO) is available in both the Growth Edition and Advanced Edition. However, please note the following prerequisites before getting started:

- **Activation Required in Setup**  
  STO must be activated during the initial setup.
- **Engagement Data Required**  
  Actual engagement data, such as opens and clicks, may be required.
- **Preparation Time After Activation**  
  It may take up to 72 hours for the feature to become fully functional after activation.
- [**Data Graph Configuration**](https://help.salesforce.com/s/articleView?id=mktg.mktg_einstein_esto_personalization_data_graph.htm&type=5)  
  Select the following path:  
  Unified Individual  
   → Unified Link Individual  
   → Individual  
   → Contact Point Email  
   → Email Send Time Optimization  
  Then, check the checkbox for “**Hourly Scores By Week**”.

## Feature Overview

Einstein Send Time Optimization (STO) uses machine learning to automatically analyze the engagement data of each contact from the past 90 days. It predicts the optimal send time for individual contacts to maximize the likelihood of engagement with your messages.

### - Handling New Customers or Limited Data

If engagement data from the past 90 days is insufficient — such as with new customers — the system sends messages based on a “**global model**”, which determines the best send time.

### - Evaluation Schedule

Engagement data is evaluated only once a week, and emails classified as transactional are excluded from the evaluation.

### - Improving Data Quality Scores

To improve your data quality score, it is recommended to distribute messages across different days of the week to as many contacts as possible.

## Considerations for Configuration

### Differences from Marketing Cloud Engagement

In the traditional **Marketing Cloud Engagement**, Einstein Send Time Optimization (STO) existed as a standalone activity. However, in Marketing Cloud Growth & Advanced Edition, STO is integrated as part of the email element functionality.

### Waiting Period and Send Timing

Once the waiting period for Einstein Send Time Optimization (STO) ends, emails are sent exclusively at the **top of the hour** (e.g., 10:00, 11:00). Until the next top of the hour, the email will remain in a waiting state.

**Example Scenario:**  
 For a scenario where emails need to be sent between 10:00 and 17:59:

- **Included Top-of-Hour Slots:** 10:00, 11:00, 12:00, 13:00, 14:00, 15:00, 16:00, 17:00.
- **Configuration:** To include 8 hourly slots, set the waiting period to **8 hours**.

This setup ensures emails are sent at each top-of-the-hour slot within the defined period.

### Adjusting Send Times: Points to Note

Accurate management of send times requires careful configuration of the **waiting element**.

### Case 1: Starting Sends at 10:00

- The email element must be reached **before 09:59**, and the STO evaluation must be completed.
- **Recommendation:** Start the flow around **09:30** to ensure sufficient time for the email element to be reached.

### Case 2: Sending Multiple Emails

Consider the following scenario:

**1. First Email Element:**

- STO set to “3 hours”.
- Followed by a “5 day wait”.

**2. Second Email Element:**

- STO set to “3 hours”.

### Timing for the First Email

If you want the first email to be sent at **15:00, 16:00, or 17:00**, you begin the flow at **14:30**. So far, no issues.

### Timing for the Second Email

When will the second email be sent?  
**Answer:** At one of these times: **16:00, 17:00, 18:00, 19:00, or 20:00.**

### Explanation

- If the first email is sent at **15:00**, the 5-day waiting period concludes, and contacts arrive at the second email element around **15:01**. Since they miss the 15:00 slot, the next available slots are **16:00, 17:00, and 18:00.**
- Similarly, if the first email is sent at **17:00**, the waiting period concludes around **17:01**, meaning the next available slots are **18:00, 19:00, or 20:00.**

This slight delay can shift send times unintentionally, requiring careful attention.

### Avoiding Timing Discrepancies

To prevent send time shifts, use the “**Resume at a specific time of day**” option in the **Wait for Amount of Time** **element** configuration.

**For example:**  
 Instead of a simple “5 day wait”, configure it as:

- **“Wait 4 days + Resume at 14:30”.**

This adjustment ensures all contacts reach the second email element at the same time, allowing the second email to be sent at **15:00, 16:00, or 17:00**, as intended.

## Evaluation Methodology

Einstein Send Time Optimization (STO) is evaluated **only once per week**. The evaluation process works as follows:

### Evaluation Targets

- **Emails sent with the Commercial classification** are subject to evaluation.
- Engagement data from the past **90 days** is analyzed **per Email Address** (❌ not by unified individual).

### Monitoring Analysis Results

Using the **DMO (Data Model Objects)** in **Data Cloud**, you can create graphs to display Einstein STO scores **per email address**, not unified individuals.

The report can be accessed from: **[Data Cloud] > [Reports] > Email Send Time Optimization**

### Data Fields in Reports

1. **Organization ID**: Core ID of the organization.
2. **Contact Point Email ID**: Contact email ID represented by a time zone number.
3. **Time of Week**: Optimal send time for each contact email ID represented as a value from 0 to 167, starting at **Monday at 12:00 AM**.
4. **Created Date**: Date stamp of the latest data.

### Example of “Time of Week” Values

- **Time of Week = 0**: Monday at 12:00 AM
- **Time of Week = 1**: Monday at 1:00 AM
- **Time of Week = 167**: Sunday at 11:00 PM

### Important Notes

### Preconditions for Evaluation:

- The target contact must have **“opens”** or **“clicks”** within the **past 90 days**.

### If Preconditions Are Not Met:

- Contacts without engagement data within the past 90 days are excluded from evaluation.
- Messages are sent based on a “generalized model” (system-defined optimal send times).

## Feature Differences Between Platforms

### Features Exclusive to Marketing Cloud Engagement:

**1. Standalone Activity**

**2. Dedicated STO Dashboard**

**3. STO Preview Functionality**

![]()

**4. “Send immediately” Option**

How was it?

In Marketing Cloud Growth & Advanced Edition, Einstein Send Time Optimization (STO) is integrated as part of the email element. By leveraging this feature more effectively, you can expect improved email delivery performance.

### If You’re Skeptical About Einstein Send Time Optimization (STO)

Try the following methods to validate its effectiveness:

- Use the **Path Experiment Element**.
- Conduct an A/B test with a path that incorporates Einstein Send Time Optimization (STO) and another path that does not.

Note: The Path Experiment Element is available only in the Advanced Edition.

### Tips to Maximize Effectiveness

By increasing the range of potential send times as much as possible, you can expect better performance improvements.

This concludes an overview and usage guide for Einstein Send Time Optimization (STO). I hope this will serve as a helpful reference for your future email delivery strategies.

That’s all for now!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
