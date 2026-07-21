# SFMC Tips #277 : Marketing Cloud Next: Custom Preference Page Setup

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-custom-preference-page-setup-311bc587f406

---

# SFMC Tips #277 : Marketing Cloud Next: Custom Preference Page Setup

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--311bc587f406---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--311bc587f406---------------------------------------)

4 min read

·

Apr 15, 2026

--

Photo by [Marie-Michèle Bouchard](https://unsplash.com/@minusculemarie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition, in addition to the standard preference page, it is now possible to create a **custom preference page** that matches your brand image, allowing customers to manage their subscriptions (opt-in/opt-out), such as email, by themselves.

- *It has been available in production environments since April 16, 2026!*

Previously, the standard preference page only allowed selecting which subscriptions to display, and no other changes could be made. However, by using a custom preference page, **it is now possible to provide a consistent and trustworthy experience aligned with your brand image**.

In this article, I will explain the setup steps for this new feature, the custom preference page.

## Setup Steps

1. In the settings screen, go to Marketing Cloud > Marketing Features, select “**Preference Page Customization**”, and confirm that the custom preference page is “**Enabled**”.

2. Click the “**Content**” tab, select the Marketing Cloud workspace, and click “Add — Content”.

3.Select “**Preference Page**” and start creating it.

4. Similar to a landing page, the Experience Builder screen will be displayed. Configure various settings here.

**Considerations**

- **The button in the “Submit Buttons” component cannot be edited**
- **“Links” can be used**
- **“Merge fields” cannot be used**

5. Use the “**Subscription List**” **component** to add channel types and the subscriptions you want to display.

**Considerations**

- The customer’s **email address** is automatically populated in “**Contact Information**”

6. After completing the setup, save and publish.

**7.** Go to the “**Consent**” tab, and from the action menu, set the created preference page as “**Set as Default**”.

8. Set the default preference page for the current business unit.

9. Create an email, include a link to the preference page, then save and publish it.

10. If the following error occurs when publishing, the cause is that “the preference page is not set as default”.

Displayed error message:  
*Something’s not right with your preference page. Your Salesforce admin can resolve the issue in Preference Manager.*

11. After publishing the email, send it.

12. Click the preference page link in the received email.

13. Confirm the display of the preference page.

**Note**

- This has been tested in an SDO org. If you encounter the error “**URL No Longer Exists**”, it is likely caused by “**Login IP Ranges**”. Please refer to the section “Common Pitfall When Viewing the SDO Landing Page” in [this article](/@marketingcloudtips/marketing-cloud-next-basic-setup-procedure-for-the-demo-environment-be441f7c37d8) and remove the restriction accordingly.

**Considerations**

- The display order of subscriptions is random
- It is currently not possible to fix the order (e.g., Brand A → Brand D)

How was it?

These are the features of the custom preference page currently available.

**Was it at the level of customization you expected?**

Since this feels like an initial release, we can hope that it will become more flexible and customizable in the future.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
