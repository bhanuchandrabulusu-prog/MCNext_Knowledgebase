# SFMC Tips #112 : Marketing Cloud Next: Understanding Default Scoring Rules

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-understanding-default-scoring-rules-1f45d9c9333f

---

# SFMC Tips #112 : Marketing Cloud Next: Understanding Default Scoring Rules

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1f45d9c9333f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1f45d9c9333f---------------------------------------)

5 min read

·

May 8, 2025

--

Photo by [Jon Tyson](https://unsplash.com/@jontyson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), leads and contacts can be scored based on predefined rules.

This article aims to help you understand the default scoring criteria based on these predefined rules, making it easier for you to customize the scoring according to your company’s needs. I hope this serves as a helpful reference.

\*It’s important to note that the scoring functionality based on predefined rules differs from **Einstein Engagement Scoring** (exclusive to Advanced Edition), which uses AI to score. So, it’s crucial to differentiate between these two when planning your setup.

### Preparation

In the scoring rule settings, make sure to set the integration profile to “**Unified Individual**”. If it’s already set to “Unified Individual”, you can ignore this step.

In this predefined scoring process, two types of scores are used either **individually** or **combined**:

## **1. Types of Scores**

### **Used Individually**

- **Engagement Score**  
  This score is similar to the “**Pardot Score”** in Account Engagement (Pardot). It is based on actions such as web interactions and clicking on messages that were sent.
- **Fit Score**  
  Similar to the “**Grade**” in Account Engagement (Pardot), the Fit Score is based on **attribute information** like the role within the company, company size, location, etc.

### **Used in Combination**

- **Overall Score**  
  This score is a **combination of the Engagement and Fit Scores**. The weighting for each can be freely customized to suit your business needs. For example, you can set the Engagement Score to 60% and the Fit Score to 40%, or adjust as needed.

## 2. How Engagement Score is Calculated

The Engagement Score accumulates based on points awarded for each action across multiple channels. Additionally, the following rules apply:

- **Positive Points**  
  Actions such as form submissions or button clicks are rewarded with positive points, increasing the score.
- **Negative Points**  
  Negative actions such as errors or unsubscribing will subtract points from the score.

## 3. Default Scoring Rules

## Engagement Scores

### **1. Website Engagement**

- **Error**: -5 points
- **Form Submission**: +10 points
- **Anchor Click**: +3 points
- **Button Click**: +3 points
- **Search**: +3 points
- **Page View**: +1 point

**2. Message Engagement** (for SMS, WhatsApp)

- **Subscription**: +5 points
- **Click**: +3 points
- **Unsubscribe**: -5 points

**3. Email Engagement** (for Email)

- **Click**: +3 points
- **Unsubscribe**: -5 points

Note: Email open tracking is not configured.

## Fit Scores

### **1. Contact Information**

- **Address**: If the country is the United States: +3 points

## 4. Utilizing the Scores

These scores are automatically aggregated through “**Calculated Insights”** and can be used in various ways:

- In flow branching decisions
- To create segments for send lists
- Displayed on CRM record pages
- To trigger flows and register tasks when a certain score threshold is reached

You can find more information on how to display these scores on CRM record pages in the following article.

[## SFMC Tips #110 : Marketing Cloud on Core: A Practical Guide to Enhanced CRM Record Pages

### Using Marketing Cloud on Core (Marketing Cloud Growth / Advanced Edition) requires integration with Sales Cloud and…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-a-practical-guide-to-enhanced-crm-record-pages-34650d05475b?source=post_page-----1f45d9c9333f---------------------------------------)

## 5. Important Notes on Scoring Rules

Once the scoring rules are published, the system will **retroactively** score based on related data stored in **Data Cloud**. Additionally, be sure to keep the following points in mind when configuring the rules:

### **1. Accuracy of Attribute Values and Settings**

When customizing or adding rules, it’s crucial to enter attribute values accurately, including proper case sensitivity.  
**Example:** For unsubscribing from emails, the attribute should be entered as “UNSUBSCRIBE” correctly.

**Tip**: Enable the **“Value Suggestions”** feature for text data-type fields to verify the accuracy of attribute values.

### **2. Limitations for Engagement and Fit Rules**

- Both engagement rules and fit rules can be set up with a maximum of **30 rules**.
- Each rule can have up to **10 conditions**. Please note that nested conditions within a group will also count toward this limit.

### **3. How Scores Are Calculated**

- The **Engagement Score** and **Fit Score** are calculated as simple sums of points.
- However, the **Overall Score** is normalized to a range of 0 to 100.

### **4. Excluding Older Engagement Data**

- If you don’t want to include older engagement data, use **date-based conditions** to ensure only recent data is used for scoring.

## 6. Related: Account Scoring

This article primarily focused on **“Individual Scoring”** (for unified individuals), but there is also a scoring function for **“Account Scoring”** (for unified accounts).

Please note that **Account Scoring** is only available in the **Advanced Edition**. The configuration pages for “Individuals” and “Accounts” are accessible via the **tabs** at the top of the screen.

### **Account Scoring (Account Score)**

- A combination of **Account Fit Score**, **Account Engagement Score**, and optionally **Account Intent Score**.

### **Account Fit Score**

- Scoring based on **account attributes**.

### **Account Engagement Score**

- Rule-based scoring based on the customer’s actions.

### **Optional**: **Account Intent Score**

- Rule-based scoring based on the customer’s **purchase intent**.

**Note:** This **Account Score** can be used to create segments, but currently cannot be displayed on the **Account Record Page**.

**Example of Segment Use:** You could target individuals within accounts that have a high engagement score for a free consultation invitation email.

## Conclusion

Through this investigation, we discovered that only “**country = United States**” is registered for the **Fit Score**.

This **Fit Score** can be customized using **attribute data** such as **Job Title**, as well as items from related data model objects. For example, if linked to “purchase data”, you could assign **20 points** to those who bought a specific product.

After enabling the scoring functionality, make sure to configure the conditions to align with your company’s needs.

> *In the Winter ’26 release, you can now use multiple scoring models. Check out the article below for more details.*

[## SFMC Tips #191 : Marketing Cloud Next: Multiple Scoring Models Now Available

### Previously, in Marketing Cloud Next Growth & Advanced Edition, only a single scoring model could be used. However…

medium.com](/@marketingcloudtips/marketing-cloud-next-multiple-scoring-models-now-available-b697017c6fd8?source=post_page-----1f45d9c9333f---------------------------------------)

That’s all for now!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
