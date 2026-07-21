# SFMC Tips #95 : Marketing Cloud Next: Email Contents and Components

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-content-creation-and-components-bf9046db9978

---

# SFMC Tips #95 : Marketing Cloud Next: Email Contents and Components

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--bf9046db9978---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--bf9046db9978---------------------------------------)

7 min read

·

Apr 1, 2025

--

Photo by [Sunder Muthukumaran](https://unsplash.com/@sunder_2k25?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I’ll explore the basic content functionalities available in **Marketing Cloud Next Growth & Advanced Edition**. The focus will be on how to create content and use fundamental components, along with specific instructions and important considerations.

## Overview of the Content Tab

When you open the **Content** tab in Marketing Cloud Growth & Advanced Edition, you’ll see the **Content Workspace** for Marketing Cloud. This workspace is equivalent to **Content Builder** in Marketing Cloud Engagement, and it houses all saved content, such as email messages and images.

## How to Create Content

**Step 1**: Click the **Add** button.  
From the dropdown menu on the far-right, select **Content**.

**Step 2**: Choose a content type.  
Select **Email** and click the **Create** button.

**Step 3**: Enter the necessary information:

- **Email Definition Name**
- **API Reference Name**
- **CAN-SPAM Classification** (choose either **Promotional** or **Transactional**)

## Content Creation Notes

### About the Company Address

Previously, when creating emails in Marketing Cloud Next, entering the company “Address” merge field was required for promotional emails in order to comply with CAN-SPAM requirements.

However, **this is no longer mandatory**, and the following type of error is no longer displayed.

If you want to display the address, enter the following merge field.

Company “Address” Merge Field  
 Merge Field Button ＞ Organization ＞ Address {!$organization.Address}

Example of the input screen in the settings

### About the Unsubscribe URL

Although a **Unsubscribe URL** is mandatory under CAN-SPAM requirements, failing to set one will not result in a validation error, and email sending will still be possible. This is because some companies use custom unsubscribe URLs.

*If you click this link, you will be unsubscribed with a single click. The only indication is the text* ***“Successfully unsubscribed”*** *displayed in the upper-left corner. Only the communication subscription selected in that email will be opted out. It does not affect any of your other communication subscriptions.*

**Pro Tips:** In the **Preview and Test**, clicking on the unsubscribe URL will record the Communication Subscription Channel Type as `dummyCsctToken`. This ensures that no registered subscriptions are opted out.

## Setting Brand

I’ve also written about brand settings for email messages in another article. You can find the details here:

[## SFMC Tips #94 : Marketing Cloud on Core: Selecting a Brand for Your Content

### When creating new email content in Marketing Cloud on Core (Marketing Cloud Growth Edition / Advanced Edition), the…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-selecting-a-brand-for-your-content-97706e59ed1b?source=post_page-----bf9046db9978---------------------------------------)

## Setting Subject Lines and Preheaders

The **Subject Line** and **Preheader** can be configured in the following section:

**Einstein AI** offers an auto-generation feature for subject lines. And you can also use a **Data Graph** to leverage:

- **Merge Fields** (e.g., inserting a recipient’s name).
- **Dynamic Content** for personalized messaging.

### Rules Tab

The **Rules** tab displays variations for dynamic content if it is being used. If you are not using dynamic content, you can simply ignore this tab.

## Available Components

Currently, the following components are available for use:

### Basic Componets

- **Button**: Quickly create buttons with links.
- **Divider**: Add dividers between sections.
- **Heading**: Easily add headings.
- **HTML**: Allows you to directly input code.
- **List**: Create bullet points or numbered lists.
- **Paragraph**: Create text in paragraph format.

### Layout Componets

- **Section**: Adjust the layout to organize your content.
- **Repeat:** Display repeating items.
- **Content Block:** Define, save, and reuse content blocks.

### Media Componets

- **Image**: You can insert images and set up links.

## Component Details

Here are the details of each component:

### Button Component

Easily create buttons with links.

**Action Settings**: The button component allows you to assign Salesforce CMS content or any URL to the button.

### Divider Component

Simply drag and drop to place a divider. It’s perfect for visually separating sections.

### Heading Component

A text component specifically for headings. Predefined styles are applied, allowing you to quickly create headings.

### HTML Component

You can directly input HTML source code to create complex content. It’s also convenient for copying and pasting HTML code created in other email tools. Example HTML created in Marketing Cloud Engagement is shown below.

### List Component

Quickly create bullet-point or numbered lists.

> ***Note:*** *This list component has a significant limitation. While copying from the list is possible,* ***pasting into the list is not supported****.*

### Paragraph Component

This component is used for paragraph-style text. You can directly type your content into the canvas.

**Enhanced Rich Text Editor for Email Styling**  
You now have more precise control over text styling and spacing within email layouts.

Key enhancements include:

- Emojis
- Font family, font size, and line height
- Text color and background color
- Quotes (blockquotes)
- Horizontal rules

Traditional Rich Text Editor

New Rich Text Editor

### Section Component

The section component is typically placed first when creating new content. It is mainly used to adjust the layout.

**Layout Settings**: Click the up arrow icon to open the layout settings screen.

Several layout options are available.

For mobile views, selecting “Stack columns on mobile” will arrange the content vertically on smartphones.

### Image Component

You can insert images that are managed in the CMS. It’s possible to set captions (descriptions) and URL links for the images. Additionally, you can easily configure the image as dynamic content directly from this screen.

### **Repeat Component**

By displaying content repeatedly, you can showcase recommended products or present articles tailored to user preferences. This feature was introduced in Summer ‘25.

Details are explained in the article below.

[## SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Summer ’25 release introduces a brand-new…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----bf9046db9978---------------------------------------)

### **Content Block Component**

Predefined blocks can be combined, saved, and reused. This feature was introduced in Winter ‘26.

Details are explained in the article below.

[## SFMC Tips #180 : Marketing Cloud Next: Introduction of Reusable Content Blocks

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, content reusability has been…

medium.com](/@marketingcloudtips/marketing-cloud-next-introduction-of-reusable-content-blocks-2b50a771fd8c?source=post_page-----bf9046db9978---------------------------------------)

### Send Emails with PDF Attachments

In the Spring ’26 new feature release, it is now possible to send emails with PDF attachments. I have explained this in the following article.

[## SFMC Tips #258 : Marketing Cloud Next: Send Emails with PDF Attachments

### As a new feature released in Spring ’26 for Marketing Cloud Next Growth & Advanced Edition, it is now possible to send…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-emails-with-pdf-attachments-78eee857af44?source=post_page-----bf9046db9978---------------------------------------)

## Conclusion

Currently, there may be some limitations compared to Marketing Cloud Engagement in terms of usability. However, with upcoming feature expansions, I expect new components that could match or even exceed those in Marketing Cloud Engagement.

That’s all for now!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
