# SFMC Tips #118 : Marketing Cloud Next: Agentforce Campaign Designer (Discontinued)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-designer-708c127992b1

---

# SFMC Tips #118 : Marketing Cloud Next: Agentforce Campaign Designer (Discontinued)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--708c127992b1---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--708c127992b1---------------------------------------)

6 min read

·

May 20, 2025

--

Photo by [History in HD](https://unsplash.com/@historyhd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) includes the AI-powered campaign creation feature, **Campaign Creation**. This functionality leverages the autonomous AI agent platform, **Agentforce**, enabling users to create campaigns quickly and efficiently through conversational interactions. For more details, please check out the article linked below.

[## SFMC Tips #117 : Marketing Cloud on Core: Agentforce Campaign Creation

### The Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----708c127992b1---------------------------------------)

In the highly anticipated **Summer ’25 new feature release**, the beta version of **Agentforce Campaign Designer**, an advanced evolution of Campaign Creation, will be introduced.

> *※* ***In Spring ’26, Campaign Designer was discontinued while still in beta.***

This new feature allows for even more sophisticated campaign creation powered by generative AI. In this article, I will dive deep into the process and key features of creating campaigns using Campaign Designer.

[## SFMC Tips #106 : Marketing Cloud on Core: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----708c127992b1---------------------------------------)

*Note: Campaign Designer is available exclusively in the* ***Advanced Edition****.*

## Steps to Configure Campaign Designer

> *※* ***Since Spring ’26, this feature has been discontinued and can no longer be enabled.***

**1. Enable Campaign Designer**  
Go to **Setup > Einstein for Marketing > Create a Campaign with Campaign Designer (Beta)** and click “**Enable**”. This action will immediately make the Campaign Designer available for use.

In Campaign Creation, the default **Agentforce** was used. For this Agentforce, it was necessary to pre-assign the following two topics:

- **Marketing Campaigns** (for campaign creation)
- **Content Creation** (for content creation)

On the other hand, Campaign Designer requires no such pre-configuration, such as topic assignments. Simply enabling it allows you to start using it right away.

**2. Start Drafting with AI**  
In the **Home** tab of Marketing Cloud, click the “**Draft with AI**” button.

When using the feature for the first time, you may see a banner with explanations and guidelines.

**3. Select or Create a Brief**  
Next, choose whether to use an existing brief or create a new one. For this guide, I will proceed with the “**Create a Brief**” option.

**4. Input Campaign Objectives**  
Input the campaign’s objective. For this example, I’ll reuse an objective from a previous **Campaign Creation** article. After entering the objective, click **Draft Brief**.

- **Objective Example**:  
  Create a brief for an email campaign. The target audience is customers who have made purchases of **$200 or more** in the past 30 days.  
  The objective is to guide these customers to a special landing page offering a **20% discount**.

**5. Create a Draft Brief**  
Based on the input, a draft brief will be generated. Unlike the conversational format of **Campaign Creation**, Campaign Designer offers the following advantages:

- **Objective Editing**: You can revise the objectives and regenerate the draft after the initial input.
- **Manual Adjustments**: You can refine the generated draft manually for more detailed customization.

*Note: Campaign Creation also allows objective refinement through conversation.*

From my trials, the generated messages often include two types:

- First Email: Introduction Email
- First SMS: Reminder SMS

**Note:** Even if SMS functionality is not active in your account, SMS messages will still be generated. *(WhatsApp is currently unsupported in the beta version?)*

For this example, let’s add a second email to the flow. Add the following text to the **Brief Description** field:

**“Add a follow-up email called ‘Final Reminder’ to the end of the flow.”**

After reviewing all brief drafts, click **Next**.

**6. Generate Campaign Draft**  
A finalized **Brief** is created, followed by the automatic generation of the campaign draft.

You will be redirected to a page with the auto-generated campaign draft.

**7. Review Messages and Finalize**  
Review the text of the generated campaign messages. If everything looks good, click **Done**.

**Current Beta Limitations:**

- Campaign names (e.g., “**Exclusive Discount Offer**”) cannot be edited during creation. This can be adjusted after the campaign is created.

**Final Auto-Generated Messages:**

- First Email: Introduction Email
- First SMS: Reminder SMS
- Second Email: Final Reminder Email

This completes the campaign creation process.

Finally, review the campaign record page. As shown below, the campaign, flow, and messages are all created.

Check the email messages.

Check the SMS messages.

**8. Final Adjustments**  
After the campaign is created, some manual configurations are still necessary:

- **Set up the schedule**
- **Add segments**  
  By default, there is a **one-day wait time** between message sends, but this can be adjusted as needed.

## Final Thoughts

The ability to create a campaign almost entirely by entering a simple **objective** demonstrates the remarkable progress of technology.

- **Objective Example**:  
  Create a brief for an email campaign. The target audience is customers who have made purchases of **$200 or more** in the past 30 days.  
  The objective is to guide these customers to a special landing page offering a **20% discount**.

While the current beta version may have some limitations in message quality, future improvements are highly anticipated.

Compared to traditional **Campaign Creation**, which was limited to email campaigns, **Campaign Designer** supports the following multi-channel capabilities:

- **Email**
- **SMS**
- **WhatsApp** *(currently unsupported in the beta version?)*

The pricing structure for this feature is also intriguing. Although no details have been disclosed, it’s likely to be similar to the existing **Campaign Creation** model.

[## SFMC Tips #117 : Marketing Cloud on Core: Agentforce Campaign Creation

### The Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----708c127992b1---------------------------------------)

[## SFMC Tips #116 : New Agentforce Pricing Model: “Flex Credits”

### Salesforce has announced the release of a new pricing model for Agentforce, called Flex Credits. This update aims to…

medium.com](/@marketingcloudtips/new-agentforce-pricing-model-flex-credits-8d38793b7ef5?source=post_page-----708c127992b1---------------------------------------)

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
