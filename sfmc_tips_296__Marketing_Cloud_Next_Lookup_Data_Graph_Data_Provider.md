# SFMC Tips #296 : Marketing Cloud Next: Lookup Data Graph Data Provider

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-lookup-data-graph-data-provider-0054d3fcdd83

---

# SFMC Tips #296 : Marketing Cloud Next: Lookup Data Graph Data Provider

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0054d3fcdd83---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0054d3fcdd83---------------------------------------)

5 min read

·

May 17, 2026

--

Photo by [Kiki Siepel](https://unsplash.com/@studiokiek?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Editions, a **Lookup Data Graph** became available, allowing existing profile data graphs to be enhanced by referencing **“data that is not directly tied to people”** such as product catalogs.

- With this feature, you can add up to **five Lookup Data Graph Data Providers** to a single email message.
- When using a lookup data graph as a data source, you specify a **Primary Key (PK)** and dynamically retrieve data related to the message recipient using that value.

## Why Use a “Lookup” Structure?

Why was this kind of **lookup-based** mechanism designed in the first place?

For example, sales data and purchase history are **data tied to individuals**, in the sense of “who purchased what”.

Therefore, it does not feel unnatural to associate them with a **profile data graph** centered around Unified Individual.

On the other hand, a product catalog itself is not originally data tied to a “person”.

In other words, if massive and independent master data such as:

- Product catalogs
- Inventory information
- Price masters
- Campaign information

were all directly nested and stored inside the profile data graph, there is a concern that the data graph would become bloated and architecturally unhealthy.

In particular, data such as product catalogs are not constantly used in every scenario.

There are many cases where:

> *“It is sufficient to retrieve only the necessary data at the necessary timing.”*

For that reason, it is likely that Lookup Data Graph Data Providers were prepared as a mechanism to keep such data separated from the profile data graph and dynamically reference it only when needed.

In addition, data such as:

- Inventory quantity
- Pricing
- Campaign information

often has a high update frequency and requires real-time characteristics.

If such data were included directly in a Unified Individual–based data graph, there is a possibility that the overall update load and recalculation cost of the data graph would become significantly larger.

Therefore, in many cases, it may be more appropriate to separate highly volatile master data from the profile data graph and reference it only when necessary.

Incidentally, Salesforce Personalization is also designed in a similar way, where data is managed separately as:

- [Salesforce Personalization Profile Data Graph](https://agentforce-marketing-9cf347fa7db7.herokuapp.com/workshops/salesforce-personalization/profile-data-graphs.html)
- [Salesforce Personalization Item Data Graph](https://agentforce-marketing-9cf347fa7db7.herokuapp.com/workshops/salesforce-personalization/item-data-graphs.html)

## Configuration Method

For example, let us assume that under the current specification, Sales Order Product Engagement stores the “product number” of a sold product, but does not store the “product name”.

In this case, you can use the “product number” held by Sales Order Product Engagement as the **Primary Key (PK)** and reference the “product number” on the Goods Product data graph side to retrieve the “product name” stored in the Goods Product data graph.

### 1. Add a Data Source

First, open the content, go to the “Data Sources” tab, and click “Add”.

### 2. Select Lookup Data Graph Data Provider

Before deciding the Name (API Name), open **Lookup Data Graph Data Provider**.

*It is recommended to enter the Name (API Name) immediately before saving because it may get cleared during the setup process.*

### 3. Select the Lookup Target Data Graph

In Lookup Data Graph, open the product data graph called “Products”.

### 4. Configure the Primary Key

For the Primary Key, select a **merge field**.

Since the Product field in Sales Order Product Engagement represents the product ID, select that field.

### 5. Configure the Name (API Name) and Save

Once the Primary Key has been entered, input the Name (API Name) and save the configuration.

*It is recommended to use a Name (API Name) that is easy to understand later. Using the data graph name itself is probably a good choice.*

## How to Use

Once the setup is complete, a **second data graph** becomes available in the merge fields.

This makes it possible to dynamically display information in email messages that is not stored within the profile data graph alone, such as:

- Product names
- Product descriptions
- Product images
- Latest pricing

When previewed, it appears as shown below.

What did you think?

It may be easier to understand Lookup Data Graphs if you think of them as a mechanism for loosely coupling **“behavioral data tied to individuals”** with **“independent master data”.**

However, I do think the difficulty of reaching this level of configuration is somewhat high.

In environments already implementing Salesforce Personalization and similar solutions, there may be cases where this can be utilized as-is, but personally, I also have some doubts about whether it is necessary to forcefully build out this configuration from scratch.

If the same requirement can be implemented more simply, prioritizing the simpler approach may be more realistic.

Rather than something that must be used aggressively, I think it is better viewed as:

> *“Use it when the opportunity naturally arises.”*

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
