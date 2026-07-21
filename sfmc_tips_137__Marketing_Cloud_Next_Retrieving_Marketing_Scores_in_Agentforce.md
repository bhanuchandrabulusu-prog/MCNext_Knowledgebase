# SFMC Tips #137 : Marketing Cloud Next: Retrieving Marketing Scores in Agentforce

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-retrieving-marketing-scores-in-agentforce-9eeb7acf3dfc

---

# SFMC Tips #137 : Marketing Cloud Next: Retrieving Marketing Scores in Agentforce

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9eeb7acf3dfc---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9eeb7acf3dfc---------------------------------------)

4 min read

·

Jun 12, 2025

--

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Summer ’25 new feature release for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), a new action called **“Marketing Cloud: Get Score for Record ID”** has been added.

[## SFMC Tips #106 : Marketing Cloud Next : Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the first…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----9eeb7acf3dfc---------------------------------------)

This functionality allows you to effortlessly retrieve **Overall Scores**, **Engagement Scores**, and **Fit Scores** for leads, contacts, and prospects by interacting with Agentforce at the desired time.

For more details on each score, refer to the following article:

[## SFMC Tips #112 : Marketing Cloud Next : Understanding Default Scoring Rules

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), leads and contacts can be scored based on…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-understanding-default-scoring-rules-1f45d9c9333f?source=post_page-----9eeb7acf3dfc---------------------------------------)

In a previous article introducing the “Campaign Creation” feature of Agentforce, I covered the following two topics:

- **Marketing Campaigns** (for campaign creation)
- **Content Creation** (for creating content)

[## SFMC Tips #117 : Marketing Cloud Next : Agentforce Campaign Creation

### The Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----9eeb7acf3dfc---------------------------------------)

The new **“Marketing Cloud: Get Score for Record ID”** action does not fall under these topics nor any existing standard topics. Therefore, I recommend creating a new custom topic and incorporating the **“Marketing Cloud: Get Score for Record ID”** action into it.

## **Setup Instructions**

1. Open the default Agentforce in the builder.

2. Change its status to Disabled or Draft to make the topic editable. Then, add a new topic.

3. Enter the action name **“Marketing Cloud: Get Score for Record ID”** as is, and click Next.

![]()

4. A basic topic content will be automatically generated. Feel free to customize the content as needed. When done, click Next.

**Note:** The scope is limited to retrieving scores for a specific record ID. Please be aware that other types of requests are not supported.

5. Finally, select **“Marketing Cloud: Get Score for Record ID”** as the action. Save the topic once completed.

6. After adding the topic, enable Agentforce to complete the setup.

## Retrieving Marketing Scores with Agentforce

1. Navigate to the CRM page. This feature is mainly intended for CRM users.

2. Click on Agentforce to launch it.

3. Enter a query such as: *“****I want to know the current score for 003Hu00003p70jmIAA****”* and submit it.

4. After a short wait, the Marketing scores corresponding to the specified record ID will be returned. Success!

## Conclusion

Of course, it is also possible to configure these scores to be displayed directly on CRM record pages, but the flexibility of the **“Marketing Cloud: Get Score for Record ID”** action allows you to check scores instantly whenever needed.

I’m very excited to see how this feature will support sales and marketing teams in the field, and how Agentforce will continue to evolve triggered by this capability.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
