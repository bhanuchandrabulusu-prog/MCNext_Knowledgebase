# SFMC Tips #119 : Marketing Cloud Next: Freedom in Design with HTML Code View

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-freedom-in-design-with-html-code-view-3673788cee5a

---

# SFMC Tips #119 : Marketing Cloud Next: Freedom in Design with HTML Code View

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3673788cee5a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3673788cee5a---------------------------------------)

3 min read

·

May 21, 2025

--

Photo by [Jeremy Bishop](https://unsplash.com/@jeremybishop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

[*Currently, there is a bug affecting organizations that were* ***not provisioned in English****, where the buttons to switch to* ***Code View*** *or* ***Plain Text*** *are not displayed. In my environment, the buttons appear when the language is set to Japanese, but they disappear when I switch the language to English*](https://help.salesforce.com/s/issue?id=a02Ka00000mm6AmIAI)*.*

![]()

In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), email creation was previously limited to template-based designs. However, with the new feature introduced in the **Summer ’25 release**, you can now create emails using custom **HTML** and **CSS** without relying on templates.

[## SFMC Tips #106 : Marketing Cloud on Core: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----3673788cee5a---------------------------------------)

This update provides unparalleled control over the finer details of email design. Additionally, it allows you to convert existing template-based emails into HTML format, enabling detailed customization of structure and stylesheets. Below, I’ll walk you through the steps for conversion and highlight important considerations.

### Steps to Convert to HTML Format

**1. Click the “Code View” Toggle**  
Click the “Code View” toggle located at the top of the Content Builder.

**2. Preview HTML**  
In the “Code View” tab, a preview of the HTML will be displayed. At this point, the code is locked and cannot be edited yet.

**3. Click “Convert to HTML”**  
Within the “Code View” tab, click the “Convert to HTML” button.

**4. Review the HTML Email**  
The email will then be converted to HTML format, which you can edit.

### Key Considerations When Converting to HTML

1. **Restricted Drag-and-Drop Functionality**  
   After conversion, you cannot add or edit components in Content Builder using drag-and-drop.
2. **Limited Style Adjustments**  
   The “Styles” tab for design changes will no longer be available.
3. **Removal of Dynamic Content**  
   The following features will be disabled and removed from your email:

- **Repeater**
- **Conditional Logic**
- **Content Variants**

**Note: Irreversible Changes**  
Once converted to HTML, you cannot revert the email back to its original template format.

### How Does This Compare to Marketing Cloud Engagement?

In Marketing Cloud Engagement, the “Code View” tab also allows HTML previews but locks editing. To make modifications, you must copy the HTML and create a new HTML-based email.

In contrast, Marketing Cloud Growth & Advanced Edition lets you use the “Convert to HTML” feature within the same email message. However, you should keep the following points in mind:

- The conversion process cannot be undone.
- Certain functionalities will be restricted.

While this new feature offers great convenience, careful planning is necessary to avoid unintended limitations. Leverage this update to streamline your email creation process and achieve a more tailored design experience.

That’s all for now — happy designing!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
