# Waterfall Segmentation in Marketing Cloud Next explained

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/waterfall-segmentation

---

**Waterfall Segmentation is a handy tool to craft mutually excluding audiences and create a priority of membership among constituting segments.** Before prioritizing, [verify membership in your source segments](/marketing-cloud-next-deep-dives/list-your-segment-members/) so you know exactly who will flow through each sub-segment.

## What is a Waterfall Segment?

Technically speaking, a Waterfall Segment is not a Segment. **It is a list of Segments (called Sub-Segments)**. The rules to create a Waterfall Segment are not criteria-based like standard types of Segments, instead, a Waterfall Segment is composed of **ordered** Sub-Segments.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-A-Waterfall-Segment-composed-of-4-Sub-Segments-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-A-Waterfall-Segment-composed-of-4-Sub-Segments.png) 

A Waterfall Segment composed of 4 Sub-Segments

In the example above, if a Unified Individual is in the first Segment, it will be removed by the Waterfall from all three others where it exists. If not in the first, but in the second, it will be remove by the Waterfall from the two Segments below where it exists. And so on…

Every Sub-Segment has its own criteria-based definition, and being part of a Waterfall adds an extra filtering feature, so that **Sub-Segments are mutually exclusive**, and a **membership priority can be easily edited by reordering the Waterfall (Drag & Drop)**.

In the example above, you create a Summer ’25 discount Campaign. You don’t want your Customers to receive more that one discount. So you create your Sub-Segments and priorise them using a Waterfall. Then, you use your Sub-Segments in Segment Triggered Flows. **Waterfall Segments are not designed to be used directly, rather they must be seen as helpers / intelligent containers**.

For example, you could define your Sub-Segment’s criteria this way:

- *10% Discount Sub-Segment*: All unified individuals who made an online purchase over $100 within the past year.
- *25% Discount Sub-Segment*: All unified individuals who made purchases (either online or in-store) for a cumulated amount over $200, within the past 2 years.
- *33% Discount Sub-Segment*: All unified individuals who did not make any purchase within the past 3 years.
- *50% Discount Sub-Segment*: All unified individuals with a Engagement Score at least 100

## Let’s create a Waterfall Segment

### 1- Create Your Sub-Segments

First, you’ll need to create your Sub-Segments. [2 Methods to list your Segment members](/marketing-cloud-next-deep-dives/list-your-segment-members/). You can use whatever criteria you wish to create them (like in the Discount example above), but here the requirements so they are available for selection in a Waterfall Segment:

- They must be an **Unified Individual** Segments (so they can be used in Marketing Cloud)
- They must not be a **nested** Segment
- They must not **be scheduled** (the Waterfall Segment will publish them) but must be **Active**.
- They must not **belong to another Waterfall Segment**
- A Waterfall Segment has **20 Sub-Segments at most**

### 2- Create your Waterfall Segment

Data Cloud > Segment > +New. Use Visual Builder and select a Waterfall Segment:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Creating-a-Waterfall-Segment.png) 

Creating a Waterfall Segment

Choose the Data Space used by Marketing Cloud (most likely Default), give it a name, a description, and Segment on Unified Individual. Select a Standard Publish (Rapid Publish is not available for this type of Segment). Schedule the Publish frequency (Sub-Segments will be published at this pace).

### 3- Add and order your Sub-Segments

From Segment Designer, available Sub-Segments are displayed on the left sidebar (note, for Waterfall Segment, there are no CI or Field based criteria).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Available-Sub-Segments.png) 

Available Sub-Segments

Drag them on the Canvas:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Draging-a-Sub-Segment-in-the-Segment-Builders-Canvas.png) 

Draging a Sub-Segment in the Segment Builder’s Canvas.

Once finished, and at anytime later, you can re-order them. [Consent Management in Marketing Cloud Next explained](/marketing-cloud-next-deep-dives/consent-management/)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Re-ordering-Sub-Segments.png) 

Re-ordering Sub-Segments

## Final thoughts

Waterfall Segments take a very long time to refresh, so be patient. It seems Sub-Segments are published by their Waterfall Segment, and hence usable, long before the Waterfall Segment switches in Published mode.

You could try to mimic this feature using this exclusion tab in Segment designer, but the priority feature is much more easily handled using a Waterfall, plus Waterfall Segments act as a publisher for your Sub-Segments so they are not refreshed independently.
