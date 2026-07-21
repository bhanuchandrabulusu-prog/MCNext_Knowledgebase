# SFMC Tips #189 : Marketing Cloud Next: Hidden Fields and Default Values in Forms

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-hidden-fields-and-default-values-in-forms-a817f76c4b2e

---

# SFMC Tips #189 : Marketing Cloud Next: Hidden Fields and Default Values in Forms

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a817f76c4b2e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a817f76c4b2e---------------------------------------)

5 min read

·

Oct 10, 2025

--

Photo by [Avi Naim](https://unsplash.com/@avinaim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843), the Marketing Cloud Next Growth & Advanced Edition introduced new form features: **Hidden Fields** and **Default Values**.

With this update, you can efficiently collect important information on forms while reducing the input burden for users. As a result, it becomes possible to **increase conversion rates** and **gain deeper insights into campaign engagement**.

**Hidden Fields:**  
 Automatically capture information such as Campaign Name or Lead Source Page from URL parameters.

**Default Values:**  
 Predefine values that users do not need to enter manually.

These features are available for the following Input component types:

- **Checkbox**
- **Dropdown**
- **Number**
- **Plain Text**
- **Text Area**

In this article, I will walk through the steps to configure **Hidden Fields** and **Default Values**.

> *You asked whether it’s possible to pre-populate a form with subscriber information that has already been retrieved. As* [*François Perret explains in his article*](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-prefill-forms-email-ctas/)*, this can be achieved by embedding Data Graph values into the CTA (such as a button) as URL parameters. However, there are limitations on the types of data that can be pre-filled, and certain fields — such as email address types — cannot be used. Because of this, it seems we’ll need to wait for future updates to the standard functionality.*

### **Example Setup: Capturing “Lead Source Page” via URL Parameter**

1. First, create a custom field on the Lead object called **Lead Source Page** (Text type).

2. From the Campaign Flow, create a new **Signup Form**.

3. Open the form editor.

4. Click **Add Data Source**.

5. Configure it so that Leads can be retrieved.

6. Drag and drop the previously created custom field **Lead Source Page** onto the form canvas.

7. Open **Lead Source Page**, check **Hide this field**, and select **URL Parameter**.

- This time, instead of setting a static value, I’ll input the URL parameter **“utm\_content”** (used for page or CTA variations) to dynamically retrieve its value.
- Set a fallback value of “**Unknown**” in case the parameter is not captured.

8. Save once and navigate to **Flow Builder**. Form publishing must be done from Flow Builder, so do not publish yet.

9. In Flow Builder, open the **Create Lead** element and click **Add Field**.

10. Map the Lead custom field **Lead Source Page** to the value captured from the form.

11. Complete the **Consent Creation** element. (Details omitted.)

12. Save and activate the flow. \*Activating the flow will also publish the form automatically.

13. Once the flow is active, return to the Campaign Flow page and open the landing page.

14. After publishing, aliases cannot be changed, so adjust the alias if necessary from the **URL** tab.

15. Complete and publish the landing page. In this example, I published directly from the **Content** tab without editing.

16. Go to the **URL** tab and confirm the published URL for the available landing page.

17. The published URL for immediate use can now be obtained:

```
https://na1740989000474.my.site.com/lp/landing-page/rba-campaign-page
```

18. Append the **utm\_content** parameter to the URL and start using it. For example, include it in a QR code in a brochure:

```
https://na1740989000474.my.site.com/lp/landing-page/rba-campaign-page?utm_content=RBA+Campaign+Page
```

19. Open the parameterized URL and fill out the form.

20. Verify that the Lead record’s **Lead Source Page** field contains the value from the parameter. Success!

21. For confirmation, fill out the form using a URL without the parameter. The fallback value **Unknown** should populate the field. This also works successfully.

## Conclusion

Until now, the lack of hidden fields may have limited how effectively forms could be used. However, with this new feature, the usability of forms has improved dramatically.

Beyond the use case introduced here, there are many other ways to leverage these features. I encourage you to experiment freely and adapt them to your own campaigns and flows.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
