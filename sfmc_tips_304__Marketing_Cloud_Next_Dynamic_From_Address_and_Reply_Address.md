# SFMC Tips #304 : Marketing Cloud Next: Dynamic From Address and Reply Address

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-dynamic-from-address-and-reply-address-ca084748f1e2

---

# SFMC Tips #304 : Marketing Cloud Next: Dynamic From Address and Reply Address

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ca084748f1e2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ca084748f1e2---------------------------------------)

6 min read

·

Jun 8, 2026

--

Photo by [Drew Colins](https://unsplash.com/@drewcolins?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Editions, it is mandatory to use email addresses from DKIM-authenticated domains as the sender address in order to increase customer engagement and enable more trustworthy communication.

With the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6), it is now possible to dynamically configure the From Address and Reply Address using information stored on Contacts and Leads.

This makes it possible to send emails that appear to come directly from a sales representative rather than from a shared address such as info@ or no-reply@. In addition, when a customer replies to the email, the reply can be delivered directly to the assigned sales representative.

In this article, I will explain the setup procedure for this dynamic sender feature and important points to consider when using it.

## Configure an Authorized Email Domain

The domain used for the From Address has likely already been registered. However, the domain used for the Reply Address has not previously been registered through the Salesforce user interface. Therefore, it must be registered as an Authorized Email Domain.

1. In Setup, select Unified Messaging > **Authorized Email Domains**, and click Add Email Domain.

2. Enter the target email domain and add it.

3. A code is generated. Make a note of it.

Example: `00D000000000P08=1TB00000000000B`

4. Create a DNS record using the verification code.

For the DNS TXT record used to verify ownership of the email sending domain, you can use any of the following three formats for the Name (host name). In other words, any of these three formats are acceptable.

***Recommendation:*** *If the domain is used by only one Salesforce org, format “①” or “②” is generally sufficient. If the same domain is shared across multiple orgs, it is recommended to use format “③”.*

### ① Use the domain name directly

This is the simplest approach.

The following example assumes the domain name is `example.com`, the verification code is `1TB00000000000B`, and the org ID is `00D000000000P08`.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
example.com          600   IN      TXT     00D000000000P08=1TB00000000000B
```

### ② Add the \_sfdv prefix

You can also create the TXT record by adding `_sfdv` to the beginning of the domain name.

The following example uses the same domain and verification code.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
_sfdv.example.com    600   IN      TXT     00D000000000P08=1TB00000000000B
```

### ③ Add the orgId.\_sfdv prefix

This format combines the org ID (18 characters) and `_sfdv`.

It is recommended when the same email sending domain is used across multiple Salesforce orgs or when a unique DNS record name is required.

The following example assumes the org ID is `00D000000000P08EAE`.

```
Name                                   TTL  CLASS  TYPE    VALUE  
--------------------------------------------------------------------  
00D000000000P08EAE._sfdv.example.com   600   IN    TXT     00D000000000P08=1TB00000000000B
```

***Important:*** *The Name values shown above include the Fully Qualified Domain Name (FQDN). For example,* `_sfdv.example.com` *already includes the parent domain (*`example.com`*).*

*However, in many DNS management consoles, the parent domain is already selected and automatically appended. Therefore, if you enter the displayed FQDN exactly as shown, the domain may be duplicated and result in an error (for example,* `_sfdv.example.com.example.com`*). In such cases, manually remove the* `.example.com` *portion and register only* `_sfdv`*.*

### Important Notes When an Existing TXT Record Already Exists

- If a TXT record already exists for any of these host names, you can either add a new TXT record or append the verification code to the value of the existing record.
- When storing multiple verification codes in a single TXT record, separate each value with a semicolon (;).

The following example stores verification codes for two orgs in a single TXT record.

```
Name                 TTL   CLASS   TYPE    VALUE  
--------------------------------------------------------------------  
example.com          600   IN      TXT     00D000000000X09=1TB00000000000C;00D000000000P08=1TB00000000000B
```

*Using this approach, multiple verification records can be managed within a single TXT record even when the same domain is used across multiple Salesforce orgs.*

5. After confirming that the DNS record has been published using nslookup or a similar tool, return to the Salesforce administration screen, select the checkbox, and click Verify.

6. If Active is displayed, domain verification is complete.

Once domain verification is complete, marketers can use merge fields to dynamically configure the Reply Address when creating campaigns.

## Send from a Sales Representative to a Lead

1. Prepare the sales representative’s name and email address on the Lead record.

*\*In my environment, I use* ***@mail4.nac-care.com*** *as the DKIM-authenticated domain. Therefore, I have configured* ***n.watanabe@mail4.nac-care.com*** *as my From Address.*

2. Create a new Audience Flow.

3. Next, select CRM Record Query Flow, specify Lead as the object, and choose Run Immediately as the schedule.

4. Proceed to the Email Activity configuration screen, where you can configure the sending options.

### Sender Options

- **① Authenticated From Address**  
  Use a sender address from a DKIM-authenticated domain (same as before).
- **② Dynamic From Address**  
  Dynamically configure only the sender name.  
  Dynamically configure both the sender name and email address.

![]()

*\*The personalization fields available here are limited to the following: for Segment Flows, only fields from the Unified Individual configured in the Data Graph can be used. For Record Query Flows, only fields from the data source can be used. Related attributes cannot be used.*

### Reply Options

- **① Use RMM Addresses**  
  Use the Salesforce-managed reply address as before.
- **② Dynamic Reply Address**  
  Dynamically configure the reply address using Lead or Contact data.  
  ***Note:*** *Selecting this option will disable RMM.*

5. After configuration, send the email.

The email will be sent using the dynamic sender name and email address based on the data stored on the Lead record.

6. For the Reply-To address, if a sales representative’s email address is available, you can configure it so that any replies from recipients are sent directly to that sales representative.

7. On the other hand, if a sales representative’s email address cannot be retrieved, a fallback configuration can be used to route replies to a shared email address, such as a general inbox or customer inquiry mailbox.

### Considerations

- Each fallback setting is applied only when an email address cannot be retrieved for the target audience.
- For the sender, you configure a combination of the **From Name** and **From Address**. In contrast, the only setting available for replies is the **Reply-To Address**. There is no setting equivalent to a **Reply-To Name**, and only an email address can be specified as the reply destination.
- In addition, the domain used for the Reply-To Address must be one of the preconfigured **Authorized Email Domains**.

## Conclusion

Instead of sending emails from a shared email address as before, it is now possible to send emails using each sales representative’s name and email address, enabling more personalized communication. Customers can also more easily identify who sent the email, which may improve reply rates and engagement.

As for the dynamic Reply Address, there are still some unclear behaviors at this time. I plan to introduce it again once my testing is complete.

Please try it in your own environment and take advantage of this feature.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
