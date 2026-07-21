# SFMC Tips #49 : Introducing the New Feature: Recommended Automation Start Times

**Source:** https://medium.com/@marketingcloudtips/introducing-the-new-feature-recommended-automation-start-times-259b17962f37

---

# SFMC Tips #49 : Introducing the New Feature: Recommended Automation Start Times

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--259b17962f37---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--259b17962f37---------------------------------------)

2 min read

·

Jul 10, 2024

--

Photo by [Analia Baggiano](https://unsplash.com/@anitabagg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The Salesforce Marketing Cloud Summer ’24 release is nearing its conclusion. **A new feature that recommends automation start times has been introduced in the automation schedule settings screen**.

When you select an automation start time marked in red, a recommended time will be displayed, as shown below:

Conversely, if you select an automation start time marked in green, no recommended time will be displayed:

I looked into how this feature works and found that for all time slots (from 0:00 to 23:00), **selecting times between “26” to “36” minutes and “46” to “06” minutes will result in a red mark and a recommended time will be shown (denoted by ✕ in the table below)**.

On the other hand, **selecting times between “07” to “25” minutes and “37” to “45” minutes will result in a green mark and no recommended time will be displayed (denoted by ◯ in the table below)**.

If the recommended minute slots, as shown in the table above, were not uniformly applied across all time slots (from 0:00 to 23:00), there might be some expectations for this recommendation feature. However, since this logic is common across all time slots, I’m a bit skeptical.

**In essence, it seems like the system is indicating that statistically, the “07” to “25” minute and “37” to “45” minute slots are relatively less busy**.

This logic may change in the future, but for now, this is my review of the current functionality.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
