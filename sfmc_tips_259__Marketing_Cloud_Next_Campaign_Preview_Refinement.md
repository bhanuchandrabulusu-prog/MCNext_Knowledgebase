# SFMC Tips #259 : Marketing Cloud Next: Campaign Preview Refinement

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-campaign-preview-refinement-1c4ef1bfda13

---

# SFMC Tips #259 : Marketing Cloud Next: Campaign Preview Refinement

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1c4ef1bfda13---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1c4ef1bfda13---------------------------------------)

9 min read

·

Feb 26, 2026

--

Photo by [Bart Kerswell](https://unsplash.com/@bartkerswell?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Edition, a new update has been added to **Campaign Creation**, one of Marketing Cloud’s Agentforce capabilities.

With this update, during the process of creating a campaign through conversations with AI, **a campaign draft now appears on the brief**.

This enables you to make detailed fixes and adjustments (**i.e., refinement**) on the spot, allowing you to complete campaigns more practically and efficiently.

In this article, I will briefly explain an overview of these feature updates and the series of operation steps.

For the basic functionality of Campaign Creation, please refer to the following article.

[## SFMC Tips #117 : Marketing Cloud Next: Agentforce Campaign Creation

### The Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----1c4ef1bfda13---------------------------------------)

> *In addition, as a minor improvement in Spring ’26, previously, even if you applied your company’s* ***brand settings*** *(button color, font color, font size, etc.) to a brief, they would not be reflected. From Spring ’26 onward, brand settings are now applied correctly.*

## Add Topics and Actions

With this new feature update, two topics have been enhanced.

1. **Campaign Planning** (updated)
2. **Campaign Preview Refinement** (new)

### Key updates — Spring ‘26

- A new **Refine Campaign Preview** topic and actions have been added.
- The **Save Campaign** and **Generate Campaign from Brief** actions have been updated.
- The prompt template for the **Draft Campaign from Brief** action has been revised.
- The **Identify Business Unit** action has been added to **Campaign Planning**.

### 🔄 What does “reconfigure” mean?

- Here, “reconfigure” means **deleting the existing topic once and adding it again**.
- Existing topics **will not be automatically updated** to the new specifications.

### How to confirm reconfiguration is complete

As of **February 2026 (Spring ’26)**, the following **three topics** must be set up in your topic list as the latest versions:

- **Content Creation**
- **Marketing Cloud: Campaign Planning**
- **Marketing Cloud: Campaign Preview Refinement**

![]()

To set up the latest versions, reconfigure as needed by following these steps:

- **Delete** the existing older topic(s)
- **Re-add** the latest topic(s)

### ⚠ Important notes

If you have **manually customized** the existing **Campaign Planning** topic or actions, please proceed with caution.

- Deleting the topic will **remove your current configuration**.
- When you re-add it, you may need to **apply the same settings again**.
- Before deleting, it is **strongly recommended** to save your current settings using notes or screenshots.

Please review carefully and proceed with caution.

### Reference

Regarding the fourth topic shown in the image above, “Marketing Cloud: Get Score for Record ID”, it is explained in detail in the following article.

[## SFMC Tips #137 : Marketing Cloud Next: Retrieving Marketing Scores in Agentforce

### With the Summer ’25 new feature release for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), a new…

medium.com](/@marketingcloudtips/marketing-cloud-next-retrieving-marketing-scores-in-agentforce-9eeb7acf3dfc?source=post_page-----1c4ef1bfda13---------------------------------------)

Since this topic is not directly related to the campaign creation feature, it is not required for this configuration. Use it as needed.

## ① “Campaign Planning” Topic

The details of the Campaign Planning topic are described below.

### **When to Use This Topic**

- Generate / create / summarize / draft Campaigns or Briefs
- Save Campaign Preview
- Analyze Campaign objects

*\*Not used for campaign “refinement (Refine)”.*

### **Basic Rules**

**① When generating a Brief**

- Always execute IdentifyBusinessUnit → GenerateBrief in this order
- Use the campaign objective entered by the user
- Only if no objective is provided, confirm via chat (do not display an input box)
- Do not automatically execute SaveBrief after GenerateBrief
- If a file is specified:
- Search using QueryRecords (up to 3 times)
- If not identified, request additional confirmation
- Do not pass an empty string to the file parameter

**② When generating a Campaign without a Brief**

- IdentifyBusinessUnit → GenerateBrief → GenerateCampaignFromBrief
- First create the Brief, then generate the Campaign
- Do not automatically execute SaveCampaign

**③ When generating a Campaign with a specified Brief**

- Directly execute GenerateCampaignFromBrief
- Always use the specified Brief
- Do not automatically execute SaveCampaign

**④ When requesting a Campaign summary or review**

- Always execute IdentifyRecordByName to obtain the recordID
- The same applies when campaignID is required

### **Associated Actions**

As of Spring ’26, the following 9 topics are associated with the Campaign Planning topic.

![]()

**① Marketing Cloud: Draft a Campaign Brief**  
Generates a brief from the campaign objective.

**② Marketing Cloud: Save Campaign Brief**  
Saves the generated brief.

**③ Marketing Cloud: Draft a Campaign Preview**  
Creates a campaign draft based on the brief.

**④ Marketing Cloud: Save Campaign**  
Formally saves the campaign.

**⑤ Marketing Cloud: Identify Business Unit**  
Identifies the business unit to use.

**⑥ Identify Record by Name**  
Identifies the target record from the campaign name.  
(Used to obtain recordID / campaignID)

**⑦ Marketing Cloud: Summarize a Campaign**  
Summarizes campaign results.  
(Open rate, click rate, delivery volume, bounces, etc.)

**⑧ Marketing Cloud: Generate Campaign Insights**  
Generates analysis and improvement insights based on engagement data.

With the new Winter ’26 feature “Marketing Cloud: Generate Campaign Insights” action, it is now easier to obtain insights regarding past campaign performance.  
Specifically, it retrieves performance data such as message open rate, click rate, and unsubscribe rate, and automatically generates a summary of key insights.

**⑨ Query Records**  
Searches for existing Briefs or related files and records.

## ② “Campaign Preview Refinement” Topic

The details of the Campaign Preview Refinement topic are described below.

### **When to Use This Topic**

- Modify / update / change Campaign Preview
- Rewrite subject lines or body text
- Add or delete steps
- Change wait times or flows

*\*Not used for saving (Save Campaign / Save Preview).*

### **Basic Rules**

**① Always confirm the requested changes**

If the requested changes are unclear, confirm via chat.

**② Always determine the BriefId**

Before executing Refine, determine a single BriefId.

- If specified by name → search using Query Records
- If specified by ID → confirm using Get Record Details
- If multiple or zero results → confirm with the user

**③ Important rules when executing Refine**

- Use RefineCampaignPreview
- Pass the user’s requested modification text in full, exactly as is, to InputRefinement
- Do not interpret or decompose it

### **Associated Actions**

As of Spring ’26, the following 3 topics are associated with the Campaign Preview Refinement topic.

![]()

**① Query Records**  
Searches for a brief by name.

**② Get Record Details**  
Verifies the validity of the specified BriefID.

**③ Marketing Cloud: Refine Campaign Preview**  
Modifies the campaign preview of the specified brief.

## Configuration Steps (Spring ’26 Version)

Now, let’s try the “latest Campaign Creation flow” as of Spring ’26.

1. On the “**Home**” tab, click the Agentforce button to launch Agentforce, then click “**Create a Brief**”.

> *Tips: To display the “Create a Brief” button immediately after launching Agentforce, make sure to launch Agentforce from the “Home” tab in Marketing Cloud. In the default configuration, it is dynamically generated by Agentforce based on the current page context.*

2. In the “**Campaign Objective**” field, enter the following “Example objective” and click “Submit”.

- **Example objective:**  
  The target is customers who have made purchases of $200 or more within the past 30 days. The goal is to drive this segment to a special landing page offering a 20% discount.

> *Tips: In rare cases, the “Campaign Objective” field itself may not be displayed. In that case, you can simply reply within the conversation.*

3. Agentforce will automatically generate a draft of the brief. If there are no issues with the content, click “Save Brief”. If you want to make changes, improve it through conversation with the Agent.

4. The “Brief” has now been saved. As before, you can proceed directly to “**Save this campaign**”, but this time we will try the new feature. First, click the created brief.

5. You will be taken to the brief record page. Scroll down and click the “**Select Brand**” button to configure it.

> *With the Spring ’26 new feature release, brand settings are now reflected in emails created through Campaign Creation.*
>
> *Brand settings are explained in another article. A brand allows you to embed predefined company standards such as “colors”, “fonts”, “button styles”, “brand identity”, and “brand tone” into email content.*

[## SFMC Tips #94 : Marketing Cloud Next: Selecting a Brand for Your Content

### When creating new email content in Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the first thing…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-selecting-a-brand-for-your-content-97706e59ed1b?source=post_page-----1c4ef1bfda13---------------------------------------)

6. After configuring the brand, click “**Generate Campaign Preview**”, which is the main feature introduced in this update.

### **Reference:**

A campaign preview can also be created by navigating to the “**Campaign Preview**” tab within the brief and clicking “**Draft Campaign Preview**”. However, if you are proceeding through conversation, it is recommended to use the button on the conversation side.

> *Note: Creating a draft campaign preview is available until the brief is associated with a campaign. Once it is associated with a campaign, the button becomes inactive.*

7. A campaign preview is generated. To display it, click the “Preview” button.

8. You will be taken to the “Campaign Preview” tab. In this scenario, you can see that three emails will be sent.

9. You can adjust the wait intervals, and by clicking one of the emails, you can modify the subject line and body text.

> *Tips: A mechanism similar to the “Campaign Designer (beta)” discontinued in Spring ’26 has been incorporated.*

10. If everything looks good, “**Save the campaign preview**”.

11. The campaign has now been created. Navigate to the campaign.

12. You will see that one flow has been created. Open it.

13. A flow that sends three emails has been completed.

14. When you navigate to one of the emails, you will see that the email containing the current offer, including the “subject” and “body”, has been created. You can also confirm that the “brand” set in the brief has been applied.

This completes the process.

## Conclusion

Previously, there was a feature called Campaign Designer (discontinued in Spring ’26 while still in beta). It was not conversation-based but instead allowed you to create campaigns using generative AI directly in the UI. However, it now feels as though that concept has been integrated and absorbed into Campaign Creation with the Spring ’26 update.

**After all, the “build through conversation” style may be the current mainstream.**

At this stage, the process still involves text input and button operations, but in the near future, it is entirely possible that this could become voice-based. In fact, that direction already feels quite realistic.

As for the completeness of the generated content and flows, to be honest, they have not yet reached the level we envision in our minds. However, considering the speed of evolution, it would not be surprising if, in the near future, a world where email delivery is completed with “no configuration required, only verbal instructions” becomes a reality.

I am very much looking forward to future advancements.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
