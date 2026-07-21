# SFMC Tips #171 : Marketing Cloud Next: Setting Domains for Landing Pages

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663

---

# SFMC Tips #171 : Marketing Cloud Next: Setting Domains for Landing Pages

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6367a4c1e663---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6367a4c1e663---------------------------------------)

6 min read

·

Sep 9, 2025

--

Photo by [Marco J Haenssgen](https://unsplash.com/@marcohaenssgen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce, each organization is automatically assigned a default domain (e.g., https://data-drive-1574.my.salesforce.com), which can be customized to match your company’s brand. This allows you to change the domain used in your landing page URLs as well.

There are two ways to customize your domain, and you can configure either one or both, depending on your needs:

- **My Domain (simple change):** Modify only the subdomain portion while keeping `my.salesforce.com` (e.g., `https://xxxxxxx.my.salesforce.com`).
- **Custom Domain (full change):** Replace it with your company-owned domain (e.g., `www.example.com`).

If both are configured, you will be able to choose from two different landing page URLs as follows.

## My Domain (simple change)

In my environment, the default domain was `https://data-drive-1574.my.salesforce.com`. I updated the subdomain to `nac-plus`, so now it is accessible at `https://nac-plus.my.salesforce.com`.

With this change:

- Clicking the old default URL will automatically redirect to the new one.
- All previously created landing page URLs will automatically switch to the new subdomain.

> ***Cases where the switch does not happen automatically:*** *For example, if you have placed an “****embed code snippet****” for a form on an external web page, that code will not be updated automatically. In such cases, you need to manually replace it with the new code.*

### Setup Steps

1. Open “**My Domain”** from Setup.
2. Enter your desired domain name and check its availability.
3. Provision the domain (prepare it and make it available).
4. If both steps 2 and 3 are marked as complete, the domain is ready to be released.

After release, the login page URL will also change to the new domain.

![]()

> ***Note:*** *Since the login page URL changes, you may experience login issues for about 10 minutes immediately after the release.*

## Custom Domain (full change)

To serve **Marketing Landing Pages (Experience Cloud sites)** using your company-owned domain, you need to add and activate the domain. After that, add a **Custom URL**.

> ***Note:*** *To serve sites with your own domain, your DNS provider must support* ***ANAME records, ALIAS records, or CNAME flattening****. If these are not supported, you cannot proceed. Also,* ***make sure you review the*** [***prerequisites***](https://help.salesforce.com/s/articleView?id=platform.domain_mgmt_prereqs.htm&type=5) ***before using this feature****. Please note that I cannot take responsibility if the configuration cannot be completed.*

### Steps

1. From **Setup**, go to **Domains** and click **Add a Domain**.

2. Enter the **domain name**. If necessary, set up an appropriate subdomain, such as `pages.mail.nac-care.com`.

3. In Marketing Cloud Next, it is recommended to select the option **“Serve the domain with the Salesforce Content Delivery Network (CDN)”**.

- A shared SSL certificate will be used, meaning **you can use SSL for free**.

4. Next, check the option **“Use the Salesforce CDN for Commerce LWR sites or sites hosted on Experience Delivery”**.

- With the box checked → Salesforce CDN partner will be **Cloudflare**.
- With the box unchecked → Salesforce CDN partner will be **Akamai**.

### Adding CNAME Records to DNS

The detailed DNS setup steps are not covered here, but you can find the basic procedure in Salesforce Help. Please work with your IT team to ensure it is properly configured: [Salesforce Help Document](https://help.salesforce.com/s/articleView?id=platform.domain_mgmt_update_dns.htm&type=5)

Typically, you will need to add two CNAME records like the following (the API identifier, such as `00d000000000000xxx`, is provided at the top of the setup page):

```
NAME               TTL   CLASS  TYPE    VALUE  
--------------------------------------------------  
[Sub Domain].example.com   3600  IN     CNAME   [Sub Domain].example.com.00d000000000000xxx.live.siteforce.com
```

```
NAME                               TTL   CLASS  TYPE    VALUE  
--------------------------------------------------  
_acme-challenge.[Sub Domain].example.com   3600  IN     CNAME   _acme-challenge.[Sub Domain].example.com.00d000000000000xxx.live.siteforce.com
```

> *Make sure these DNS records are registered* ***beforehand****. If not, you will encounter an error when saving in the following step.*

5. Once all settings are complete, click **Save**.

6. Salesforce’s CDN partner **Cloudflare** will then begin provisioning (preparing and making the domain available). You cannot proceed to the next step until provisioning is complete. This can take up to 24 hours (in my environment, it took about 4 hours). You will receive an email notification once provisioning is finished.

7. After confirming provisioning is complete, the status will show as **“Awating Activation”**. Click **Activate**.

> *Once activated, the new custom domain will automatically switch from* ***HTTP to HTTPS****.*

8. When the domain has been activated, domain setup is complete. Next, select **New Custom URL**.

9. Choose the registered domain and **Marketing Landing Pages**, then add `/lp` to the path and save the settings.

10. Two entries will then be automatically registered.

11. Finally, check the landing page URLs you have already created. You should now see that the landing page links are available under the domain you registered, e.g., `pages.mail.nac-care.com/lp`. At this point, you are ready to start using the custom domain.

## Closing Notes

Please note that this domain configuration is **not mandatory** but entirely optional. Your setup will still work with the default domain provided at the time of purchase. However, to ensure that customers can use your site with confidence, I recommend configuring at least “My Domain.” Please consider this option.

### One additional note:

If the **eTLD+1** (naked domain, e.g., the `nac-care.com` portion) of your external website matches that of your landing page, tracking is now handled with the same first-party cookie.

As a result, the same **Individual ID** (an anonymous identifier) is assigned in Website Engagement. While this specification does not yet appear in the help documentation, it seems to be functioning as expected.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)

### Series on Domain Configuration in Marketing Cloud Next

1️⃣ [Steps for Email Domain Authentication](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d)  
2️⃣ [Adding From Addresses & Reply Mail Management](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258)  
3️⃣ [Setting Domains for Landing Pages](/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663)  
4️⃣ [Setting Domains for Email Tracking Links](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d)
