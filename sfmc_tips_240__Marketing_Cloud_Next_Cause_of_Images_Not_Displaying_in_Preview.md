# SFMC Tips #240 : Marketing Cloud Next: Cause of Images Not Displaying in Preview

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-cause-of-images-not-displaying-in-preview-b3e1e8c9576f

---

# SFMC Tips #240 : Marketing Cloud Next: Cause of Images Not Displaying in Preview

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b3e1e8c9576f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b3e1e8c9576f---------------------------------------)

3 min read

·

Jan 23, 2026

--

Photo by [Bart Christiaanse](https://unsplash.com/@bartchristiaanse?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next (Growth & Advanced Edition) content, there are cases where **images are configured, but only the images do not appear when you open the preview**.

Even though the images are set,

![]()

For some reason, they are not displayed in the preview…

The cause of this issue is that **the domain of the image delivery source is not registered** under  
**[Setup] > [Trusted URLs]** in Salesforce.

> *“Trusted URLs” is an allowlist that Salesforce uses to treat external domains as safe.*

## How to Fix

The steps to resolve this issue are as follows.

1. Open **Salesforce [Setup] > [Trusted URLs]**.

2. Register the image delivery source domain as a **Trusted URL**.

> *Example:  
> If you want to register multiple subdomains such as*`https://www.discogs.com` *and* `https://i.discogs.com`*,  
> you can use a wildcard like* `https://*.discogs.com` *to register them all at once.*

3. Close the content once and return to the top page of the relevant content.

4. Open the preview again.

5. You will then see that the images are displayed correctly as shown below.  
This resolves the issue ✅

## Conclusion

When you encounter issues where content is not displayed or cannot be loaded on the screen, it is often related to **Trusted URL** settings, so please try checking and configuring them.

I hope this helps when you encounter a similar issue.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
