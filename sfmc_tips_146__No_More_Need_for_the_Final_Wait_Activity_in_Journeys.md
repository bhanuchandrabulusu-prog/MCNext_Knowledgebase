# SFMC Tips #146 : No More Need for the Final Wait Activity in Journeys

**Source:** https://medium.com/@marketingcloudtips/no-more-need-for-the-final-wait-activity-in-journeys-e4ade2176b2b

---

# SFMC Tips #146 : No More Need for the Final Wait Activity in Journeys

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e4ade2176b2b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e4ade2176b2b---------------------------------------)

2 min read

·

Jun 30, 2025

--

Photo by [Wesley Tingey](https://unsplash.com/@wesleyphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Summer ’25 release of Marketing Cloud Engagement, the requirement to add a “final wait activity” at the end of a journey has been removed. This change, which addresses the performance impact previously associated with this activity, allows marketers to create journeys more efficiently.

[## SFMC Tips #120 : Marketing Cloud Engagement: Summer ’25 Release Highlights

### Salesforce Marketing Cloud’s new features for the Summer ’25 release have been announced, so I’d like to share a…

medium.com](/@marketingcloudtips/marketing-cloud-engagement-summer-25-release-highlights-6af46f09309e?source=post_page-----e4ade2176b2b---------------------------------------)

In a past article, I demonstrated how the final wait activity, when placed at the end of a journey, was essentially ignored.

[## SFMC Tips #68 : Understanding Wait Activity Behavior at the End of a Journey

### The help documentation on optimizing the performance of Journey Builder has undergone significant updates.

medium.com](/@marketingcloudtips/understanding-wait-activity-behavior-at-the-end-of-a-journey-ad08e68ff43d?source=post_page-----e4ade2176b2b---------------------------------------)

However, with this update, the “final wait activity” is no longer added by default, enabling marketers to build smarter journeys without unnecessary elements.

## Scenarios Where the Final Wait Activity Is Still Needed

That said, the final wait activity is not entirely obsolete. In certain scenarios, it continues to play a critical role, such as:

### Using “Re-entry only after exiting”

The “Re-entry only after exiting” setting is a highly convenient feature. By placing a wait activity at the end of a journey, you can fine-tune the timing of re-entry. For precise control of re-entry timing, the final wait activity remains an essential component.

### Using “Goal Activities”

Goal activities are evaluated when exiting a wait activity. If you want to assess goals at the very end of a journey, a final wait activity becomes indispensable.

In summary, while the final wait activity is no longer a default requirement, it remains valuable in specific scenarios. Be sure to incorporate it thoughtfully where needed, such as in the cases mentioned above. For other situations, there is no major need to be concerned about omitting it.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
