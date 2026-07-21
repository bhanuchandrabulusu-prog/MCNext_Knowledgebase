# SFMC Tips #70 : Einstein Engagement Frequency Demystified

**Source:** https://medium.com/@marketingcloudtips/einstein-engagement-frequency-demystified-601bd50a84cc

---

# SFMC Tips #70 : Einstein Engagement Frequency Demystified

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--601bd50a84cc---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--601bd50a84cc---------------------------------------)

6 min read

·

Dec 25, 2024

--

Photo by [Sayan Majhi](https://unsplash.com/@minimalsayan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Previously, I wrote an article on one of Salesforce Marketing Cloud’s AI features, ***Einstein Send Time Optimization***.

[## SFMC Tips #29 : Discussing Einstein Send Time Optimization

### In this article, I would like to discuss Einstein Send Time Optimization. This feature, currently available for…

medium.com](/@marketingcloudtips/discussing-einstein-send-time-optimization-6dd825a5d2b3?source=post_page-----601bd50a84cc---------------------------------------)

[## SFMC Tips #51 : Evaluating Einstein Send Time Optimization

### In this article, I want to explore how Einstein Send Time Optimization (STO) evaluates subscribers.

medium.com](/@marketingcloudtips/evaluating-einstein-send-time-optimization-6c769e0972b4?source=post_page-----601bd50a84cc---------------------------------------)

This time, I’d like to delve into another AI feature: ***Einstein Engagement Frequency***.

By reading this article, you’ll gain a clear understanding of Einstein Engagement Frequency and eliminate any uncertainties about it.

## What is Einstein Engagement Frequency?

**Einstein Engagement Frequency** is a feature that uses AI to recommend the **optimal email sending frequency** for each contact.

With this feature, you can prevent subscribers from feeling overwhelmed by too many emails — reducing unsubscribe rates — while enhancing customer satisfaction.

💡 Keep in mind that the goal of this feature is to **prevent unsubscribes** and **boost customer satisfaction**.

## Requirements for Model Generation

To model Einstein Engagement Frequency, certain conditions must be met:

- A minimum of **10 subscribers** is required.
- At least **5 sends** (with specific intervals) within **28 days** are necessary, with these sends classified as **Commercial emails**.

Once these requirements are fulfilled, Einstein Engagement Frequency will be ready for use.

## How It Works

Einstein analyzes the **past 28 days of a contact’s engagement data from Commercial emails** and classifies them into the following frequency categories:

**1. Saturated** (Too many emails sent):

- Based on open and click rates, Einstein suggests reducing email frequency to alleviate subscriber stress.

**2. On Target** (Reasonable frequency):

- Maintain the current frequency to continue maximizing results.

**3. Undersaturated** (Too few emails sent):

- Increase the frequency to expand revenue opportunities.

*\*A contact’s frequency classification is* ***updated daily****.*

*\*Once the model is established, each contact will receive a frequency classification, even if fewer than 5 Commercial emails are sent.*

## **Almost Saturated** Settings

In addition to the three settings mentioned above, it is possible to configure an **Almost Saturated** setting that indicates a state just before Saturated. This allows you to identify contacts that are not yet in a Saturated state but are approaching it.

### Key Points:

Contacts marked as **Almost Saturated** can be classified into one of two categories: **On Target** or **Undersaturated**.

In other words, they fall into one of the following conditions:

- **Almost Saturated** and in the **On Target** state.
- **Almost Saturated** and in the **Undersaturated** state.

Note: Almost Saturated contacts are those that are close to becoming Saturated but are **not yet included in the Saturated category**.

### Types of **Almost Saturated** Settings:

- Contact reaches saturation limit in 1 email
- Contact reaches saturation limit in 3 emails
- Contact reaches saturation limit in 5 emails

### Implementation Tips:

When using multiple **Almost Saturated** settings in the same Journey, evaluate them in the following order:

**1 email → 3 emails → 5 emails**.

This is because “5 emails” is synonymous with “within 5 emails” and would therefore satisfy all the other conditions as well.

## Features and Use Cases

### 1. Einstein Engagement Frequency Dashboard

This dashboard provides an overview of email frequency distribution across your account.

- The dashboard updates **weekly**.
- Individual contact classifications (e.g., Saturated, Undersaturated) cannot be viewed directly on the dashboard.
- Transactional and test sends are excluded from the analysis.

### 2. Journey Builder Frequency Split Activity

In Journey Builder, the Frequency Split activity can be easily implemented with drag-and-drop functionality.

As noted above, contacts with insufficient data are described as being classified under the On Target segment. However, in reality, they may also be classified under other segments such as Saturated or Undersaturated. The graph below illustrates how contacts with insufficient data are evaluated. While the majority fall under On Target, a small portion can also be observed in other categories.

![]()

## Capturing Specific Contact States

Until October 2020, the following two dedicated data extensions for checking the status of each contact were enabled in Marketing Cloud:

1. **Einstein\_MC\_EMAIL\_Frequency\_Undersaturation**
2. **Einstein\_MC\_Email\_Frequency\_Oversaturation**

However, these have been deprecated and are no longer available.

As an alternative, let’s store the specific status of each contact in a data extension using another method.

This storage method will be implemented through **Journey Builder**. For this demonstration, we will create two patterns: one without the Almost Saturated setting and one with it.

### Data Extension Setup

Create a sendable data extension with the following fields:

- **Id**: Text (50), Primary Key
- **EEF1**: Text (50) (Stores states without **Almost Saturated** settings)
- **EEF2**: Text (50) (Stores states with **Almost Saturated** settings)

- **EEF1** will store the states when there’s no Almost Saturated setting.
- **EEF2** will store the states when the Almost Saturated setting is applied.

## Journey Builder Configuration

### 1. Without the Almost Saturated Setting

Set up the branches as shown below:

In the Update Contact activity, set up **EEF1** to store one of the three states: Undersaturated, On Target, or Oversaturated.

This journey should be scheduled to **run daily**.

### 2. With the Almost Saturated Setting

Set up the branches as follows:

- When using multiple Almost Saturated conditions, evaluate them in the order: 1 email left → 3 emails left → 5 emails left.
- This ensures proper evaluation because the 5 emails left condition is essentially the same as within 5 emails, which would encompass all other conditions.

In the Update Contact activity, configure **EEF2** to store one of six states: 1 email left, 3 emails left, 5 emails left, Undersaturated, On Target, or Oversaturated.

This journey should also be scheduled to **run daily**.

**Important Note:**  
Contacts categorized as Almost Saturated can fall into either the On Target or Undersaturated categories. To accurately track Almost Saturated contacts, create branches for this condition before handling the On Target and Undersaturated categories.

## Potential Issues with This Method

Some contacts (those who did not enter the journey) might retain outdated data in the data extension.

## Use Cases for the Data Extension

These data extensions have various potential applications:

- For example, excluding Oversaturated contacts from the sending master list allows you to suppress sending to these contacts.
- This opens the possibility of reallocating those sends to Undersaturated contacts, sending them alternate messages.

Feel free to explore other creative ways to use these extensions!

**⚠️ Caution:**  
Using Einstein Engagement Frequency in ways that deviate from its intended purpose (preventing unsubscribes and improving customer satisfaction) may disrupt the expected modeling. Avoid excessive or unintended usage.

## Tips for Limited Sending Patterns

If you’ve just implemented Einstein Engagement Frequency and your sending patterns are limited, contacts may be incorrectly categorized as Oversaturated even with low email volumes.

To address this:

- Send messages to various customer segments **at different intervals**.
- Gradually accumulate data to diversify your sending patterns.

Over time, Einstein’s model will provide more accurate assessments. Be patient and keep iterating!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
