# SFMC Tips #168 : Marketing Cloud Next: Disabling Consent Management

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-disabling-consent-management-41d58a4acbef

---

# SFMC Tips #168 : Marketing Cloud Next: Disabling Consent Management

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--41d58a4acbef---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--41d58a4acbef---------------------------------------)

5 min read

·

Sep 3, 2025

--

Photo by [Jakob Rosen](https://unsplash.com/@jakobnoahrosen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Next Growth & Advanced Edition comes with a built-in Consent Management mechanism as standard.  
For promotional emails, it is possible to send emails or SMS messages only to contacts who have opted in in advance.

> *For the basic concept and overall overview of Consent Management, please refer to the following article.*

[## SFMC Tips #90 : Marketing Cloud Next: A Guide to Consent Management

### The Importance of Consent Management

medium.com](/@marketingcloudtips/marketing-cloud-on-core-a-guide-to-consent-management-5ca95a1602a0?source=post_page-----41d58a4acbef---------------------------------------)

## Disabling Consent Management

Consent Management can be disabled from the Setup screen.  
 However, there are important points to note.

Disabling it does **not** mean that Consent Management is completely stopped for all emails across the entire account.

After disabling, please be aware of the following behaviors.

### Notes

- Even if you disable Consent Management, consent settings applied to emails in flows that are already active are **not automatically removed**.
- Even after disabling, if you configure a **Communication Subscription** when sending an email, the consent status will still be checked at send time.

### In the Case of Transactional Sends

Unless you include the **Preference Manager** link merge field in the email body:

```
{!$link.PreferenceCenterUrl}
```

Consent Management will **not** be applied.  
In other words, if this link is not included, the email will always be sent.

> *\* This behavior is by product design and is not a bug.*

You need to configure your settings with these behaviors in mind.

## Setup Configuration Steps

### 1. Navigate to the Consent Management Settings Screen

Go to **Setup** ＞ **Guided Setup** ＞ **Channels** ＞ **Email**, and move to the **Manage Consent Validation** section.

### 2. Check the Default State

By default, the settings are as follows:

- Commercial Email: Enabled
- Transactional Email: Disabled

### 3. Disable Consent Management

When you click the toggle, a popup is displayed.  
Click the **Disable** button, and selecting a **Communication Subscription** will no longer be mandatory when configuring email sends.

\* Even after disabling, this setting can be re-enabled later.

## Flow Configuration

Configuration in the flow is simple.  
Set **Communication Subscription** to **Not Set** (do not select anything).

### Important Notes

If any Communication Subscription is configured,  
even if Consent Management is disabled in Setup,  
the email will always be sent **only after checking the consent status**.

## Summary of the Key Point

## The Correct Meaning of “Disable”

This “Disable” setting is best understood as:

> *A mechanism that allows you to save email elements without selecting a Communication Subscription (leaving it unset) without causing an error.*

- Communication Subscription: **Not Set**  
   → Consent Management is not referenced
- Communication Subscription: **Set**  
   → Consent Management for that subscription is enabled, and consent status is checked

## How to Think About Disabling Consent Management

There are different ways to think about disabling Consent Management, but I basically believe it should **not** be disabled.

If we translate this concept to Marketing Cloud Engagement, it is close to  
 **“abandoning All Subscribers status management”.**

### Relationship with the List-Unsubscribe Header

For example, consider one-click unsubscribe via the List-Unsubscribe header.

To correctly receive this unsubscribe intent, a Communication Subscription is required.

If no Communication Subscription is set,  
 even if the user clicks the unsubscribe button, that intent will be ignored.

### Recommended Operational Example

If you want to use your own internally managed subscription flags, the following operation is realistic:

- Keep Consent Management enabled
- [Use a record-triggered flow to temporarily set all contacts to an opted-in state](/p/5ca95a1602a0)  
   (equivalent to “All Subscribers” in Marketing Cloud Engagement)
- Separately control sending by excluding contacts whose subscription flag is opt-out using segments or data space filters

**With this approach:**

- One-click unsubscribe via the List-Unsubscribe header can be correctly received
- Consent Management can be utilized as a **mechanism for receiving List-Unsubscribe one-click unsubscribe requests**

### Additional Note

One-click unsubscribe via the **List-Unsubscribe header** operates on essentially the same underlying mechanism as the standard unsubscribe link.

The specific behavior rules are as follows:

- **When a Communication Subscription is specified**  
   → Only the specified communication subscription is opted out.
- **When no Communication Subscription is specified**  
   → The process is ignored, and effectively nothing happens.

What’s important to note here is the difference in **display conditions**.

A standard unsubscribe link cannot be placed in transactional emails, so this usually does not cause any issues.

On the other hand, the **one-click unsubscribe button provided via the List-Unsubscribe header** may be displayed at the mail client’s discretion, regardless of whether the email is promotional or transactional.

In such cases, transactional emails are typically sent **without** any communication subscription configured. As a result, even if the recipient clicks the one-click unsubscribe button, the action is ultimately ignored.

Most importantly, the customer themselves has no way of realizing that their action was “ignored.”

Understanding this behavior can be helpful when troubleshooting inquiries such as: “I unsubscribed, but I’m still receiving emails.”

## Conclusion

- “Disabling Consent Management” does **not** mean a complete shutdown
- The essence of disabling is **“allowing saves with an unset Communication Subscription”**
- For long-term and healthy operations, keeping Consent Management enabled is recommended

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
