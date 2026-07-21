# SFMC Tips #51 : Evaluating Einstein Send Time Optimization

**Source:** https://medium.com/@marketingcloudtips/evaluating-einstein-send-time-optimization-6c769e0972b4

---

# SFMC Tips #51 : **Evaluating Einstein Send Time Optimization**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6c769e0972b4---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6c769e0972b4---------------------------------------)

3 min read

·

Aug 14, 2024

--

Photo by [Olena Bohovyk](https://unsplash.com/@olenkasergienko?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, **I want to explore how Einstein Send Time Optimization (STO) evaluates subscribers**.

*The content I’m about to explain is based on my understanding and not an official stance, so there might be some inaccuracies. However, I hope it provides some clarity.*

Firstly, **the evaluation by Einstein Send Time Optimization happens only once a week**. This evaluation focuses on emails sent under the Commercial classification. **It analyzes the engagement data from the past 90 days for each email address (not subscriber key) and then returns the results to the “subscriber key”**. Like Einstein Engagement Scoring, it appears that Einstein primarily analyzes data on a per-email address basis.

Regarding when this weekly evaluation occurs, you can check the schedule in the Einstein STO dashboard.

The analysis results returned to the “subscriber key” can also be viewed by entering the “subscriber key” into the appropriate field in the Einstein STO dashboard.

For this analysis to take place, **the subscriber must have “open” or “click” engagement data within the past 90 days**. **If, at the time of the weekly evaluation, there is no engagement data within the past 90 days for a “subscriber key”, no evaluation will be conducted**.

\*You can check whether there is “open” or “click” data within the past 90 days for a subscriber by opening the “History” tab in the “Properties” of All Subscribers List.

![]()

As mentioned earlier, **the evaluation by Einstein STO is conducted “per email address”**.

This means that, **at the time of the weekly evaluation, if the same email address is registered for multiple “subscriber keys”, the same result will generally be returned**.

Now, considering all these factors, I’d like to summarize my understanding of how Einstein Send Time Optimization (STO) evaluates subscribers.

**My image is that the engagement data accumulated for “subscribers with engagement data (opens or clicks) within the past 90 days” is aggregated based on email addresses, analyzed per email address, and then returned to the “subscribers with engagement data within the past 90 days” based on their email addresses.**

What do you think?

I can’t say for certain that my understanding is entirely correct, but I believe it’s not too far off.

Finally, **let’s consider what this evaluation could lead to**. For example, in a scenario **where a subscriber’s email address has been changed**, **is the engagement data history from the previous email address still valid for the new one, or is it reset?**

To conclude, **the engagement data obtained with the old email address remains “valid” and is not reset**. 💡

**This is because even if the email address is changed, the 90-day “History” tab in the subscriber’s properties, containing the “open” or “click” engagement data, is not deleted**.

So, even if the email address is changed to a new one, as long as there was engagement (like opens or clicks) within the 90 days before the change (**👈️**this condition is important), the analysis will utilize the engagement data from the old email address, and **some form of** analysis result will still be returned. This means that Einstein Send Time Optimization (STO) remains effective.

*The reason I emphasize “****some form of****” is that* ***the new email address will undergo a fresh analysis with possibly different conditions, so the analysis results could differ significantly from previous ones****.*

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
