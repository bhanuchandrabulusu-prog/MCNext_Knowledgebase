# SFMC Tips #170 : Marketing Cloud Next: Hard Bounce and Soft Bounce

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-hard-bounce-vs-soft-bounce-8106419bb008

---

# SFMC Tips #170 : Marketing Cloud Next: Hard Bounce and Soft Bounce

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8106419bb008---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8106419bb008---------------------------------------)

3 min read

·

Sep 6, 2025

--

Photo by [Maria Malone](https://unsplash.com/@angitamalone90?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When working with **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, it’s important to understand how **bounces** occur during email sends. In this article, we’ll explain the difference between **hard bounces** and **soft bounces**, and how each is handled.

This behavior applies specifically to the following products:

- **Marketing Cloud Growth & Advanced Editions**
- **Salesforce Foundations**
- **Salesforce Pro Suite**
- **Salesforce Starter**

## What is a Hard Bounce?

A **hard bounce** occurs when an email address does not exist or is permanently unreachable.

- When this happens, the affected email address is **immediately marked as “Hard Bounced”** and transitions to the **“Held”** status, preventing any further emails from being sent to that address.

![]()

*Note: Previously, the 85-day resend rule was mentioned in the Help documentation, but it has since been removed.*

- In rare cases, even when an email address is clearly valid, it may still be reported as a hard bounce due to a temporary issue or false detection. If you would like to remove the “Held” status, please **create a case with Support and request the release**.
- Currently, there is no way to check email addresses that have been placed in a **“Held” status**. You can vote for this request on IdeaExchange [[here](https://ideas.salesforce.com/s/idea/a0BHp000016LlyXMAS/view-hard-bounce-held-addresses-in-marketing-cloud-growth-advanced-editions)].

## What is a Soft Bounce?

A **soft bounce** occurs when delivery fails due to temporary issues. Examples include the recipient’s mailbox being full or the receiving server being temporarily unavailable.

- The system retries delivery **several times within a 12-hour period**.  
  *Previously, the documentation explicitly stated up to 9 retries, but it has since been changed to the more ambiguous wording “several times.”*
- If delivery still fails, the result is recorded as a **soft bounce**.
- Normally, even if an address soft bounces, future sends will not be marked as **NOT SENT**.
- Depending on the ISP’s response, some may immediately return as a bounce and be logged as a **soft bounce**.  
  \*Bounce Reason Example: *Exchange 550 5.1.10 RecipientNotFound*
- In such cases, the address may be treated the same way as a hard bounce: moved to **Held** status, and in future sends it will be considered **NOT SENT (hard bounce)**.

🔗 Salesforce Help: [help.salesforce.com](https://help.salesforce.com/s/articleView?id=005103633&type=1)

In Marketing Cloud Engagement, it was possible to adjust the retry period, but in Marketing Cloud Next, **it appears that this cannot be changed at the moment**. As a result, depending on the timing of the retries, emails may end up being delivered late at night, so caution is required.

## Summary

- **Hard Bounce:** **Immediately** placed into “Held” status → Can be released by requesting Support.
- **Soft Bounce:** The system retries delivery **several times within 12 hours** → If delivery still fails, it is recorded as a soft bounce → Depending on the case, it may immediately become “Held.”

Note: When an address is marked as **NOT SENT**, the email send process does not occur, so no email credits are consumed.

That’s it for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
