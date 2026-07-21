# SFMC Tips #310 : Marketing Cloud Next: LinkedIn Posting from Campaigns

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-linkedin-posting-from-campaigns-61e043fe8a88

---

# SFMC Tips #310 : Marketing Cloud Next: LinkedIn Posting from Campaigns

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--61e043fe8a88---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--61e043fe8a88---------------------------------------)

5 min read

·

Jun 16, 2026

--

Photo by [Fabian Gieske](https://unsplash.com/@fbngsk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, it is now possible to publish posts to a specific LinkedIn account either immediately or on a scheduled basis. This allows marketers to publish content directly from Marketing Cloud Next to a connected LinkedIn account.

By incorporating LinkedIn posts as part of a campaign, it becomes possible to manage activities consistently across the entire initiative.

As a result, engagement for individual posts and overall campaign performance can be monitored in a centralized manner, making it easier to drive data-based improvements and optimization.

## Campaign Setup

1. Select the **Campaign** object in Object Manager and open **Page Layouts**.

2. Locate the **Related Lists** section near the bottom of the page and drag and drop **Social Posts** into the layout.

3. Once added, save the configuration.

## Connect a LinkedIn Account

1. Open any **Campaign record**, locate the **Social Posts** related list, and click **Manage Connections**.

2. You should see **LinkedIn** displayed. Select it.

3. Click **Connect to LinkedIn**.

4. Log in with your LinkedIn account. You will be asked to authorize access from Salesforce. Approve the request.

![]()

5. Disconnecting the account is also easy. Only one account can be connected.

***Note:*** *Once an account is connected, it applies to all campaigns.*

## Create a LinkedIn Post

1. Open the **Social Posts** related list on the campaign record again and click **Add Social Posts**.

2. Click **Manage Connections**.

3. The post creation screen opens.

Enter the following information.

- **Post Name** — Name used for post management (this is not displayed publicly)
- **Post Body** — The content to be posted to LinkedIn

***Note:*** *At this time, image posting is not supported.*

## Set a Schedule

### Publish Immediately

If you select **Publish Now** without setting a schedule, the post is published to LinkedIn immediately.

***Note:*** *No confirmation screen is displayed, and the post is published immediately. There may be a delay of 1–2 minutes before the post appears on LinkedIn.*

### Scheduled Post

If you want to schedule the post, specify:

- Publication Date
- Publication Time

Then click **Schedule Post** to complete the scheduling process.

## Verify the Post

I confirmed that the post was successfully published to LinkedIn.

![]()

## View Results from the Campaign Page

1. Click the **View Engagement Statistics** action button.

2. You can review the following engagement statistics:

- **Total Reactions**
- **Total Comments**
- **Total Comments excluding Replies (Top-Leve Comments)**

3. The link included in this LinkedIn post was created as a landing page associated with the same campaign. As a result, website engagement metrics such as button clicks can also be tracked through Marketing Performance’s Website Analytics.

\* Metrics are collected only for visitors who accepted the tracking consent banner.

## What did you think?

How did you find it?

Here is the LinkedIn post that was actually published from Marketing Cloud Next.

[## #salesforce #linkedin #agentforcemarketing #marketingcloudnext #momentmarketer #marketingchampion…

### 🚀 Marketing Cloud Next Summer '26 New Release Info ※ This post was published using Marketing Cloud Next. ⬇️ ⬇️ ⬇️…

www.linkedin.com](https://www.linkedin.com/posts/nobuyuki-watanabe_salesforce-linkedin-agentforcemarketing-share-7472467993646616577-Pqlc/?utm_source=share&utm_medium=member_desktop&rcm=ACoAACy9CycBou0Y0TMGTScLWA4i9K-cYqIwypA&source=post_page-----61e043fe8a88---------------------------------------)

As someone who uses LinkedIn regularly, I personally welcome the addition of this feature.

That said, the current limitation is that image-based posts are not yet supported, which is a little disappointing. However, posts that include links are supported, and the URLs are published using LinkedIn’s own shortened URL format.

The biggest advantage of this feature is the ability to manage LinkedIn posts as part of a campaign. By combining LinkedIn activity with email and other marketing initiatives, marketers can manage the entire campaign in a more unified way while comparing performance across channels.

For example, **if you create a webinar registration form on a landing page, you can compare registrations generated through LinkedIn posts with those generated through email within the same campaign**. This makes it easier to understand which channels are driving better results and helps inform future optimization efforts.

For anyone who has wanted to incorporate LinkedIn posts into their campaign strategy, this feature is incredibly easy to use and definitely worth trying out.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
