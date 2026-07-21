# SFMC Tips #172 : Marketing Cloud Next: Setting Domains for Email Tracking Links

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d

---

# SFMC Tips #172 : Marketing Cloud Next: Setting Domains for Email Tracking Links

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1195027cb56d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1195027cb56d---------------------------------------)

5 min read

·

Sep 11, 2025

--

Photo by [Junior REIS](https://unsplash.com/@juniorreisfoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, when a recipient clicks a link in an email, the tracking link typically appears with a domain like this:

```
https://xxxxx.tracking.e360.salesforce.com/click?.....  
  
For Example: https://cdp91.tracking.e360.salesforce.com/click?.....
```

You can replace this **default tracking link domain** with a **custom, branded domain** unique to your company.

### **Note:**

- Only **one domain** can be configured.
- This domain must be **different** from your custom landing page domain and SMS short link domain.

This setup cannot be completed by the marketing team alone. Preparation is required, so please coordinate with your IT team in advance.

### Required Preparations:

- A **CA-signed HTTPS certificate**
- DNS record configuration at your **domain registrar**

## Preparing a CA-Signed Certificate

### **Step**

1. In **Setup**, search for **“Certificate”** and open **Certificate and Key Management**. Click “**Create CA-Signed Certificate”**.

2. Fill in the required details and save.

### Example configuration:

- **Label:** CASignedCert\_10Sep2025 (display name for Salesforce admin use)
- **Unique Name:** CASignedCert\_10Sep2025 (API name for Salesforce admin use)
- **Common Name:** click.xxx.com (the **subdomain** for tracking links)
- **Organization:** XXX Company (official company name)
- **City:** Minato-ku (company location)
- **Country Code:** JP (2-letter country code)
- **Key Size:** 2048 (recommended)
- **Email Address:** abc@xxx.com
- **Department:** IT, etc.
- **State/Province:** Tokyo (company location)

Note: After saving, only the Label and Unique Name can be edited.

3. Open the saved record and click **Download Certificate Signing Request**. This generates a **.csr** file.

4. Send the CSR file to a **Certificate Authority (CA)**. [There are also services offering free certificates valid for 3 months](/@marketingcloudtips/marketing-cloud-next-creating-a-free-digital-certificate-ssl-8e8b43becd9b).

5. Once the CA returns the signed file, open the record of the CA-signed certificate you created earlier. Click “**Upload Signed Certificate”**.

6. Upload the file and save.

7. The record will now be marked as **“Active”**.

## Email Tracking Link Domain Settings

### **Step**

1. Navigate to **Setup > Links** and click **Create New**.

2. Enter the **subdomain** you want to use for email tracking links, select the **CA-signed certificate** you created earlier, and save.

**3.** When first registered, the status will be **Inactive**. Click **Show Details**.

**4.** Register a **CNAME record** in your DNS so that your custom domain points to Salesforce. Copy the provided information and configure it in your DNS.

5. Once the DNS entry is propagated across the internet, toggle the status to **On**.

**6.** The status will now show **“Active”**, completing the setup.

7. When you send emails, the tracking link URL will now reflect your **custom domain**.

![]()

## When the Certificate Expires

Once the certificate expires, it will be displayed in red in the management screen as shown below.

⚠️ Depending on the browser behavior, links with expired certificates may display an error screen like the one below, and users will not be able to navigate directly to the destination website.

Salesforce sends reminder emails with the subject line “One or more of your Salesforce certificates expires soon” **10 days and 1 day before** the expiration date of your registered certificates.

If you temporarily need to revert to using links such as “https://xxxxx.tracking.e360.salesforce.com/click?.....”, search for “Links” in Setup and remove the configured domain. However, please note that removing the domain will not improve the status of emails that have already been sent.

Once a domain has been activated, it cannot be disabled, so it must be deleted instead.

*Note: In rare cases, cached settings may remain, and emails may still be sent using the deleted domain. Please be aware of this behavior.*

## Closing Notes

By setting a domain for email tracking link URLs, the following benefits can be expected:

✅ **Improved Brand Trust**  
 By default, tracking links use an external domain like `xxxxx.tracking.e360.salesforce.com`. Using your own branded domain helps recipients recognize the links as **official**, increasing trust and click-through rates.

✅ **Higher Click & Open Rates**  
 Recipients may hesitate to click links on unfamiliar domains. Displaying your own branded domain lowers this psychological barrier and improves engagement.

✅ **Domain Alignment and Stronger Authentication**  
 When combined with **SPF / DKIM / DMARC**, this ensures consistency between the sender and link domain, improving email authentication scores and helping protect against phishing.

As you can see, there are many advantages to setting up a custom domain for your email tracking links, so it’s highly recommended to consider this configuration.

That’s all for this guide.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)

### Series on Domain Configuration in Marketing Cloud Next

1️⃣ [Steps for Email Domain Authentication](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d)  
2️⃣ [Adding From Addresses & Reply Mail Management](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258)  
3️⃣ [Setting Domains for Landing Pages](/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663)  
4️⃣ [Setting Domains for Email Tracking Links](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d)
