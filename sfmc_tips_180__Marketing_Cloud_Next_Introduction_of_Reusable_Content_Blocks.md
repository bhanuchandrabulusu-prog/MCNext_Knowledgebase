# SFMC Tips #180 : Marketing Cloud Next: Introduction of Reusable Content Blocks

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-introduction-of-reusable-content-blocks-2b50a771fd8c

---

# SFMC Tips #180 : Marketing Cloud Next: Introduction of Reusable Content Blocks

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--2b50a771fd8c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--2b50a771fd8c---------------------------------------)

4 min read

·

Oct 4, 2025

--

Photo by [SHAYAN Rostami](https://unsplash.com/@shayan_rostami?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of Marketing Cloud Next Growth & Advanced Edition, content reusability has been significantly enhanced. In addition to “**Content Blocks**”, which allow you to save a combination of text, images, links, and buttons, the platform now offers a robust system for saving and reusing assets such as “**Email Templates**” and “**Landing Page Templates**”.

Furthermore, Content Blocks support **variation rules**, enabling you to automatically deliver different content to different audiences — making email campaigns even more personalized.

However, there are some current limitations:

- You cannot directly save a block that is still in draft status as a Content Block.
- The ability to save an email in draft status as a template is not included in this release.

All Content Blocks and templates must be created in advance within the CMS Workspace.

## Key Points When Using Content Blocks

When working with Content Blocks, keep the following in mind:

- **Available in Draft Status**  
  Content creators can add blocks to emails even before they’re published. Once the email is published, the draft block will be published simultaneously.
- **Always Shows the Latest Version**  
  Regardless of publication status, the saved latest version is reflected across the canvas, preview screen, and CMS details page.
- **Brand and Style Priority**  
  By default, a Content Block follows the brand settings of the email it’s placed in. However, if the block creator sets brand or style properties within the block itself, those will take priority and remain intact.
- **No Repeater Components**  
  At this time, repeater components cannot be included within a Content Block.

## How to Create a Content Block

1. From the Marketing Workspace, select **Add → “Content Block: Email”**.

2. Add the necessary block components to the canvas and configure the required elements. Note: repeater components cannot be added here.

3. Once complete, save and publish the block.

## How to Use a Content Block in an Email

1. Add the **Content Block** component to the canvas.

2. Click **Select Block**.

3. Choose the desired Content Block and add it. Confirm that the appropriate brand settings have been applied.

4. Configure audience-specific variations as needed.

- In the properties panel, click **New Variation**.

- Define the variation (rule name and conditions).

![]()

- Since all variations start with the same content, replace each variation and the default Content Block with the desired version.

![]()

> *For details on how to configure variations, please refer to the following article.*

[## SFMC Tips #174 : Marketing Cloud Next: How to Set Up Dynamic Content

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can create dynamic content tailored to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-set-up-dynamic-content-3c8ba2c53036?source=post_page-----2b50a771fd8c---------------------------------------)

## Conclusion

It’s especially useful to save reusable content such as headers and footers. In the previous Marketing Cloud Engagement, once content was used in a send, cached versions made updates cumbersome. In contrast, with Marketing Cloud Next, publishing a Content Block automatically updates all linked emails. This greatly reduces operational overhead and makes content management much easier.

I highly recommend taking full advantage of this feature.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
