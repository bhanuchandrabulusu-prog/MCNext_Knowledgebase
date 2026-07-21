# SFMC Tips #163 : Marketing Cloud Next: Adding From Addresses & Reply Mail Management (RMM)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258

---

# SFMC Tips #163 : Marketing Cloud Next: Adding From Addresses & Reply Mail Management (RMM)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8cc7bd2ce258---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8cc7bd2ce258---------------------------------------)

5 min read

·

Aug 22, 2025

--

Photo by [Jamakassi](https://unsplash.com/@jamakassi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition) does not provide an SAP (Sender Authentication Package) like Marketing Cloud Engagement.

However, while it is not exactly the same as SAP, you can achieve a similar setup by combining **standard features of Salesforce CRM** with **capabilities unique to Marketing Cloud Next**.

For details on the “Domain Authentication” process, please refer to the following article.

[## SFMC Tips #140 : Marketing Cloud Next: Email Domain Authentication Steps

### For instructions on Email Domain Authentication, which is part of the basic setup in Marketing Cloud Next (Marketing…

medium.com](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d?source=post_page-----8cc7bd2ce258---------------------------------------)

Once “Domain Authentication” is completed, you will be able to:

- **Adding From Addresses**
- **Reply Mail Management (RMM)**

In this article, I’ll take a closer look at these two features.

## Adding From Addresses

Unfortunately, at this time it is not possible to create **dynamic from addresses**. Since this functionality is considered essential in B2B marketing, it is highly likely that Salesforce will release it in the future, but the development status is currently unknown.

When adding a from address, you must always work with a **verified domain** as the prerequisite. Unlike Marketing Cloud Engagement, you cannot register just any email domain.

### Setup Steps

1. Open **Details** for the verified domain that has been added.

2. Select the **From Addresses** tab.

3. Click **Add From Address**.

4. Enter the **Display Name** and **Username** (the part before the @ symbol). You can register multiple entries at once. Save your changes.

5. The from address has now been registered. It can also be deleted later if needed.

6. Confirm that the new from address is available when setting up your send configuration.

## Reply Mail Management (RMM)

Next, let’s look at **Reply Mail Management (RMM)**.

Normally, when you use a verified domain and configure a subdomain for your from address (e.g., **info@mail.nac-care.com**), there isn’t actually a recipient behind that address. So, if a customer replies to it, no one will ever see the response.

Of course, one option is to simply state, *“This email address is for sending only and cannot receive replies”,* and ignore responses. However, with RMM, you can do more — such as sending automatic responses or routing incoming replies to a specific email address.

> *That said, RMM currently does* ***not*** *support setting routing addresses dynamically. In contrast, Marketing Cloud Engagement allows more flexible handling, as explained in [*[*this article*](/p/11f541c0d57f)*].*

### Setup Steps

1. Open **Details** for the verified domain that has been added.

2. Select the **Reply Mail Management** tab.

3. Configure the following three settings:

### **a. Delete Auto-Replies and Out-of-Office**

- Yes / No
- Decide whether to automatically delete auto-replies or out-of-office notifications received when you send an email.
- If set to Yes, these types of replies will not be processed.

### **b. Auto-Response**

- None / Create Auto-Response Message
- Set up an automatic reply to send back to customers when they respond.
- Example: Thank you for contacting us. We will review your inquiry and a representative will reach out within two business days.

### **c. Enable Email Forwarding**

- Yes / No
- Decide whether to forward incoming replies to another email address.
- If set to Yes, you can specify the forwarding address under **Routing Address**.

4. Once the settings are complete, save your changes.

![]()

> ***Tip:*** *In Spring ’26, the design of the admin interface has changed to the layout shown below, but the available settings and configurable options remain the same.*

### **Automatic Opt-Out by Keywords**

When RMM is enabled, if the reply body contains any of the following strings within the first 200 characters, the email address that sent the reply will be automatically unsubscribed (opted out):

- unsub
- unsubscribe
- opt-out
- remove
- stop

**Important Notes**

- Only the communication registration used at the time of sending will be opted out. Not all communication registrations will be opted out.
- If these strings are present, no auto-reply or forwarding of the reply content will occur.
- These strings must be entirely lowercase. Some email clients automatically capitalize the first letter, and in such cases, the automatic opt-out will not be applied.

## Conclusion

In practice, auto-replies and forwarding via Reply Mail Management are usually processed **within about 30 seconds**. If you change the forwarding address in the settings, the update takes effect immediately.

These settings are not mandatory, but some organizations may find them necessary. Although more advanced features such as dynamic routing are not yet fully available, they are expected to be added over time. Be sure to keep up with the latest updates so you can make the most of these features.

> ***Note:*** *In the organizations I manage, I experienced an issue in two accounts consecutively where automatic replies and forwarding of reply contents did not occur. In both cases, I created support cases, and the issue was resolved through fixes on the internal system side. If you encounter problems such as emails not being received, please consider creating a support case as soon as possible.*

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)

### Series on Domain Configuration in Marketing Cloud Next

1️⃣ [Steps for Email Domain Authentication](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d)  
2️⃣ [Adding From Addresses & Reply Mail Management](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258)  
3️⃣ [Setting Domains for Landing Pages](/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663)  
4️⃣ [Setting Domains for Email Tracking Links](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d)
