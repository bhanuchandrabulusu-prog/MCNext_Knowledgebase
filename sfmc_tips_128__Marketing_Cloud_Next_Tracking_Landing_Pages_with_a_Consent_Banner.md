# SFMC Tips #128 : Marketing Cloud Next: Tracking Landing Pages with a Consent Banner

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73

---

# SFMC Tips #128 : Marketing Cloud Next: Tracking Landing Pages with a Consent Banner

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3672df5f9e73---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3672df5f9e73---------------------------------------)

5 min read

·

Jun 6, 2025

--

Photo by [Yiran Ding](https://unsplash.com/@yiranding?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, it is possible to track visitor activities and engagement on **landing pages and external websites**.

### Classification of Web Tracking

Web tracking can be broadly categorized into **four patterns**, based on the **presence of a consent banner** and the **type of page being tracked.**

1. ⭕ [Tracking Marketing Cloud landing pages with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73)
2. ✖️ [Tracking Marketing Cloud landing pages without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52)
3. ️️✖️ [Tracking external websites with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c)
4. ✖️ [Tracking external websites without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412)

In this article, I focus on the method of **tracking visitor behavior after obtaining consent**, specifically:

- **Tracking Marketing Cloud Landing Pages with a consent banner.**

## **Trackable Actions**

By enabling **Web Tracking**, the following visitor activities on **Marketing Cloud Landing Pages** can be tracked:

- **Page views**
- **Scrolling to the bottom of the page**
- **Link clicks**
- **Button clicks**
- **Form submissions**

### **Important Considerations**

If **consent for tracking is required**, the **first page view of a website visitor is not recorded**, because it occurs **before consent is obtained**.

**Note:** The [**Summer ’25 release notes**](https://help.salesforce.com/s/articleView?id=release-notes.rn_mktg_reporting.htm&release=256&type=5) state that the functionality was improved so that the **first page view of website visitors would also be tracked**. However, in practice, it appears that this improvement has **not actually been implemented**.

## Requirements for Enabling Consent-Based Tracking

To track Marketing Cloud landing pages with a Consent Banner, the following are required:

1. **Banner Design Configuration**
2. **Data Cloud Integration**
3. **Integration of Data Cloud Web Tracking Consent Banner**

## Configuration Steps

As a first step, you should **configure the design of the consent banner**.  
 This is because if you edit the consent banner **after the site has been published**, you will need to **republish the site again**.

> ***Important:*** *If you change the consent banner settings, you must* ***republish the Marketing Landing Page site****.*

### **1. Enable the Consent Banner**

Search for **“Web Tracking”** in **Setup**, select **“Consent Banner”**, and turn **“Require Consent Banner”** **On**.

### **2. Customize the Banner Content**

Customize the **default text** and add items such as a **link to your company’s privacy policy**.  
You can also customize the **banner position, font, and colors** as needed, and then **save** the settings.

**What is Privacy Policy Link Text?**  
This is the link text that directs users to your privacy policy page. It allows users to review your data processing policies and understand how their data is used.

- Examples: “Privacy Policy”, “About Privacy”, etc.

**What is Information Link Text?**  
This is the link text that provides users with more detailed information. Clicking it navigates to a page or section that explains cookies and data collection in detail.

- Examples: “Learn more”, “View details”, etc.

> ***Note:*** *You can make the above changes, but the button text on the consent banner —* ***Accept*** *and* ***Reject*** *— cannot be modified.*

### **3. Open the Marketing Landing Page Builder**

Next, search for **“All Sites”** in **Setup** and select the **Marketing Landing Page Builder**.

### **4. Add the Data Cloud Integration**

Click the **Settings (gear icon)** and select **“Integration”.**  
 Then click **“Add to Site”** under **Data Cloud**.

### **5. Enable Data Cloud**

Turn the **toggle to Enabled**, associate the **Data Space**, and click **Save**.

### **6. Add the Data Cloud Web Tracking Consent Banner**

Next, click **“Add to Site”** for **Data Cloud Web Tracking Consent Banner**.

### **7. Enable the Consent Banner**

Turn the **toggle to Enabled**, then click **Save**.

### **8. Wait for Activation**

Wait until each **Enabled status (green icon)** is completed.

> ***Note:*** *Enabling* ***Data Cloud*** *may take some time. Refresh the page with* ***F5*** *and check the status.*

### **9. Publish the Site**

To start **tracking visitor behavior**, click **Publish**.

### Important Considerations

- The **Marketing Landing Page site** is designed to **run in the background**, so **do not add additional content**.
- Changes to settings **will not be reflected until the site is published**.
- If you modify the **banner text or style settings after publishing**, you must **republish the site again**.

This completes the configuration.

### **10. Confirm the Consent Banner**

Finally, open the **Marketing Cloud Landing Page**, and you will see a **consent banner displayed as shown below**.

If it appears, the setup has been completed successfully.

## Conclusion

By utilizing this data, you can create highly refined segments to optimize your marketing strategies.

### Segmentation Examples

- **Customers who accessed the website 10 or more times within the past 30 days**  
  (Example: Customers demonstrating high interest)
- **Customers who viewed the URL of the product price list page updated this week**  
  (Example: Customers likely to have a strong interest in pricing)
- **Customers with 5 or more web accesses within the past 30 days**  
  (Example: Potential leads requiring follow-up)
- **Users associated with opportunities lost to competitors, who viewed the introduction page for similar services within the past 30 days**  
  (Example: Customers offering a chance for re-engagement)

> *When you configure this web setting, a large number of* ***Anonymous User*** *profiles may be created.*
>
> *If you want to exclude anonymous users, configure a* ***Data Space Filter*** *on the relevant profile source with the following condition:*
>
> ***- isAnonymous NOT EQUALS 1***
>
> *This filter excludes anonymous user profiles, allowing you to work only with non-anonymous profile data.*

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
