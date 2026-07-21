# SFMC Tips #129 : Marketing Cloud Next: Tracking Landing Pages without a Consent Banner

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52

---

# SFMC Tips #129 : Marketing Cloud Next: Tracking Landing Pages without a Consent Banner

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d23c0ba6da52---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d23c0ba6da52---------------------------------------)

4 min read

·

Jun 6, 2025

--

Photo by [Tim Hüfner](https://unsplash.com/@huefnerdesign?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, it is possible to track visitor activities and engagement on **landing pages and external websites**.

### Classification of Web Tracking

Web tracking can be broadly categorized into **four patterns**, based on the **presence of a consent banner** and the **type of page being tracked.**

1. ️️✖️ [Tracking Marketing Cloud landing pages with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73)
2. ⭕️ [Tracking Marketing Cloud landing pages without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52)
3. ️️✖️ [Tracking external websites with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c)
4. ✖️ [Tracking external websites without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412)

In this article, I focus on the method of **tracking visitor behavior without obtaining consent**, specifically:

- **Tracking Marketing Cloud Landing Pages without a consent banner.**

## Trackable Actions

By enabling **Web Tracking**, the following visitor activities on **Marketing Cloud Landing Pages** can be tracked:

- **Page views**
- **Scrolling to the bottom of the page**
- **Link clicks**
- **Button clicks**
- **Form submissions**

## Requirements for Enabling Tracking Without Consent

To track Marketing Cloud landing pages **without a consent banner**, the following requirements must be met:

- **Data Cloud Integration**
- **Relaxation of CSP (Content Security Policy)**
- **Adding Event Tracking Code to the Head Markup of Landing Pages**

## Configuration Steps

***Prerequisite:*** *It is fine to keep* ***Setup → Web Tracking → Consent Banner******enabled****. This setting is* ***only used for external websites****.*

### 1. Open the Marketing Landing Page Builder

First, search for **“All Sites”** in **Setup**, and select the **Marketing Landing Page Builder**.

### 2. Open Security and Privacy Settings

Click **Settings (gear icon)** and select **Security and Privacy**.

### 3. Change the Security Level

From the **Security Level** dropdown menu, select:

- **Relaxed CSP: Permit Access to Inline Scripts and Allowed Hosts**

### 4. Add the Data Cloud Integration

Next, select **Integration**.  
Find **Data Cloud** and click **Add to Site**.

> ***Note:*** *Do* ***not*** *add* ***“Data Cloud Web Tracking Consent Banner”*** *(shown in the upper-right of the screen) to the site.  
> If it is already enabled,* ***disable it****.*

### 5. Enable Data Cloud

Turn the **toggle to Enabled**, associate the **Data Space**, and click **Save**.

> ***Note:*** *Enabling* ***Data Cloud*** *may take some time. Refresh the page with* ***F5*** *and check the status.*

### 6. Open Advanced Settings

Next, select **Advanced**.

### 7. Insert the Script

Click **Edit Head Markup**, copy the following code, and paste it into the **Head Markup** section. Then **save** the settings.

```
<script>  
document.dispatchEvent(  
        new CustomEvent('experience_interaction', {  
            bubbles: true,  
            composed: true,  
            detail: {  
                name: 'set-consent',  
                value: true,  
            },  
        })  
    );  
</script>
```

### 8. Publish the Site

To start **tracking visitor behavior**, click **Publish**.

### Important Considerations

- The **Marketing Landing Page site** is designed to **run in the background**, so **do not add additional content**.
- Changes to settings **will not be reflected until the site is published**.
- If you modify the **banner text or style settings after publishing**, you must **republish the site again**.

This completes the configuration.

### 9. Verify the Script

Finally, check the **source code of the published landing page** and confirm that the script has been inserted.

Setup is now complete.

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
