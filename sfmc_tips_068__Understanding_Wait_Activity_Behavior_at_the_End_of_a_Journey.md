# SFMC Tips #68 : Understanding Wait Activity Behavior at the End of a Journey

**Source:** https://medium.com/@marketingcloudtips/understanding-wait-activity-behavior-at-the-end-of-a-journey-ad08e68ff43d

---

# SFMC Tips #68 : Understanding Wait Activity Behavior at the End of a Journey

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ad08e68ff43d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ad08e68ff43d---------------------------------------)

5 min read

·

Dec 11, 2024

--

Photo by [Patrick Tomasso](https://unsplash.com/@impatrickt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The help documentation on optimizing the performance of Journey Builder has undergone significant updates.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_jb_optimize_sending_in_journey_builder.htm&type=5&source=post_page-----ad08e68ff43d---------------------------------------)

For users leveraging Salesforce Marketing Cloud, staying up-to-date with the latest information on performance optimization is crucial. Be sure to review the revised documentation and apply the best practices to enhance your operations effectively.

Now, among the updates, one particular section caught my attention: the **“Wait Activity”** section.

- Use wait activities sparingly. Don’t add a wait activity as a journey’s first step, and avoid using wait activities that are less than 15 minutes.
- By default, one Wait by Duration activity is on the canvas and configured to a duration of 1 day. In most scenarios, these required wait activities at the end of a journey can be lowered to 1 minute without impacting the contact’s journey. Lowering these final wait activities reduces unnecessary system load and improves the predictable performance of your journeys.
- If a wait activity in the middle of a journey is 3 minutes or less, it’s ignored unless the journey contains exit criteria or a Goal activity with exit criteria.

## My Concerns About This Update

The part that stood out was the claim:

*“If a wait activity in the middle of a journey is 3 minutes or less, it’s ignored unless the journey contains exit criteria or a Goal activity with exit criteria.”*

This statement seemed unusual.

**Midway Wait Activities:**  
I confirmed that even a one-minute Wait Activity midway through a journey functions as expected, maintaining the specified duration. If this truly got ignored, it would create significant issues.

**Final Wait Activities:**  
I also confirmed the behavior of the final Wait Activity in a journey. Previously, in journeys where the entry mode was set to *“No Re-entry”* or *“Re-entry Anytime”* without a Goal Activity, the final Wait Activity in the journey path was ignored. There was no mention of a *“three minutes or less”* condition.

Interestingly, this behavior is still documented in another Help page but has been removed from the new performance optimization guidelines:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_jb_wait_for_a_period_of_time.htm&type=5&source=post_page-----ad08e68ff43d---------------------------------------)

To improve overall Journey Builder performance, the last wait of any Journey Builder Path before the Exit is ignored in the following scenarios.

- Re-Entry Mode is Re-Entry Anytime OR No Re-Entry
- AND the journey doesn’t have a Goal Activity

This revision suggests a new condition has been introduced *“****three minutes or less****”*. To verify this, I conducted an investigation.

## Investigation

### Setting the Wait Activity

As shown below, a one-week wait activity is configured at the end of the journey.

At the time of this investigation, if the condition “less than 3 minutes” has **not** been added, the results will be as follows:

1. **“Re-entry only after exiting”** → Not ignored, the 1 week wait is applied.
2. **“Re-entry anytime”** → Ignored, no wait is applied.
3. **“No re-entry”** → Ignored, no wait is applied.

Conversely, if the condition “less than 3 minutes” **has** been added, the results will change as follows:

1. **“Re-entry only after exiting”** → Not ignored, the 1 week wait is applied.
2. **“Re-entry anytime”** → Not ignored, the one-week wait is applied.
3. **“No re-entry”** → Not ignored, the one-week wait is applied.

### Criteria for Determining Completion

In this investigation, whether or not a contact has reached the end of the journey is determined by examining the journey history for the presence of:

- A **“Stop Interaction”** activity.
- A **“Complete”** status for the **“Wait”** activity.

### Investigation Results

**Case 1: “Re-entry only after exiting”**

- **Stop Interaction (Activity):** Not present
- **Wait (Activity) Complete (Status):** Not present

This means the final wait activity has not completed and is still “in progress”.

The yellow section of the pie chart indicates no blue segments, confirming there are no contacts that have completed.

**Case 2: “Re-entry anytime”**

- **Stop Interaction (Activity):** Present
- **Wait (Activity) Complete (Status):** Present

This means the final wait activity has completed, and the journey is considered “completed”.

The blue section of the pie chart confirms that contacts have completed the journey.

**Case 3: “No re-entry”**

- **Stop Interaction (Activity):** Present
- **Wait (Activity) Complete (Status):** Present

Similar to the previous case, the final wait activity has completed, and the journey is “completed”.

The blue section of the pie chart confirms that contacts have completed the journey.

## Summary

Based on the investigation results, it is clear that the condition “less than 3 minutes” has **not** been added at this time. Therefore, regardless of the wait duration set for the final wait activity, the results are as follows:

1. **“Re-entry only after exiting”** → Not ignored, the wait is applied.
2. **“Re-entry anytime”** → Ignored, no wait is applied.
3. **“No re-entry”** → Ignored, no wait is applied.

※ This applies only when there is no “Goal” activity in the journey.

The recent update to the Journey Builder performance optimization help documentation seems to align with the current recommendations (to reduce system load). However, as the final wait activity is ignored regardless of whether it is less than 3 minutes, there is no need to adjust the wait duration.

Additionally, while not the focus of this investigation, it was confirmed that if a “Goal” activity is configured in the journey, the final wait activity will not be ignored in any of the three cases.

If an “Exit Condition” activity is configured, the final wait activity will be ignored, and it will not be evaluated as part of the exit condition. There are no changes in this behavior either.

That concludes this investigation.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
