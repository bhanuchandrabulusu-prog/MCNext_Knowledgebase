# SFMC Tips #140 : Marketing Cloud Next: Steps for Email Domain Authentication

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d

---

# SFMC Tips #140 : Marketing Cloud Next: Steps for Email Domain Authentication

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--424e9cbbf76d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--424e9cbbf76d---------------------------------------)

8 min read

·

Jun 15, 2025

--

Photo by [Federica Maniezzo](https://unsplash.com/@federicamaniezzo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

For instructions on **Email Domain Authentication**, which is part of the basic setup in **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), I recommend checking out the excellent LinkedIn post below.

[## Email Authentication for Marketing Cloud Growth

### After recently helping a customer authenticate a subdomain for Marketing Cloud Growth, I wanted to document the entire…

www.linkedin.com](https://www.linkedin.com/pulse/email-authentication-marketing-cloud-growth-sabuhi-yahya-kaote/?trackingId=E5PPgyT%2BRBqgF3wqPzWI8w%3D%3D&source=post_page-----424e9cbbf76d---------------------------------------)

This post was written by **Sabuhi Yahya-san**. He is also the creator of the well-known learning programs **AMPscript30** (currently on hiatus), **SQL30**, **MCAE30**, and **NEXT30**.

![]()

[Sabuhi Yahya](https://www.linkedin.com/in/sabuhiy/overlay/about-this-profile/)

These are free learning platforms designed to help you master **AMPscript**, **Marketing Cloud SQL**, **Marketing Cloud Account Engagement**, and **Marketing Cloud Next** in just 30 days.

I have personally used some of these programs in the past and was genuinely impressed by both the quality of the content and the effectiveness of the learning experience.

I’ve included the links below, so I highly recommend taking advantage of these excellent resources.

### AMPscript30

[## AMPscript30 Archives - MarketingCloud30

### MarketingCloud30 - Learn new skills with daily hands-on Marketing Cloud 30-day challenges.

marketingcloud30.com](https://marketingcloud30.com/challenge/ampscript30/?source=post_page-----424e9cbbf76d---------------------------------------)

### SQL30

[## 30-day SQL Challenge | MarketingCloud30

### Join the 30-day SQL challenge and take your data analysis and marketing skills to the next level with daily practical…

marketingcloud30.com](https://marketingcloud30.com/challenge/sql30/?source=post_page-----424e9cbbf76d---------------------------------------)

### MCAE30 (Marketing Cloud Account Engagement)

[## Marketing Cloud Account Engagement 30-day Challenge | MC30

### MCAE30 offers a 30-day challenge program that aims to teach participants how to effectively use Marketing Cloud Account…

marketingcloud30.com](https://marketingcloud30.com/challenge/mcae30/?source=post_page-----424e9cbbf76d---------------------------------------)

### **NEXT30 (Marketing Cloud Next)**

[## Next30 | MarketingCloud30

### Learn new skills with daily hands-on Marketing Cloud 30-day challenges.

marketingcloud30.com](https://marketingcloud30.com/challenge/next30/?source=post_page-----424e9cbbf76d---------------------------------------)

Now, I also went through the email domain authentication setup process on my side. Please review the following points.

**Considerations**

- Marketing Cloud Next supports only the self-hosted DNS configuration method. **It does not support the “**[**Delegated Subdomain**](https://help.salesforce.com/s/articleView?id=mktg.mc_es_subdomain_delegation_guide.htm&type=5)**” approach** used in Marketing Cloud Engagement.
- In addition, regarding whether the same subdomain currently used in Marketing Cloud Engagement can also be shared with Marketing Cloud Next, **Salesforce recommends configuring separate subdomains for each, regardless of whether you use the delegated method or the self-hosted method**. Salesforce also provides guidance on this point in the following help documentation.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=001533984&type=1&source=post_page-----424e9cbbf76d---------------------------------------)

- Salesforce Starter, Salesforce Pro Suite, and the Marketing App included with Salesforce Foundations send emails through the **salesforce.com** domain, and **email authentication can be used without any DNS configuration**. If you want to send emails using your own custom domain, you will need to upgrade to **Growth Edition** or higher.

## Steps for Email Domain Authentication

**1.** From **Settings**, go to **Channel > Email**, and click **Go to Authenticated Domains**.

**2.** In the “All Authenticated Domains” section, click + **Add Domain**.

**3.** The next steps will be displayed. Simply click **Continue**.

- 1. First, enter the details of your domain.
- 2. Next, ask your **domain registrar** to update the DNS records.
- 3. Once that is complete, configure **Reply Mail Management** to enable automatic routing and handling of inbound replies.

A domain registrar is the company that manages domain names. Examples include **GoDaddy, Namecheap, Cloudflare Registrar and Onamae.com**.

**4.** Enter the “**subdomain**” you want to use for sending emails, then click **Submit**.

**5.** On the next screen, set up the **From Address** under “Create an email address for this domain”. The username is the part before the “@”. This will become the default From Address. Once ready, click **Create New**.

**6.** Next, configure the DNS records — work with your IT team for this step.

Updating DNS records will vary depending on your **DNS provider** (the service that provides DNS servers linking domain names to IP addresses).

1. Log in to your DNS provider and access the DNS management screen. Look for a section labeled “DNS Management”, “DNS Settings”, or “Domain Management”.
2. Add the DNS records using the provided values.
3. Save and apply the changes. Verify that they are reflected on your provider’s side. Propagation may take more than 24 hours.

*For requests to the domain registrar,* [*I recommend using the following template shared in Sabuhi Yahya’s recent post*](https://www.linkedin.com/pulse/email-authentication-marketing-cloud-growth-sabuhi-yahya-kaote/)*. I also used it for my implementation, and it was extremely helpful!*

Thank you so much, Sabuhi-san!!

```
Subject: Request to Add DNS Records for Salesforce Marketing Cloud  
  
Body: Hello [name],  
  
I'm working with the marketing team to implement Marketing Cloud Growth (MCG), our new marketing automation platform. We will be using MCG to send communication to our customers and prospects from @[sub domain].yourdomain.com. To guarantee great email deliverability, we need to make the following changes:  
  
We need to add new CNAME records so MCG is authorized to send emails on our behalf.  
  
Please add the following to DNS entries:  
  
Type: CNAME  
Name: [insert name here].[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: [insert name here].[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: [insert name here].[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: anonymous.[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: bounce.[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: fbl.[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: reply.[sub domain]  
Value: [insert value here]  
  
Type: CNAME  
Name: leave.[sub domain]  
Value: [insert value here]  
  
Optional  
Please add the following DMARC record if we don't have one already.  
  
Type: TXT  
Name: _dmarc  
Value: v=DMARC1;p=reject;adkim=r;aspf=r;pct=100;  
  
  
Please let me know when these steps are completed so that we can complete the setup process within Marketing Cloud Growth. Feel free to reach out with any questions.  
  
Best,  
Marketing Operations
```

***Note:*** *Applying a DMARC policy such as* `p=reject` *to your organization’s root domain can affect all email sending that uses that domain. If the policy is misconfigured, even legitimate emails may be rejected by receiving mail servers.*

*Before applying a DMARC policy to your root domain, carefully review its impact on your email sending environment and coordinate with your IT department or network administrators.*

Fill-in details will be displayed by clicking the corresponding button.

***Important:*** *The Name obtained from the* ***DNS Record Information*** *includes the fully qualified domain name (FQDN).  
For example, for a bounce record, it may be displayed as* `bounce.mail.nac-care`*, which includes the parent domain (*`nac-care`*).*

*However, in many DNS management consoles, the parent domain is already preselected and automatically appended. As a result, if you enter the displayed FQDN directly into the Name field, the domain may be duplicated and cause an error (for example,* `bounce.mail.nac-care.nac-care`*).*

*In such cases, manually remove the parent domain portion (*`nac-care`*) before registering the record.  
In other words, instead of entering* `bounce.mail.nac-care`*, remove the* `.nac-care` *part and register* `bounce.mail` *as the Name.*

**7.** Once the above setup is complete, check the box and click **Activate My Domain**.

**8.** A popup will appear saying “DNS changes may take up to 48 hours to propagate”. Enter an email address to be notified once the process is complete, and click **Finish**.

**9.** The update will begin.

**10.** Wait up to 48 hours. In my case, I received the confirmation email after about 1 hour.

**11.** Finally, log back into the admin screen and check that the status shows **Active**. You’re done!

**Note:** Once an authenticated domain has been created, it cannot be deleted.

After domain authentication is complete, you’ll be able to add **From Addresses** and configure **Reply Mail Management (RMM)** from the red tab at the top. Please check the related article for details.

[## SFMC Tips #163 : Marketing Cloud Next: Adding From Addresses & Reply Mail Management

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) does not provide an SAP (Sender Authentication…

medium.com](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258?source=post_page-----424e9cbbf76d---------------------------------------)

How was it?

The records registered in DNS are not just simple settings — they are directly linked to the following:

- **Email deliverability**
- **Spam classification**
- **Reply processing (Reply Mail Management)**

Therefore, it is assumed that all settings are configured correctly.  
 I will summarize the content below for your reference.

## Outbound (Sending-related: 3 records)

### **s1 / s2 / s3 (DKIM records)**

- s1-e360-xxx.\_domainkey.sub-domain
- s2-e360-xxx.\_domainkey.sub-domain
- s3-e360-xxx.\_domainkey.sub-domain

These are all records for **DKIM (email authentication)**.

### **Role**

- Proves that the email has not been tampered with
- Increases the trustworthiness of the sending domain (affects deliverability)

### **Why are there three?**

- For key rotation (switching encryption keys)
- Multiple keys are prepared so that Salesforce can switch them safely

### **Summary**

- Outbound = Email sending reliability (DKIM)

## Inbound (Receiving-related: 5 records)

These are all settings for **Reply Mail Management (RMM)**.

**① anonymous.sub-domain (for anonymous replies)**

- Handles replies where the sender cannot be identified
- Acts as a fallback for rare cases

**② bounce.sub-domain (for bounce processing)**

- Detects delivery failures (Hard / Soft Bounce)
- Automatically used for unsubscribe processing or status updates

**③ fbl.sub-domain (for feedback loop / complaints)**

- Receives reports when users mark emails as spam
- Processes complaint notifications from ISPs (such as Gmail and Yahoo)

**④ reply.sub-domain (for standard replies)**

- Receives replies sent by users
- Used for inquiry handling and automated response processing
- Also used by the Conversational Email feature

**⑤ leave.sub-domain (for unsubscribe-related processing)**

- Detects replies requesting to unsubscribe
- Automatically linked to opt-out processing

That’s it for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)

### Series on Domain Configuration in Marketing Cloud Next

1️⃣ [Steps for Email Domain Authentication](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d)  
2️⃣ [Adding From Addresses & Reply Mail Management](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258)  
3️⃣ [Setting Domains for Landing Pages](/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663)  
4️⃣ [Setting Domains for Email Tracking Links](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d)
