# SFMC Tips #126 : Marketing Cloud Next: Embedding Forms into External Sites

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-embedding-forms-into-external-sites-fe21918045e2

---

# SFMC Tips #126 : Marketing Cloud Next: Embedding Forms into External Sites

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fe21918045e2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fe21918045e2---------------------------------------)

5 min read

·

Jun 4, 2025

--

Photo by [Nathan Dumlao](https://unsplash.com/@nate_dumlao?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Spring ’25 release, **Marketing Cloud Next (Growth & Advanced Editions)** introduces an exciting new feature: the ability to **embed published signup forms into external websites via iframes**. This enhancement enables marketers to seamlessly collect leads from virtually anywhere on the web.

### What’s an iframe?

An **iframe (inline frame)** is a standard HTML element used to embed one webpage within another. Think of it as a “window” inside your website that shows content from another URL. You’ve likely seen it in action when embedding a YouTube video into a blog post or displaying a Google Map on a contact page.

When using the signup form for Marketing Cloud Growth & Advanced Edition on an external site, it must be an iframe-compatible external site. Let’s begin by understanding this key point and proceed with the setup steps.

## Setup Guide: Embedding into a CloudPages Site

In this walkthrough, I’ll demonstrate how to embed a Marketing Cloud signup form into **CloudPages**, a part of **Marketing Cloud Engagement**, which supports iframe embedding. In fact, CloudPages allows for embedding content like YouTube videos, so it’s a good testing ground for our forms.

### Check the form behavior without correct settings

Let’s first observe what happens if we try to embed a form without the proper setup.

1. From the form’s **“Embed”** tab in the form properties, copy the provided code snippet.

2. In CloudPages, create a new landing page and drag in an **HTML content block**. Paste the copied code directly into it.

3. Publish the CloudPage. Even if this is published, the form will be blocked due to a connection refusal and will not be displayed.

## How to Configure Your Form for Successful Embedding

Now, let’s go through the steps to **properly configure your form so it displays correctly** when embedded in an external site like CloudPages.

### Step 1: Navigate to the Site Builder

1. In **Salesforce Setup**, search for **“All Sites”**.
2. Select the builder for the **Marketing Landing Page** site you’re using to host your form.

### Step 2: Adjust Security Settings

1. In the Site Builder, click on **“Settings”** (Gear Icon).
2. Go to the **“Security & Privacy”** tab.
3. Under **Clickjack Protection Level**, change the setting to:  
    **“Allow framing of site pages on external domains”**.

### Step 3: Add Trusted Domains

1. Just below the clickjack setting, look for the section labeled **“Trusted Domains for Inline Framing”**.
2. Click **“+ Add Trusted Domain”**.

3. In the pop-up window, enter the **domain** of your **Marketing Cloud Engagement CloudPages URL** (the site where you plan to embed the form).

*Note:* Whether or not the domain ends with a **trailing slash (“/”)** does not matter.

### Step 4: Publish the Site

Once you’ve added the trusted domain, be sure to click **“Publish”** to make the changes effective.

### Important Notes

- **Don’t forget to publish**: The trusted domain setting won’t take effect until the site is published.
- The **Marketing Landing Page site** is intended to function in the background. **You should not add any content to it.**

## Verify the Embedded Form

After completing the setup, I returned to the CloudPages site and refreshed the page. This time, the **signup form displayed correctly** — success!

Even better, submitting the form triggered the connected **Flow**, confirming that everything was functioning as intended.

## Known Issue

Currently, forms cannot be embedded when the site is published in a language other than English.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/issue?id=a028c000010Fw0oAAC&title=marketing-cloud-growth-advanced--cannot-embed-a-form-when-site-is-published-in-languages-other-than-english&source=post_page-----fe21918045e2---------------------------------------)

**Workaround:**  
There is an issue with generating the embed script for languages other than English. In the form’s embed code, locate “/en-US/” and replace it with the language code that matches your site’s language. Then, paste the modified code into the HTML where you want the form to appear.

If the form is created in Japanese, **change “/en-US/” to “/ja/”**.  
*Note: Using “ja-JP” will not display the form, so please be careful.*

You can verify whether the form was created in Japanese by checking the following:

## Final Thoughts

And there you have it — with just a few configurations, we’ve successfully embedded a **Marketing Cloud Growth & Advanced Edition signup form** into an external site using an iframe.

This setup allows you to **quickly capture leads from outside your Salesforce environment**, without the need for additional landing pages or complex integration.

Here are a few key takeaways:

- You don’t need to create or publish a full landing page to use a signup form on an external site. As long as the form and its related flow are properly configured, it will work as expected.

For detailed instructions on how to create and configure signup forms, refer to below article.

[## SFMC Tips #104 : Marketing Cloud on Core: Creating a Signup Form

### Marketing Cloud on Core (Marketing Cloud Growth & Advanced Editions) provides an efficient way to capture new leads by…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea?source=post_page-----fe21918045e2---------------------------------------)

- Even if you edit the content of the form, simply republishing the form will automatically update its display on the external site.
- If the form is unpublished, it will no longer appear on the external website.
- The embed code for the form includes variable information such as “My Domain”. If “My Domain” is set during operation, the embed code already embedded on the external site will not be updated automatically. In that case, please update it manually. Otherwise, the device ID may not be retrieved correctly.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
