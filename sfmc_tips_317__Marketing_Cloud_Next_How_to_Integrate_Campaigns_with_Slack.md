# SFMC Tips #317 : Marketing Cloud Next: How to Integrate Campaigns with Slack

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-integrate-campaigns-with-slack-082b5b628342

---

# SFMC Tips #317 : Marketing Cloud Next: How to Integrate Campaigns with Slack

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--082b5b628342---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--082b5b628342---------------------------------------)

6 min read

·

Jun 29, 2026

--

Photo by [Chase Yi](https://unsplash.com/@chaseyi_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions introduces **integration with Slack channels, enabling smoother and more efficient collaboration for marketing campaign management**.

When you create a marketing campaign in Salesforce and start the first message from the campaign record, a dedicated Slack channel is automatically created for that campaign. You can also link to an existing channel, allowing Slack to function as the collaboration hub for the campaign.

Because campaign updates and related conversations are centralized in the dedicated channel, it becomes easier for everyone involved to stay up to date. In addition, AI-powered task automation helps reduce communication overhead and enables more efficient campaign operations.

Furthermore, the initial Slack setup has been simplified. You can now access the Slack setup screen directly from **Setup > Assistant Home**.

In this article, we’ll start by creating a new Slack workspace, connect it with Marketing Cloud Next, and verify that a dedicated campaign channel is automatically created.

## Create a Slack Account

1. From **Setup > Assistant Home**, click the **Set Up Slack** button.

2. Since we’ll create a new workspace in this example, click the **Start Slack Setup** button.

3. Next, click the **Get Started** button.

4. Enter a workspace name and save it. You can use either your company name or department name.

5. After the setup is complete, you’ll receive a confirmation email from Slack. Click **OPEN SLACK** in the email.

*Then sign in using the same email address as the user currently logged in to Salesforce. Enter the six-digit verification code sent to your email address to complete the Slack sign-in process.*

## Enable the Slack Panel

1. Next, proceed to **Step 2** of the setup guide.

You can also navigate to this screen from **Setup > Slack Channels for Records**.

***Note:*** *This article skips* ***Step 3****, which is user synchronization.*

2. Enable the button to display the Slack panel. To use Slack from a campaign record, this button must be enabled.

3. Next, select the objects that can use Slack. Since the Campaign object already appears as an available option, simply select it.

4. For this demo, we’ll also enable the **Account** object.

5. Only the objects selected here will be able to use the Slack panel.

## Campaign Channel Integration

1. Now let’s actually create a campaign.

Create a new marketing campaign in Marketing Cloud Next (for example, **My 1st Slack Campaign**) and save it.

2. Open the campaign page and click the **Slack** button.

3. The Slack panel is displayed. At this point, the Slack channel has not yet been created.

4. Post the first message.

5. A Slack channel with the same name as the campaign is automatically created in real time and associated with the current campaign.

6. The message is also synchronized successfully.

Next, move to the **Campaign Details** tab.

7. Try adding campaign members.

8. Click **Add New Campaign Members**.

9. Add campaign members.

![]()

10. The registration is complete.

11. Return to Marketing Cloud Next, and you can also confirm the newly added campaign members from the Marketing Cloud Next side.

12. Next, change the campaign name in Marketing Cloud Next.

13. The Slack channel name is also updated in real time.

This confirms that the campaign and Slack are synchronized correctly.

## Configure the Component for Other Objects

For objects other than Campaign, you can use the Slack Lightning Web Component by placing it on the record page.

This time, let’s try it with the **Account** object that we enabled earlier.

1. Open an Account record and click **Edit Page** from Setup.

2. Drag and drop the **Slack Lightning Web Component** to any location on the page.

3. Save and activate the page.

4. The Slack component is now displayed on the Account record as well. The usage is the same as for campaigns — post the first message.

5. A channel is then created using the account name.

You can use this dedicated channel to share information and hold discussions related to the account.

## Conclusion

With this release, my impression is that Salesforce has gone beyond simply “connecting Salesforce and Slack” and has further strengthened the foundation for team collaboration centered around records.

Going forward, I believe we’ll gradually move toward a world where users can create segments using natural language from Slack, generate campaign flows, execute multi-channel deliveries, and even analyze the results — all without leaving Slack.

As a first step toward a future where marketing work is centered around Slack instead of opening the Salesforce interface, I found this Slack integration to be a very interesting update.

I encourage you to set it up early and experience how it works for yourself.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
