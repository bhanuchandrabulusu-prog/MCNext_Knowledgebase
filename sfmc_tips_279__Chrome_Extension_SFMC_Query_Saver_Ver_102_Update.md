# SFMC Tips #279 : Chrome Extension SFMC Query Saver Ver. 1.0.2 Update

**Source:** https://medium.com/@marketingcloudtips/chrome-extension-sfmc-query-saver-ver-1-0-2-update-11863e380df6

---

# SFMC Tips #279 : Chrome Extension SFMC Query Saver Ver. 1.0.2 Update

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--11863e380df6---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--11863e380df6---------------------------------------)

5 min read

·

Apr 20, 2026

--

Photo by [Jonathan Cooper](https://unsplash.com/@theshuttervision?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

About a month ago, I shared that **smart grouping** had become available in the Chrome extension “**SFMC Query Saver**”, but even within this short one-month period, updates have continued, and there has been even greater evolution.

[## SFMC Tips #272 : Chrome Extension SFMC Query Saver Ver. 0.2.2 Update

### The Google Chrome extension SFMC Query Saver, which automatically saves queries executed in Query Studio, well known in…

medium.com](/@marketingcloudtips/chrome-extension-sfmc-query-saver-ver-0-2-2-update-79db07a0e298?source=post_page-----11863e380df6---------------------------------------)

What I especially want to highlight this time is that the **version notation has changed from the 0.2 series to the 1.0 series**. With it now becoming **Ver.1.0.2**, it seems reasonable to view this as finally entering an official release version.

Also, this feature is provided by **Matheswaran Kanagarajan**. The **SFMC Automation Viewer** he created is also excellent, so I recommend installing both.

![]()

[**Matheswaran Kanagarajan**](https://www.linkedin.com/in/mathesk/)

## Installation (For Those Who Have Not Installed It Yet)

If you have not installed it yet, you can install it from below.

- **SFMC Query Saver — Chrome Web Store**

[## SFMC Query Saver - Chrome Web Store

### This Extension saves any SQL queries executed in Query Studio.

chromewebstore.google.com](https://chromewebstore.google.com/detail/sfmc-query-saver/bkajbggginfjnjhaiififajmncgdneli?source=post_page-----11863e380df6---------------------------------------)

- **SFMC Automation Viewer — Chrome Web Store**

[## SFMC Automation Viewer - Chrome Web Store

### View SFMC automation details without pausing active automations.

chromewebstore.google.com](https://chromewebstore.google.com/detail/sfmc-automation-viewer/bfdjgmcdnopdhpkfiolfmkcgeadgapmb?source=post_page-----11863e380df6---------------------------------------)

*For how to use Automation Viewer, please refer to a separate article.*

[## SFMC Tips #124 : SFMC Automation Viewer: New Journey Activity Search Feature Added

### A new feature has been introduced to the SFMC Automation Viewer, a Google Chrome extension created by Matheswaran…

medium.com](/@marketingcloudtips/sfmc-automation-viewer-new-journey-activity-search-feature-added-a686a9f10fea?source=post_page-----11863e380df6---------------------------------------)

## Difference Update Details

As differences from Ver.0.2.2, **what is particularly significant is that it has gone beyond the scope of being simply a query saving tool**.

From its previous positioning as “a tool to save queries”, **it has now become much stronger in character as an alternative and complementary tool to Query Studio**.

In particular, the following improvements have been made to address issues that existed in Query Studio.

## ① Query Execution Results Can Be Saved as a Data Extension

Just like Query Studio, queries can now be executed from SFMC Query Saver, and the execution results can be saved as a data extension within the Query Studio folder.

You can easily access the created data extension from the “**Run History**” tab.

Moreover, **the original source data extension definition is preserved**.

- The **same data types** as the original source data extension are retained.  
   (\*Unlike Query Studio, they do not all become text data types.)
- Only the **email address type** is handled as a text type.
- **No ltrim / rtrim** is performed to fit within 255 characters.
- **Primary keys** are also preserved.

This is a very welcome improvement for **sample data creation and validation purposes**.

## ② SELECT \* FROM Is Available

**SELECT \* FROM** can now be used.

In conventional Query Studio, the asterisk could not be used, so fields had to be written each time. It may seem minor, but it is a significant improvement.

## ③ Multiple Queries Can Be Executed in Parallel

Multiple queries can be executed in parallel, and the results of each can be reviewed.

In Query Studio, once one query was executed, you had to wait before executing the next query, but that limitation has been resolved.

In other words, queries like “A” and “B” can be run simultaneously in separate tabs. There is no longer a need to wait for one before running another, improving efficiency.

## ④ Export Is Easy

Exporting execution results has also become easy.

Export itself was possible in conventional Query Studio as well, but being able to do it without screen transitions is a usability improvement.

According to Mathes-san, **the main purpose of this update was to complement the shortcomings of Query Studio**.

That makes a lot of sense.

## Favorites Feature Also Added

In addition, it is now possible to mark queries as “**Favorites**” within smart grouping.

If frequently used queries are added to Favorites, they can be accessed immediately.

Personally, I had been searching my own medium articles each time to retrieve queries, so this was a feature I had wanted for a long time. I am genuinely happy it was added.

## Further Expanded into “Content Builder”

And this time, an **update has also gone beyond the scope of Automation Studio**.

Remarkably, **version history can now be saved when saving emails in Content Builder**.

This surprised me when I tested it. **When you save an email, past versions are automatically saved in the “Email” tab of SFMC Query Saver**.

As expected, rollback to a previous version is not possible, but:

- You can check previous text content
- It can serve as insurance against accidental overwrites

In that sense, it is highly practical.

How was it?

It is packed with very useful features.

If you are used to Query Studio, the operation may feel a little different at first and may be confusing, but once you get used to it, I think it is a very easy-to-use tool.

**It may be possible to view it not simply as a query saving tool, but as a Query Studio complementary tool, and even as a Content Builder support tool**.

I think it is well worth trying for a while, so please give it a try.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
