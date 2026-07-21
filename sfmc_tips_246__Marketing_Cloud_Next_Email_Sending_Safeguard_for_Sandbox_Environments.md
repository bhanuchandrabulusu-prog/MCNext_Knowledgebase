# SFMC Tips #246 : Marketing Cloud Next: Email Sending Safeguard for Sandbox Environments

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-email-sending-safeguard-for-sandbox-environments-7f285435afe1

---

# SFMC Tips #246 : Marketing Cloud Next: Email Sending Safeguard for Sandbox Environments

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7f285435afe1---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7f285435afe1---------------------------------------)

2 min read

·

Feb 7, 2026

--

Photo by [Kunj Parekh](https://unsplash.com/@kunjparekh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

To enable safer use even in environments that contain actual customer data, such as **Full Sandbox** and **Partial Copy Sandbox**, a new feature was added in the [Spring ’26 release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition that automatically discards emails sent from Sandbox environments (Full Sandbox and Partial Copy Sandbox).

This helps prevent the risk of accidentally sending emails to customers registered in the production environment.

> *※ Currently, Developer Sandbox and Developer Pro Sandbox are not supported.*

This feature can be accessed from **Setup → Marketing Cloud → Email**.

When this feature is enabled, **all emails sent from Full Sandbox and Partial Copy Sandbox will not be delivered externally**.

However, if you want to allow delivery only to specific domains for testing purposes, you can register up to **five allowed domains (Allow List)** to enable delivery as exceptions.

When registering domains, add them **including the “@” symbol**.

Example: @gmail.com

## Conclusion

Opportunities to develop and test using Sandbox environments are increasing every year, but accidental email delivery can lead to serious incidents.

This feature is a **very important safety mechanism** designed to prevent such accidents before they occur. If you are using Sandbox environments (Full Sandbox or Partial Copy Sandbox), please enable and actively use this feature.

That’s all for today.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
