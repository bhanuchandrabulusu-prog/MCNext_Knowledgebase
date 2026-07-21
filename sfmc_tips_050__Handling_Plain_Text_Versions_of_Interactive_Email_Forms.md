# SFMC Tips #50 : Handling Plain Text Versions of Interactive Email Forms

**Source:** https://medium.com/@marketingcloudtips/handling-plain-text-versions-of-interactive-email-forms-97b764c40607

---

# SFMC Tips #50 : Handling Plain Text Versions of Interactive Email Forms

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--97b764c40607---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--97b764c40607---------------------------------------)

2 min read

·

Jul 31, 2024

--

Photo by [Mikita Yo](https://unsplash.com/@mikitayo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

*The content I’m about to share is not listed in Salesforce help documentation, as far as I know. Therefore, please proceed at your own risk in case of any issues. This method has been used by some of my clients.*

When conducting surveys via email, it is common to include a link in the email body that directs recipients to a survey page. **However, Salesforce Marketing Cloud has a feature called “Interactive Email Forms”, which allows survey forms to be embedded directly within the email body**.

## How to Handle Plain Text Versions in Multi-Part MIME Emails?

Interactive Email Forms are designed for HTML emails and cannot be displayed in plain text versions. **However, it is possible to redirect users to a survey page (Cloudpages) where the survey is displayed**.

**You can use the AMPscript function** `%%=v(@afbCPURL)=%%`.

Here’s an example of what the plain text version might look like:

Newsletter

What is your favorite sport?  
Please answer the survey from the link below:  
`%%=v(@afbCPURL)=%%`

XYZ Corporation

This AMPscript will generate a link to the survey page (Cloudpages) in the text version.

## Configuration Tips

I would like to share an important setup instruction: Please make sure to use “Automatic Fallback”. **As shown in the diagram below, you need to check the “Include Automatic Fallback” box. If you do not do this, the system will not work, and the links will not be displayed**.

![]()

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
