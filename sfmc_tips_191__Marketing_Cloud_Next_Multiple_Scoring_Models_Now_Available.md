# SFMC Tips #191 : Marketing Cloud Next: Multiple Scoring Models Now Available

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-multiple-scoring-models-now-available-b697017c6fd8

---

# SFMC Tips #191 : Marketing Cloud Next: Multiple Scoring Models Now Available

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b697017c6fd8---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b697017c6fd8---------------------------------------)

4 min read

·

Oct 14, 2025

--

Photo by [Jamie Street](https://unsplash.com/@jamie452?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Previously, only one scoring model was available in Marketing Cloud Next Growth and Advanced Editions. However, starting with the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843), the **Advanced Edition now supports multiple scoring models — up to two**. The Growth Edition remains limited to one scoring model.

This enhancement enables more flexible and accurate evaluations.

- Segment scoring by **need, product, region, or channel**
- Use **sub-scoring** as a testing environment to reduce migration costs when introducing new scoring rules

For details on the default rules of rule-based scoring, please refer to the article below.

[## SFMC Tips #112 : Marketing Cloud Next: Understanding Default Scoring Rules

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), leads and contacts can be scored based on…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-understanding-default-scoring-rules-1f45d9c9333f?source=post_page-----b697017c6fd8---------------------------------------)

## **Setup Procedure**

1. Previously, when you opened the scoring settings screen, it would take you directly to the rule settings page. However, starting with **Winter ’26**, the **Scoring Model List Page** is now displayed first. From here, you can click the **New** button to begin creating a model.

2. Next, create your **second scoring model**. When creating it, select whether the scoring will be for **Individuals (People)** or **Accounts**.

![]()

3. Then, select the **Identity Resolution Ruleset** to proceed. This selection is required because a **Calculated Insight** is automatically generated at creation and used to compute scores. In other words, the choice of which ruleset to use for calculation is critical, and **it cannot be changed later**.

![]()

4. The newly created scoring model will initially be in **Draft** status and will **not yet be activated (published)**. Also, the **Score ID** is automatically generated, so you cannot manually enter it.

5. At this stage, the **Calculated Insight** is also not yet scheduled. Once the scoring model is **activated (published)**, it will be scheduled automatically.

6. Even if multiple scoring models are created, as in this example, the **default rules** are the same across all models.

7. Once all configurations are complete, **publish the model**.

8. After publishing, it takes about **five minutes** for the **Calculated Insight** to become active.

9. You can then immediately use it in **Data Graphs** and other areas.

## Conclusion

As mentioned at the beginning, you can now perform scoring by **need, product, region, or channel**.

For example, the **sales team** can focus on the **purchase intent** score to guide their outreach, while the **marketing team** can use the **engagement** score to drive nurturing activities. This allows you to evaluate a single lead from multiple perspectives, even when each team values different criteria — enabling more **strategic actions** overall.

Another major advantage is the ability to **safely test and improve** your scoring setup. You can add or update new rules without affecting existing scores, allowing you to experiment freely without impacting active users.

For companies that actively leverage scoring, this is truly a **long-awaited release**. Take advantage of this new capability to achieve **more precise lead scoring**.

That’s all for this time!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
