# SFMC Tips #131 : Marketing Cloud Next: Tracking External Websites without a Consent Banner

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412

---

# SFMC Tips #131 : Marketing Cloud Next: Tracking External Websites without a Consent Banner

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--467326874412---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--467326874412---------------------------------------)

5 min read

·

Jun 7, 2025

--

Photo by [Juan Ordonez](https://unsplash.com/@juzu_me?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, it is possible to track visitor activities and engagement on **landing pages and external websites**.

### Classification of Web Tracking

Web tracking can be broadly categorized into **four patterns**, based on the **presence of a consent banner** and the **type of page being tracked.**

1. ️️✖️ [Tracking Marketing Cloud landing pages with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73)
2. ✖️️ [Tracking Marketing Cloud landing pages without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52)
3. ✖️️ [Tracking external websites with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c)
4. ⭕️ [Tracking external websites without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412)

In this article, I focus on the method of **tracking visitor behavior after obtaining consent**, specifically:

- **Tracking external websites without a consent banner.**

### 🚨 Important: Changes Introduced in the Winter ’26 Release

The “**wtcp\_id**” **parameter** has been added to the **existing Web Tracking JavaScript SDK (Beacon Script)**.

> ***Important Note:*** *If you configured* ***external tracking before Winter ’26 (mid-October 2025)****, please* ***reconfigure the setup from scratch****.  
> External tracking configurations created* ***before Winter ’26*** *are* ***not compatible with the latest feature updates*** *and may* ***stop working correctly in the future****.*

## Trackable Activities

By configuring web tracking, the following activities can be tracked:

- **Page Views（page-view）**
- **Link Clicks（anchor-click）**
- **Button Clicks（anchor-click）**
- **Form submissions（form-submit）**

### Important Considerations

When tracking **external websites**, the information that can be collected **differs from tracking Marketing Cloud Landing Pages**.

For example, the following information **cannot be captured**:

- **page-scroll-to-bottom event information**
- **Detailed information about clicked links**, such as the **link text or URL**

In addition, **some information about the visitor’s OS and browser** can be viewed in the **DLO (Data Lake Object)**, but **it is not automatically mapped to the Website Engagement DMO**.

If you need to use this information in the **DMO**, configure the **mapping manually as required**.

## Steps to Enable Tracking Without Consent Banner

The procedure for tracking external websites **without a consent banner** is as follows:

1. **Disable tracking consent requirement**
2. **Create a website connector**
3. **Generate the embed code**
4. **Add the embed code to the external website**

## Configuration Steps

### 1. Disable the Consent Banner

Search for **“Web Tracking”** in **Setup**, select **“Consent Banner”**, and turn **“Consent Banner Required”** **Off**.

### 2. Create a Website Connector

Next, select **“Website Connector”** in **Setup**, and click **New**.

### 3. Define the Connector Name

Enter a **Connector Name**, then click **Create**.

### 4. Website Connector Created

The **Website Connector** will be created instantly.

### Spring ’26 Update

With the [**Spring ’26 new feature release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb), the following components — previously required to be installed manually — are now **automatically installed when creating a Website Connector**:

**Data Streams**

- **Web Tracking — Identity (person data)**
- **Web Tracking — Behavioral Events (behavioral data)**
- **MarketingStreamingAppConfig\_Home (campaign association)**

In addition, another improvement introduced in **Spring ’26** allows **a single Web Connector to be reused across multiple campaigns**.

As a result, it is **no longer necessary to create a new connector for each campaign**.

### 5. Create an Embed Code

Next, create an **Embed Code**.  
In the **Embed Code section** that appears after creating the connector, click **New**.

### 6. Configure the Embed Code

Enter an **Embed Code Name**, associate it with a **Campaign**, and enable **“Consent Enabled”** for the consent banner setting. Then complete the configuration.

### 7. Open the Embed Code

The **Embed Code** has now been created. Click the **link**.

### 8. Copy the Embed Code

The **Embed Code** will be displayed on the screen. Copy the code.

### 9. Open the External Website Page

In this article, we will configure the consent banner on **Marketing Cloud Engagement CloudPages** as an example of an external website.

Open the **page editor** and select **Code View**.

### 10. Insert the Embed Code

Insert the copied code **inside the** `<head>` **tag**.

### 11. Insert the Code Snippet

If you are not using the consent banner, insert the following code snippet after the embed code.

```
<script>  
        const consent = {  
            provider: "Salesforce Marketing Cloud",  
            purpose: "Tracking",  
            status: "Opt In"  
        };  
  
        SalesforceInteractions.init({  
            consents: [consent],  
        }).then(() => {  
            SalesforceInteractions.initSitemap({ pageTypes: [] });  
        });  
</script>
```

### 12. Publish the Page

Publish the **CloudPages page**.

This completes the configuration.

## Conclusion

By leveraging this data, you can create more precisely targeted segments and optimize your marketing strategies.

### Segmentation Examples

- **Customers who accessed the website 10 or more times within the past 30 days**  
   *(Example: Customers demonstrating high interest)*
- **Customers who viewed the URL of the product price list page updated this week**  
   *(Example: Customers likely to have a strong interest in pricing)*
- **Customers with 5 or more web accesses within the past 30 days**  
   *(Example: Potential leads requiring follow-up)*
- **Users associated with opportunities lost to competitors, who viewed the introduction page for similar services within the past 30 days**  
   *(Example: Customers offering a chance for re-engagement)*

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
