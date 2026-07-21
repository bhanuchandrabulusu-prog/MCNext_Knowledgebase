# SFMC Tips #291 : Marketing Cloud Next: Shared IP Addresses and Dedicated IP Addresses

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-shared-ip-addresses-and-dedicated-ip-addresses-5237675268e2

---

# SFMC Tips #291 : Marketing Cloud Next: d IP Addresses and Dedicated IP Addresses

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--5237675268e2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--5237675268e2---------------------------------------)

4 min read

·

May 12, 2026

--

Photo by [Tide\_trasher\_x](https://unsplash.com/@tide_trasher_x?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Editions, the long-awaited **“Dedicated IP Address”** feature was introduced. Until now, email sending had only been performed through **“d IP Addresses”.**

You can check the currently used IP address type and which IP pool you belong to from the following screen.

- **Settings ＞ Unified Messaging ＞ Email ＞ Settings ＞ Sending IP Addresses**

## How It Works

Dedicated IP addresses in Marketing Cloud Next are **not something that needs to be purchased separately from Salesforce as an additional option.**

When the monthly sending volume from Marketing Cloud Next exceeds a certain threshold (**approximately 5 million emails per month as a guideline**), the system automatically detects it and begins the migration process to **Dedicated IP Addresses**.

After that, when the sending volume reaches around **10 million emails per month**, a **second Dedicated IP Address** is assigned. As the volume continues to increase, additional IPs are assigned sequentially.

In addition, if the sending volume continues to remain below the threshold for a certain period of time, the assigned Dedicated IP Addresses are sequentially reclaimed, and eventually sending is returned to **d IP Addresses**.

For those who are familiar with Marketing Cloud Engagement, this may feel like a unique approach.

There are also the following mechanisms.

## About IP Warm-Up

When migration to Dedicated IPs begins, **IP warm-up is automatically performed by Salesforce.**

The warm-up period is carried out over approximately **0 to 35 days** after the migration starts.

In addition, if sending volume exceeds the limit during the warm-up period, the excess portion continues to be sent from d IPs, so users do not need to finely control sending volume themselves.

As a result, the traditional **“manual IP warm-up process” basically becomes unnecessary.** However, this only applies to **“IP reputation”.** From the perspective of **domain reputation (domain warm-up),** it is still necessary to maintain a gradual sending plan and stable sending quality.

## About Dedicated IP Address Reclamation

If the average sending volume over the most recent **45 days** falls below the threshold (**approximately 5 million emails per month as a guideline**), the assigned Dedicated IP Addresses are sequentially reclaimed.

Furthermore, if only the final **1 IP** remains and sending below **5 million emails per month** continues for **90 days**, it is automatically returned to d IP Addresses.

The reclaimed Dedicated IP Addresses are reused after a certain cooldown period.

## Introduction of the Gray IP Address Pool

Among d IP users, accounts with high bounce rates (**approximately 5% as a guideline**) are temporarily moved to a dedicated IP pool called the **“Gray Pool”.**

This is an area separated from the normal d IP pool and Dedicated IP pool, and emails are sent from this pool until the bounce rate improves.

This mechanism helps maintain the overall health of both the d IP pool and Dedicated IP pool.

## Outside the Scope of SLA (Service Level Agreement)

Please note that the figures introduced here are only **“guidelines”.**

These are considered **outside the scope of the SLA (Service Level Agreement),** so even if there are cases such as:

> *“Sending volume exceeds 5 million emails per month, but migration to Dedicated IPs does not happen immediately.”*

it is necessary to rely on Salesforce’s control and judgment.

What did you think?

For those who have been using Marketing Cloud Engagement for a long time, this may appear to be a very interesting mechanism.

The fact that **“IP warm-up may no longer be necessary”** is extremely attractive, but the importance of **sending quality itself** remains unchanged.

In particular, providers such as **Google** are increasingly emphasizing **“domain reputation”** in recent years.

Therefore, the following basic practices for maintaining sending quality continue to be extremely important regardless of whether you use d IPs or Dedicated IPs:

- **Do not send to invalid email addresses**
- **Prioritize sending to high-quality customers who are likely to open and click**
- **Minimize unsubscribes and complaints**

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
