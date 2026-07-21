# SFMC Tips #89 : Marketing Cloud Next: Basic Elements of Marketing Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-understanding-the-basic-elements-of-flow-builder-1a749ecf92fa

---

# SFMC Tips #89 : Marketing Cloud Next: Basic Elements of Marketing Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1a749ecf92fa---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1a749ecf92fa---------------------------------------)

8 min read

·

Mar 18, 2025

--

Photo by [Natalya Letunova](https://unsplash.com/@naletu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, you can use flows to automate a variety of scenarios. This article explains the basic elements that make up a flow.

### Wait Elements

- **Wait for Amount of Time**
- **Wait Until Date / Wait By Attribute** (added in Winter ’26)
- **Wait Until Event**

### Split Elements

- **Decision**
- **Path Experiment**
- **Einstein Decision** (added in Summer ’25)
- **Determine CRM Record for Individual** (added in Winter ’26)

Now, let’s take a closer look at each element.

## Wait for Amount of Time Element

When a contact reaches this element, they will wait for the specified duration before resuming the flow.

Here’s the configuration screen for this element:

### Interval Options

The following intervals can be specified:

- **Minutes**
- **Hours**
- **Days**
- **Months**

Additionally, there is an option called “Resume at a specific time of day”. This feature is useful for adjusting the timing of email sends. Let’s consider the following scenario:

**Example: When the send times for the first and second emails differ**  
If the entry time into the flow is 3:30 PM, the default setting sends both the first and second emails at 3:30 PM. However, if you want the second email to be sent at 3:00 PM, you can use the “Resume at a specific time of day” option to adjust the send time.

**Example Scenario**

- Entry Time: March 12, 2025, at 3:30 PM
- Wait Duration: 3 Days
- **Resume at a specific time of day**: 3:00 PM

**Here’s how the schedule unfolds:**

1. Contact enters the flow on **March 12, 2025, at 3:30 PM**.
2. They wait for 3 days, reaching **March 15, 2025, at 3:30 PM**.
3. The **Resume at a specific time of day** option adjusts the send time to **March 16, 2025, at 3:00 PM**.

As a result, the actual wait time becomes approximately **4 days**. If this specification is not well understood, emails may not be sent at the desired timing.

**Solution**If you want the send to occur on **March 15, 2025, at 3:00 PM**, you need to set the wait period to **2 days**. This is a common source of configuration errors, so it’s important to understand this in advance.

## Wait Until Date Element

The “Wait Until Date” element allows a contact to pause at this step until a specified date, after which the flow resumes.

This feature supports selecting a date/time in **two patterns**:

1. **Static Date/Time** based on a fixed schedule
2. **Dynamic Date/Time** based on a date attribute (New in Winter ‘26)

![]()

### **1. Static Date/Time Based on a Fixed Schedule**

This simply allows you to pick a date and time from a calendar.

**Difference from Marketing Cloud Engagement:**

**Configurable Date Range**

- **Marketing Cloud Engagement**: Dates can be set up to a maximum of 5 years in the future.
- **Marketing Cloud Growth & Advanced Edition**: Dates can be set up to December 31, 2125.

### **2. Dynamic Date/Time Based on a Date Attribute (New in Winter ‘26)**

Previously, “Wait Until Date” only supported fixed dates/times. With Winter ’26, flows can now resume based on dates/times stored in attributes, eliminating the need for complex workarounds.

![]()

This enables flexible flow control based on user-specific attributes (e.g., contract start date or birthday).

Optionally, you can specify the flow to resume **a certain number of days before/after, or hours before/after** the attribute’s date/time.

![]()

## Wait Until Event Element

The **Wait Until Event** element allows the flow to proceed based on a customer’s specific behavior (event trigger).

**Practical Use Case: Email Engagement**

The Wait Until Event element can monitor events such as:

- **Email opens**
- **Email clicks on specific or any link**
- **Email bounces**
- **Email Response** (added in Spring ’26)

If the specified condition is met within the defined period, the flow immediately resumes to the next step.

![]()

**Fallback Path for Untriggered Events**

When no events occur within the specified period, a fallback path can redirect contacts to an alternate course of action. For example:

- **Reminder Email:** If a link isn’t clicked, send a follow-up email.
- **Campaign Adjustment:** Move unresponsive contacts to a different campaign.

**Adjusting Timing for Optimal Engagement**

To avoid inconveniences, such as triggering emails at inconvenient times (e.g., late at night), use a Wait Until Event element for added control.

**Example:**

1. Add a Wait element to control email timing.
2. Set the delivery time to 3:00 PM for the second email.

- If the link is clicked **before 3:00 PM**, the email sends at **3:00 PM the same day**.
- If clicked **after 3:00 PM**, the email sends at **3:00 PM the following day**.

This ensures timely communication while enhancing customer satisfaction and engagement.

## Decision Element

The **Decision** element is used to identify target audiences that meet specific conditions based on attribute data and to route them accordingly, such as for different email delivery paths.

The following is an example of the condition configuration screen for a **Decision** element.

### Preparing a Data Graph

Before using a Decision element, you must create a **Data Graph** based on the **Unified Individual** object and specify that Data Graph in **Setup > Marketing Cloud > Reporting and Optimization > Customer Engagement > Set Up Basic Personalization**.

A **Data Graph** is “a visual representation of the relationships between data model objects” (quoted from Salesforce Help). If a Data Graph is not configured in advance, its attributes cannot be selected within the Decision element.

For more information about configuring a Data Graph, please refer to the article below.

[## SFMC Tips #96 : Marketing Cloud Next: How to Configure Data Graphs

### Photo by Nathan Lee on Unsplash

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026?source=post_page-----1a749ecf92fa---------------------------------------)

**Additional Information**

In the [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) introduced support for the following aggregation functions on numeric values from Related Attributes retrieved through Data Graphs and other related data sources:

- **Average**
- **Sum**
- **Max**
- **Min**

Previously, the only available option was to evaluate conditions based on the number of related records, such as **“Count >= 1”**.

In addition, date-based conditions have been significantly enhanced. Twenty new operators are now available for Date fields, including options such as “Is Anniversary of Today”, “Is Today”, and “Last Number of Days”.

New Date Operators:

- Is Anniversary of Today
- Is Not Anniversary of Today
- Is Today
- Is Tomorrow
- Is Yesterday
- Is This Month
- Is Next Month
- Is Last Month
- This Year
- Next Year
- Last Year
- Is On
- Is Before
- Is After
- Greater Than Last Number of Days
- Last Number of Days
- Next Number of Days
- Last Number of Months
- Next Number of Months
- Last Number of Years

*Note: Datetime fields continue to support the same eight operators that were previously available.*

*Previously, it was difficult to create flexible conditions based on numeric or date values contained in related attributes. As a result, implementing complex decision logic often required pre-processing data or creating dedicated segments in advance.*

*With these enhancements, it is now possible to evaluate sophisticated conditions directly within a flow. For example:*

- *Customers whose* ***average purchase amount is $100 or more*** *and who* ***have not made a purchase in the last 14 days***
- *Customers whose* ***last purchase date falls on the same anniversary date as today***

*This enables more advanced and accurate audience control than ever before, allowing marketers to build highly targeted customer journeys directly within Marketing Cloud.*

## Path Experiment Element

***Note:*** *Path Experiment is available exclusively in the* ***Advanced Edition****.*

The **Path Experiment** element combines the functionalities of **Random Split** and **Path Optimizer** from Marketing Cloud Engagement. This versatile element allows you to configure paths tailored to specific goals.

For more details on this feature, please see the following article.

[## SFMC Tips #188 : Marketing Cloud Next: A/B Testing with the “Path Experiment” Element

### The “Path Experiment” element in Marketing Cloud Next Growth & Advanced Edition combines the capabilities of “Random…

medium.com](/@marketingcloudtips/marketing-cloud-next-a-b-testing-with-the-path-experiment-element-5e39af4e0210?source=post_page-----1a749ecf92fa---------------------------------------)

## **Einstein Decision** Element

***Note:*** *Path Experiment is available exclusively in the* ***Advanced Edition****.*

In the **Summer ’25** release, a new AI-powered decision element called **Einstein Decision** was added to flows. By using this feature, you can create smarter branching based on two types of AI analyses: **Einstein Engagement Scoring** and **Einstein Engagement Frequency**.

Using **Einstein Decision**, you can automatically generate optimal paths with just a few clicks. For example, if you select the **Persona Splits** option from Einstein Engagement Scoring, the branching paths are created automatically as shown below.

For more details on this feature, please see the following article.

[## SFMC Tips #135 : Marketing Cloud Next: Einstein Decision Element in Flow Builder

### New Feature: Summer ’25 Release In the Summer ’25 release, Flow Builder introduces a new decision element, “Einstein…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-einstein-powered-decision-element-in-flow-builder-26c34372b92c?source=post_page-----1a749ecf92fa---------------------------------------)

## **Determine CRM Record for Individual**

In the **Winter ’26** release, a new branching element called **Determine CRM Record for Individual** was added. This feature allows flows triggered by a segment to automatically determine whether a unified individual corresponds to a **Contact**, **Lead**, or **Prospect** in the CRM.

![]()

For more details on this feature, please see the following article.

[## SFMC Tips #185 : Marketing Cloud Next: Determine CRM Record for Individual

### In the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, a new feature called “Determine CRM Record…

medium.com](/@marketingcloudtips/marketing-cloud-next-determining-the-corresponding-crm-record-for-each-individual-3ad8b0d5a805?source=post_page-----1a749ecf92fa---------------------------------------)

## Summary

As for the elements in Flow Builder, there aren’t any particularly groundbreaking features for Marketing Cloud Engagement users at this point. While there are some minor specification changes, you should be able to adapt to them quickly.

That’s all for this time!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
