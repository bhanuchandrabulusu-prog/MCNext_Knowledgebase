# SFMC Tips #204 : Data Cloud: Grouping, Ranking, and Limit Functions (GRL)

**Source:** https://medium.com/@marketingcloudtips/data-cloud-grouping-ranking-and-limit-functions-grl-9c8445541eb7

---

# SFMC Tips #204 : Data Cloud: Grouping, Ranking, and Limit Functions (GRL)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9c8445541eb7---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9c8445541eb7---------------------------------------)

5 min read

·

Nov 17, 2025

--

Photo by [COSMOH](https://unsplash.com/@cosmoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The **Group, Rank, and Limit (GRL) features** added in the October 2025 Data Cloud release are extremely powerful new capabilities that allow marketers to control segments more strategically.

Traditional segments had the characteristic of “extracting all profiles that match the conditions as they are”, making it difficult to meet advanced requirements such as priority management at the account level or setting upper limits on the number of people.

However, with the introduction of GRL, Data Cloud segments have evolved into a practical feature that enables you to “reach higher-value customers more appropriately”.

In this article, I will explain everything from the basics of GRL to use cases in a way that is as clear and practical as possible.

## What Is Group, Rank, Limit (GRL)?

GRL is a new feature that combines Group, Rank, and Limit and allows you to apply them within a single segment.

This enables marketers to perform advanced control directly from the GUI, such as:

- Limiting the number of people per account (e.g., only the top 2 per company)
- Prioritization within groups (e.g., job level, creation date descending, annual revenue descending)
- Fine-grained filtering applied in addition to Include / Exclude conditions

Practical requirements that were previously handled with Excel or queries can now be accomplished directly within Data Cloud.

## Considerations When Using GRL

Although it is a convenient feature, there are several points you must keep in mind to avoid issues in real-world operations.

### ① GRL is available only in segments on Profile DMOs

It **cannot** be used in the following cases:

- Engagement DMOs
- Other category DMOs
- When used as a child segment

### ② GRL is applied “in addition to” the result of Include / Exclude

Because GRL operates as “post-processing”, designing the base conditions correctly becomes extremely important.

### ③ Only “direct attributes” can be used

Fields via related objects cannot be used.  
Data model adjustments may be necessary depending on the situation.

### ④ Path selection is configured at the rule-set level

You specify the path per rule set — not per individual rule.

### ⑤ Up to three rule sets can be created

Possible patterns include:

- Limit only
- Limit + up to 3 Sorts (ascending/descending)
- Limit + up to 3 Groups

You can define up to three rule sets.  
Execution runs from the bottom rule set upward, and results are passed to the upper rule sets.

## Business Use Cases

The situation where GRL is most effective is:

**“Prioritize within a group, and limit the number of people”.**

Here are two representative examples.

### Use Case 1

### A technology company sending VIP invitations to executives

A company is planning a large global conference and wants to send special invitations to industry executives.

However, each account contains many contacts with different job levels, and budget limitations prevent inviting everyone.

GRL helps in this scenario.

### ✔ Solution: Extract “top 2 senior contacts” per account

**Group:** AccountId  
 ※ If attribute paths are displayed, choose the shortest one.

**Rank:** Job level (seniority)

Note: You will need to create something like a job-rank formula field.

```
IF(sourceField['Title'] == "CEO", 1,  
  IF(sourceField['Title'] == "VP", 3,  
    IF(sourceField['Title'] == "Manager", 5,  
      99  
    )  
  )  
)
```

**Limit:** Up to 2 per account

As a result, there were 3 accounts with registered contacts, so 2 × 3 = 6 contacts were extracted.

With this, the highest-ranking individuals in each customer company can now be extracted automatically and reliably.

### Use Case 2

### A financial institution extracting the “top X customers” based on annual income

Here is an example of a financial institution that ranks customers based on annual income by combining CRM data with external high-net-worth datasets.

The company wants to send a “VIP club membership” offer to the highest-value customers.

### ✔ Solution: Extract the “top X customers” by income

- **Sort:** Annual income (descending)
- **Limit:** Top X

This enables a strategic campaign targeted only at the highest-value segment.

## Effects of Using GRL

By adopting GRL, marketing activities can benefit in many ways:

### Improved conversion rates

You can prioritize outreach to high-value customers.

### Optimization of marketing budgets

Avoids over-targeting and maximizes the use of limited budgets.

### Balanced audience design

Prevents over-focusing on certain accounts and ensures fairer reach.

## Conclusion

Group, Rank, and Limit (GRL) is a powerful tool that solves — through standard Data Cloud functionality — requirements that previously required manual work or complex queries.

For marketers who want to:

- Extract the top N per account
- Rank customers and intentionally target only the upper layer
- Allocate budgets appropriately

GRL is truly a game-changer.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
