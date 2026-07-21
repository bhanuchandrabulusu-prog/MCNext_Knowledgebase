# SFMC Tips #47 : How to Handle Scheduling Issues in the New Version of Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-handle-scheduling-issues-in-the-new-version-of-journey-builder-f6b1c19bb2f1

---

# SFMC Tips #47 : How to Handle Scheduling Issues in the New Version of Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--f6b1c19bb2f1---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--f6b1c19bb2f1---------------------------------------)

3 min read

·

Jul 2, 2024

--

Photo by [Bruno Figueiredo](https://unsplash.com/@bfigas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Have you ever experienced updating a journey version in Salesforce Marketing Cloud’s Journey Builder, only to find that **you can’t change the schedule?** You might end up deleting the entry source and reconfiguring it, which can be quite frustrating.

Let’s walk through a concrete example to make this clearer.

Imagine you have a journey set on a one-time schedule. Once the distribution is complete, you decide to create a “new version” for reuse.

Once the draft is up, you try to set the schedule.

However, **you’ll notice that “View” is displayed, and “Edit” is not available**.

**Clicking on “View” only results in a grayed-out screen**, preventing any editing. Many people give up at this point and delete the entry source, but there is a way to edit it.

**The key is to eliminate any “Running” versions**.

Go back to the “Running” version and stop the journey.

Once the version is confirmed as stopped, check the draft version’s schedule settings.

Now, **you’ll see that the button has changed to “Edit”**.

## Conclusion

Remember, **if there is a “Running” version, you cannot change the schedule**. However, having a “Finishing” version is not an issue.

Thank you for reading.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
