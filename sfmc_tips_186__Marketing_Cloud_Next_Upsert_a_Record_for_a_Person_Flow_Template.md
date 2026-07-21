# SFMC Tips #186 : Marketing Cloud Next: Upsert a Record for a Person Flow Template

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-upsert-a-record-for-a-person-flow-template-76fe6855686e

---

# SFMC Tips #186 : **Marketing Cloud Next: Upsert a Record for a Person Flow** Template

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--76fe6855686e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--76fe6855686e---------------------------------------)

4 min read

·

Oct 8, 2025

--

Photo by [Jonathan Cooper](https://unsplash.com/@theshuttervision?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of **Marketing Cloud Next Growth & Advanced Edition**, a new flow template called **“Upsert a Record for a Person”** was introduced.

This template enables you to automatically search, update, or create the relevant record even in cases where a **Salesforce ID** is not yet available when the flow starts — such as form-triggered flows.

**Tip:** To display Marketing Cloud–specific flow templates, click **New Flow** and search for **“marketing”.**

As of [**Summer ’25**](/p/4ad6f39c5d6d), there were five available templates:

- Birthday promotion scenario
- Event registration scenario
- Lead nurturing campaign scenario
- Re-engagement scenario
- Form submission and follow-up scenario

## What is the “Upsert a Record for a Person” Flow Template?

This template first searches for an existing **Contact** or **Lead** record.  
If a matching record is found, it updates that record.  
If none exists, it creates a new **Prospect** record.

By referencing this automation in a **Subflow element**, you can extend your existing flows and achieve more consistent flow construction.

> ***Tips:*** *A* ***subflow element*** *is a component in a Salesforce Flow that lets you call another flow from within your current flow. It’s like reusing a mini flow inside a bigger one — so you don’t have to rebuild the same logic multiple times.*

![]()

## Purpose of the Template

When customer information is submitted via a form, **a quick response is critical**. However, when ID resolution takes time, a Salesforce ID might not be immediately available.

With this template, you can instantly link the form submission to an existing record or create a new Prospect record — allowing for **faster follow-up and smoother automation**.

## How to Use

1. **Create a flow** using the “**Upsert a Record for a Person**” template  
    (It’s designed as an autolaunched flow with no trigger, since it’s meant to be used as a subflow.)
2. **Reference this flow** within a subflow element.
3. The flow **returns the “recordId”** of the created or updated record.
4. In the parent automation, use this “recordId” to access individual data.

### Flow Variables

![]()

**Inputs:**

- `company`
- `lastname`

**Output:**

- `recordId`

This process automatically handles **record matching and deduplication**, maintaining data consistency while enabling rapid marketing actions.

## Final Thoughts

After reviewing the template, it’s clear that it’s **not a one-size-fits-all solution** — it requires customization for each organization.

Therefore, it’s best to **take inspiration from its design concepts**, such as “performing update operations” or “using subflows for reusability”, and tailor the logic to fit your own use case.

Ultimately, this template serves as a **starting point** — much like Journey templates in **Marketing Cloud Engagement** — a resource to **learn the underlying techniques** and adapt them to your needs.

Also, based on my understanding, a new feature introduced in **Summer ’25** allows you to **directly reference records** created by the **“Create Records”** element.

For example, a Lead record created after a form submission can now have its **Salesforce ID** referenced directly in subsequent flow elements.

In practice, this capability might already cover many use cases.  
However, the advantage of the new template lies in its **step-by-step handling of Contacts → Leads → Prospects**, and once set up, it can be **reused efficiently** across multiple processes.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
