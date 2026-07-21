# SFMC Tips #183 : Marketing Cloud Next: Smarter Identity Resolution Match Rules

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-smarter-identity-resolution-match-rules-ea432cbb5cc5

---

# SFMC Tips #183 : **Marketing Cloud Next: Smarter Identity Resolution Match Rules**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ea432cbb5cc5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ea432cbb5cc5---------------------------------------)

2 min read

·

Oct 6, 2025

--

Photo by [Sierra Alpha Juliet](https://unsplash.com/@mrhz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of Marketing Cloud Next Growth & Advanced Edition, the contents of the “**default identity resolution rule set**” for unified individuals have been updated, improving the accuracy of tracking web visitors and preventing duplicate records.

When the default identity resolution rule set is generated at initial setup, two new match rules are automatically included:

- **Lead to Contact (lead-to-contact)**: Prevents duplication when a lead is converted to a contact.
- **Device to Known (device-to-known)**: Matches web visitors to known profiles.

Previously, the default identity resolution rule set only used **email address** matching.

### **Considerations**

- The newly added Identity Match-type rules, such as Device to Known and Lead to Contact, cannot be combined with other conditions. As a result, the “⚠️ Warning” message displayed in the interface cannot be removed.
- If you are already using an existing rule set, it is recommended to manually add these new match rules. The steps for adding them are explained below.

[## SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

### In Marketing Cloud Next Growth & Advanced Edition, the Summer ’25 release introduced the ability to add Identity Match…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e?source=post_page-----ea432cbb5cc5---------------------------------------)

**Tips**: If you are working with Prospects, we also recommend adding the following match types manually at this stage:

- **Prospect to Lead (prospect-to-lead)**
- **Prospect to Contact (prospect-to-contact)**

## Conclusion

By adding these recommended match rules, identity resolution can continue even when email addresses differ. Please note that in Marketing Cloud Next, if multiple email addresses are associated with a single unified individual ID, emails will be sent to all of those addresses. More details on this behavior are provided below.

[## SFMC Tips #166 : Marketing Cloud Next: Understanding Which Email Addresses Are Used for Sending

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), it’s crucial to correctly identify which email…

medium.com](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9?source=post_page-----ea432cbb5cc5---------------------------------------)

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
