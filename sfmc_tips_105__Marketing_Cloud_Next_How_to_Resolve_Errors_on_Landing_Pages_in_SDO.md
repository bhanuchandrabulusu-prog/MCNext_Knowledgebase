# SFMC Tips #105 : Marketing Cloud Next: How to Resolve Errors on Landing Pages in SDO

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-how-to-resolve-errors-on-landing-pages-in-sdo-644dee92aa8e

---

# SFMC Tips #105 : Marketing Cloud Next: How to Resolve Errors on Landing Pages in SDO

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--644dee92aa8e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--644dee92aa8e---------------------------------------)

2 min read

·

Apr 23, 2025

--

Photo by [Michael C](https://unsplash.com/@michealcopley03?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article is intended for Salesforce partners using Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) in an SDO environment.

Previously, I introduced the ability to create a **signup form**.

[## SFMC Tips #104 : Marketing Cloud on Core: Creating a Signup Form

### With Marketing Cloud on Core (Marketing Cloud Growth / Advanced Edition), you can easily create a “Signup Form” on a…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea?source=post_page-----644dee92aa8e---------------------------------------)

However, some users may encounter an issue where clicking the generated URL of a published landing page results in an error. This guide provides a workaround to resolve this issue.

## Steps to Resolve the Issue

### **1. Access Marketing Landing Pages Builder**

Navigate to **Setup > Digital Experiences > All Sites** and click on the **Marketing Landing Pages** Builder.

### 2. Adjust the Guest User Profile

From the left menu, click the gear icon, select **General**, and then click on **Marketing Landing Pages Profile** under **Guest User Profile**.

### 3. Update Login IP Ranges

Go to **System > Login IP Ranges**.

And remove the listed IP restrictions.

After completing these steps, your landing pages should display correctly.

That’s all for now. 🚀

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
