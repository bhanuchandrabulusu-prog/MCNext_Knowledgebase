# SFMC Tips #190 : Marketing Cloud Next: Merge Fields for Landing Pages

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-merge-fields-for-landing-pages-e07985ecc67f

---

# SFMC Tips #190 : Marketing Cloud Next: Merge Fields for Landing Pages

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e07985ecc67f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e07985ecc67f---------------------------------------)

3 min read

·

Oct 12, 2025

--

Photo by [Mag Pole](https://unsplash.com/@magpole?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of **Marketing Cloud Next Growth & Advanced Edition**, you can now use **merge fields** on landing pages.

This enhancement allows you to **personalize content for each visitor**, capture their attention, and **maximize lead generation**.

## Limitations by Organization

- This feature is **available only for orgs created after Spring ’25**. 💀💀💀
- It’s **not available in SDO environments** (Salesforce Partner demo orgs).

When unavailable, you can still set a **Data Graph** as the data source for your landing page, but the **merge field button won’t appear**.

*Button not displayed*

*Button displayed*

## Using Data Graphs

- **Standard Data Graph**: Display visitor information such as “Name” or “Company Name”.
- **Real-Time Data Graph**: Display dynamic information that changes per visitor, such as “Available Points”.

However, there are a few current limitations:

- **Repeat** components are not supported on landing pages.
- **Image** components cannot use merge fields — meaning dynamic image URLs are not yet supported.  
  \*I also tested this with the **HTML** component, but it didn’t work as expected. It might be an implementation issue on my side, so I plan to investigate further. 🤔

For now, it seems that **only text-based merge fields** are supported on landing pages.

## Key Points for Fallback Design

On landing pages, certain fields may sometimes fail to display as intended. Therefore, it’s important to design your layout so that it looks natural whether the field is displayed or not.

For example, by intentionally **avoiding the use of punctuation marks such as commas**, you can prevent awkward spacing or unnatural phrasing in both cases.

when the field is displayed

when the field is not displayed

Since the optimal approach varies depending on your language’s grammar rules, please adjust the design to suit your local language accordingly.

## Integration with Email

Simply place the landing page URL as a link in your email — when the link is clicked, data such as **Name** or **Company Name** is automatically passed to the landing page.

One key point to remember:  
When a recipient clicks the link, a token like the following is appended to the URL as a parameter:

> *sftoken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE3NjAyNzAxNjgsImV4cCI6MTc2MDI3MDIyOCwiaW5kaXZpZHVhbElkIjoiYWU4YjdhOGUtNWI3NS00M2YzLThjZTgtNjQzMTk1OTAyY2E4IiwidGVuYW50SWQiOiJhMzYwL3Byb2Q5L2Y3YWY4NGUxMDY3YjQxMzM4ZTc4ZjA4YTI0ZjAyYmY2In0.dnCNXH\_jG6NqRggI6aTttUFqqT-9UFJ79A5ZdRbnveo*

If this parameter is removed or modified in any way, the page will revert to the **fallback display**. Since customers might accidentally alter the URL, careful fallback design is crucial.

Also, note that this behavior **requires “click tracking to be enabled”**.  
The per-customer data is included within the click-tracking parameters.

![]()

## Conclusion

As shown in the examples above, adding a **personalized name field** to your landing page can significantly enhance the visitor’s impression.

With this update, you can now **easily deliver more personalized experiences** — be sure to make the most of it.

That’s all for this update!

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
