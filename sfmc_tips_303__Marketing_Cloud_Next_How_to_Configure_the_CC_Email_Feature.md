# SFMC Tips #303 : Marketing Cloud Next: How to Configure the CC Email Feature

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-configure-the-cc-email-feature-7f9fb279aa97

---

# SFMC Tips #303 : Marketing Cloud Next: How to Configure the CC Email Feature

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7f9fb279aa97---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7f9fb279aa97---------------------------------------)

6 min read

·

Jun 8, 2026

--

Photo by [Hưng Nguyễn](https://unsplash.com/@hungngng?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions introduced the **CC (Carbon Copy) feature for email sending**.

Until now, emails in Marketing Cloud Next were basically intended to be sent directly to customers themselves. However, in actual business operations, there are many cases such as:

- **Wanting to share the sent content with sales representatives**
- **Wanting to send the same email to a customer’s manager or assistant**
- **Wanting to deliver contract or procedure-related notifications to all related parties**

With this release, these requirements can now be addressed, allowing related parties to be included as CC recipients when sending emails to customers.

On the other hand, when using this feature, there are several points that should be understood, including:

- **The concept of Consent**
- **Salesforce message credit consumption**
- **Domain verification for internal recipients**

In this article, let’s take a detailed look at the overview of the CC email feature, how to configure it, and the points to consider when using it.

## Types of CC Recipients

In Marketing Cloud Next, CC recipients are classified into the following two types.

### 1. External Recipients

These are individuals related to the customer.

For example:

- Manager
- Assistant
- Family member
- Representative

### 2. Internal Recipients

These are employees of your company.

For example:

- Sales representatives
- Customer Success representatives
- Support representatives

*When using internal recipients, configuration of an “Authorized Email Domain”, described later, is required.*

## Considerations When Using CC

Please note the following when using the CC feature.

- Even CC recipients consume Salesforce Message Credits. For example, if you send an email to 10,000 recipients and add four CC recipients to each email, a total of 50,000 email credits will be consumed.
- When including internal employees as CC recipients, their email addresses must belong to an Approved Email Domain. If no approved domains are configured, all recipients are treated as external recipients.
- CC recipients also require consent when sending promotional emails.
- BCC (Blind Carbon Copy) is not currently supported. As a result, both the primary recipient and all CC recipients can see who has been included in the CC list, so this feature should be used with caution.
- If the primary recipient is not eligible to receive the email — for example, if the email address has hard bounced or the required consent has not been obtained — the email will not be sent to any CC recipients.
- However, if processing has already begun and delivery to the primary recipient later fails due to a delivery-time error or similar issue, the email will still be sent to the CC recipients.
- You can add up to 10 CC email addresses per email send.

## Configure an Authorized Email Domain

Now let’s configure settings for internal recipients.

To have internal employees recognized as Internal Recipients, you must first register your company’s email domain with Salesforce and verify ownership.

In Setup, select **Unified Messaging** > **Authorized Email Domains**, and then click **Add Email Domain**.

Enter the target email domain and add it.

A verification key is generated. Make a note of this value.

Example: `00D000000000P08=1TB00000000000B`

## Add a TXT Record to DNS

From this point, you will need to work with your DNS administrator or IT department.

Salesforce uses a TXT record to verify ownership of the target domain.

There are three configuration patterns.

*Recommended: If the domain is used by a single Salesforce org, format “1” or “2” is generally sufficient. If the same domain is shared across multiple orgs, format “3” is recommended.*

### ① Use the Domain Name Directly

This is the simplest method.

The following example uses the domain name `example.com`, verification key `1TB00000000000B`, and org ID `00D000000000P08`.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
example.com          600   IN      TXT     00D000000000P08=1TB00000000000B
```

### ② Add the \_sfdv Prefix

You can also create the TXT record by adding `_sfdv` to the beginning of the domain name.

The following example uses the same domain and verification key.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
_sfdv.example.com    600   IN      TXT     00D000000000P08=1TB00000000000B
```

### ③ Add the orgId.\_sfdv Prefix

This format combines the org ID (18 digits) and `_sfdv`.

It is recommended when the same sending domain is used by multiple Salesforce orgs or when a unique record name is required in DNS.

The following example uses org ID `00D000000000P08EAE`.

```
Name                                   TTL  CLASS  TYPE    VALUE  
--------------------------------------------------------------------  
00D000000000P08EAE._sfdv.example.com   600   IN    TXT     00D000000000P08=1TB00000000000B
```

***Important:*** *The Name values above contain the Fully Qualified Domain Name (FQDN). For example,* `_sfdv.example.com` *already includes the parent domain (*`example.com`*).*

*However, in many DNS management interfaces, the parent domain is already selected and automatically appended. If you enter the displayed FQDN exactly as shown, the domain may be duplicated, resulting in an error (*`_sfdv.example.com.example.com`*).*

*In such cases, manually remove the* `.example.com` *portion and register only* `_sfdv`*.*

↓ ↓ ↓

### If Existing TXT Records Already Exist

If TXT records already exist for these host names, you can either add a new TXT record or append the verification code to the existing TXT record value.

When storing multiple verification codes in a single TXT record, separate each value with a semicolon (`;`).

The following example stores verification codes for two orgs in a single TXT record.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
example.com          600   IN      TXT     00D000000000X09=1TB00000000000C;00D000000000P08=1TB00000000000B
```

*Using this method, even when the same domain is used across multiple Salesforce orgs, multiple verification values can be managed within a single TXT record.*

## Complete Domain Verification

After confirming that the DNS record has been published using a tool such as nslookup, return to the administration screen, check the checkbox, and click the **Verify** button.

If **Active** is displayed, domain verification is complete.

Marketing Cloud Next can now recognize email addresses using this domain as internal recipients.

## Enable CC Email

In Setup, select **Unified Messaging**, and then **Send Settings**.

Enable CC for external recipients.

- Enable Carbon Copy.
- You can configure the maximum number of CC recipients between 1 and 10.
- The default value is 5.

Configure CC for internal recipients.

- Enable Internal Recipients.
- Choose whether consent should be checked for internal employee email addresses when sending promotional emails.

## Try Using CC

A CC configuration section now appears approximately in the middle of the email send configuration screen, where you can insert email addresses for CC.

*\*The inserted field can be either an “Email” field type or a “Text” field type.*

The sent email is displayed as a normal CC in standard email clients.

![]()

## Summary

With the Summer ’26 release, Marketing Cloud Next now supports CC when sending emails.

This makes it possible to support scenarios such as:

- Sharing with sales representatives
- Sharing with customer-related parties
- Sharing information related to contracts and procedures

These scenarios, which previously required custom handling, can now be achieved using standard functionality.

On the other hand, it is important to understand the following points in advance:

✅ Consent is required for CC recipients as well  
✅ BCC is not supported  
✅ Message credits are consumed for each CC recipient  
✅ Authorized Email Domains must be configured for internal recipients

In particular, message credit consumption can easily be overlooked. For organizations performing large-scale email sends, it is recommended to establish operational rules before using this feature.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
