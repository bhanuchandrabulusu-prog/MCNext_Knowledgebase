# SFMC Tips #30 : Pause and Resume Multiple Journeys from the Journey Dashboard

**Source:** https://medium.com/@marketingcloudtips/pause-and-resume-multiple-journeys-from-the-journey-dashboard-2325894d8693

---

# SFMC Tips #30 : Pause and Resume Multiple Journeys from the Journey Dashboard

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--2325894d8693---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--2325894d8693---------------------------------------)

3 min read

·

Feb 27, 2024

--

Photo by [Melissa Askew](https://unsplash.com/@melissaaskew?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Spring ’24 update of Salesforce Marketing Cloud, managing journeys has become even more straightforward with the ability to pause and resume multiple journeys directly from the Journey Dashboard.

*\*This release is scheduled* ***between February 16 and March 8, 2024****. Please note that depending on your current environment, the feature may not be available or visible on your screen yet.*

Thanks to this new feature update, **you can now select up to 10 journeys at once and “pause” or “resume” either the current version or all versions of these journeys**.

In the previous Winter ’24 release, the capability to “stop” multiple journeys from the Journey Dashboard was introduced. Building on that update, the current release now allows for both “pause” and “resume” actions.

By utilizing the pause and resume functionality for multiple journeys, you can avoid the following troubles. **For example, if there are discrepancies or shortages in the data on the core system’s side, leading to issues in the integration, or if Automation Studio’s SQL encounters malfunctions or timeouts, coming to a halt with no SQL-savvy personnel available for immediate recovery, this feature allows you to collectively pause the currently active journeys**. It proves to be an extremely useful functionality for marketers.

To learn more about these stop, pause, and resume functionalities, refer to the recently published help document titled **“Bulk Actions in Journey Builder**”. It contains detailed information on these features.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_jb_bulk_actions.htm&type=5&source=post_page-----2325894d8693---------------------------------------)

When it comes to the pause and resume functionality, I believe everyone is curious about the following options:

- Can you add the paused period to the waiting period and extend it?
- Can you specify the number of days for the pause period within 14 days?
- If you don’t resume before the end of the pause period, will it automatically stop, or will it resume automatically?

Regarding these options, after selecting the pause action through the Actions button, a popup will appear, allowing you to configure settings. However, note that these settings apply to all journeys collectively, so exercise caution.

Of course, you can still configure pause settings for each journey individually in the respective journey canvases. For instance, if you wish to stop only a specific journey after the pause period expires, you can work on that journey’s canvas separately.

As shown in the above diagram, in the pause options for periodic schedules of journeys when set to **“Evaluate new records only”**, there seems to be an option to queue newly entered contacts for processing after resuming. However, it appears that this particular selection is not visible.

The help document mentions, “Some advanced pause options are not available in this dashboard view”. Presumably, this refers to the situation mentioned above. In the case of bulk actions, the default setting might be **“Do not queue”**, though this needs confirmation through testing.

How was this information for you?

While it may be a minor update, this new feature is a game-changer for marketers. Recognize the addition of this functionality, reduce unnecessary tasks, and try to work efficiently.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
