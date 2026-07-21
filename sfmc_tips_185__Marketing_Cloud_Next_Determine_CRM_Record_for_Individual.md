# SFMC Tips #185 : Marketing Cloud Next: Determine CRM Record for Individual

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-determining-the-corresponding-crm-record-for-each-individual-3ad8b0d5a805

---

# SFMC Tips #185 : Marketing Cloud Next: **Determine CRM Record for Individual**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3ad8b0d5a805---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3ad8b0d5a805---------------------------------------)

4 min read

·

Oct 7, 2025

--

Photo by [Andreas Fickl](https://unsplash.com/@afafa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of **Marketing Cloud Next Growth & Advanced Edition**, a new feature called **“Determine CRM Record for Individual”** has been introduced. This action allows you to automatically identify whether an individual flowing through a **segment-triggered flow** corresponds to a **Contact**, **Lead**, or **Prospect** record in CRM.

![]()

Based on the result of this determination, you can apply different paths and configure only specific actions such as updating existing records or creating new ones.

![]()

![]()

> ***Note:*** *On the paths branching directly from this action, elements such as* ***Wait****,* ***End****, and* ***Send Email******Message*** *are* ***not supported****. If you need to include these elements or actions, they must be placed* ***after all paths merge****.*

Although the **Determine CRM Record for Individual** action is limited to **segment-triggered flows** and **doesn’t allow even email sends** directly from its paths 🤔, it can be quite useful in scenarios such as:

- Bulk updating specific fields for **Contacts**, **Leads**, or **Prospects** that meet certain segment criteria
- Resetting fields to **NULL** for **Contacts**, **Leads**, or **Prospects** that match certain segment conditions

### **Simplified Record Referencing in Winter ’26**

In **Winter ’26**, referencing records within a flow has become even easier. On paths following the **“Determine CRM Record for Individual”** action, you can now place elements such as **Update Records** without having to set up a **Get Records** element beforehand. This means that the object record relevant to that path is automatically available for direct access.

> *For example, if you’re working on the* ***Lead*** *path, you can reference all fields from the Lead object directly.*

### **Easier Access to Individual DMO Data Within Flows**

Another new enhancement in Winter ’26 is that **Individual DMO** fields are now available as “**Attributes**” in the **Flow Profile**.

\*This referencing capability isn’t limited to paths under **Determine CRM Record for Individual** — it applies more broadly.

You can now directly access fields from the **Individual DMO** based on the **Data Graph** associated with the flow. However, keep in mind that **related object attributes** cannot be referenced at this time.

With these two enhancements, you can now build flows without having to configure **Get Records** elements, significantly reducing setup time and complexity!!

## Conclusion

I’ve tested it myself and confirmed that it’s now possible to update CRM records easily using segment-based conditions.

That said, I also encountered a few cases where the expected records weren’t updated — likely due to a misunderstanding on my part about the branching logic. I plan to continue testing this behavior and will share more detailed insights soon.

As for use cases, the examples are still somewhat conceptual at this stage. Once I have clearer, more practical scenarios, I’ll update this post accordingly.

For now, just keep in mind that this new capability has been released — and it’s a big step forward for simplifying flow design.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
