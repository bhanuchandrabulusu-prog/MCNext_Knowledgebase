# SFMC Tips #132 : Understanding Object Activity in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/understanding-object-activity-in-journey-builder-621c7fac53a2

---

# SFMC Tips #132 : Understanding Object Activity in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--621c7fac53a2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--621c7fac53a2---------------------------------------)

4 min read

·

Jun 8, 2025

--

Photo by [RhondaK Native Florida Folk Artist](https://unsplash.com/@rhondak?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud Engagement, when integrated with Salesforce CRM via Marketing Cloud Connect, you can use the **Object Activity** in Journey Builder to efficiently update CRM object data based on Marketing Cloud data.

![]()

## Exploring the Behavior of “Find and Update”

The behavior of **Find and Update** in Object Activity can sometimes be complex. This article provides a breakdown of its functionality with illustrative scenarios.

### Scenarios Covered:

1. When no matching records are found in CRM.
2. When exactly one matching record is found in CRM.
3. When two or more matching records are found in CRM.

## 1. When No Matching Records Are Found

This option allows you to choose the action to take when no matching records are found on the CRM side during a lookup.

![]()

### Option 1: “Do Not Update”

![]()

- **Lookup by Salesforce ID**: The journey status will show as **Soft Error**, and **no action** will be taken in CRM.
- **Lookup by other fields (**e.g., Email**)**: The journey status will show as **Success**, but **no action** will be taken in CRM.

### Option 2: “Create New Record”

![]()

- The journey status will show as **Success**, and a new record will be **created** in CRM.

**Important Notes:**

- If the new record triggers **Potential Duplicate rules**, the journey status will show as **Soft Error**, and no new record will be created. For objects where duplicate rules are not enforced, records may be created repeatedly.
- If the record violates **Validation Rules**, the journey status will show as **Soft Error**, and no new record will be created. These errors will only become apparent after submission; they will not be flagged during setup.

## 2. When Exactly One Matching Record Is Found

This scenario represents a case where updates on the CRM side are successfully executed, meaning it does not involve the use of the following options.

![]()

- The journey status will show as **Success**, and the record will be updated as expected.

**Important Notes:**

- Fields used in the lookup criteria (e.g., Opportunity Name) can also be updated, even if they are part of the lookup.
- When searching using criteria other than Salesforce ID and performing updates in a one (CRM) to many (MC) relationship, the update will use the bottommost record in the Data Extension.
- When creating or updating **Number** or **Currency** fields in CRM, the corresponding field in Marketing Cloud must be of the **Decimal** type.
- If the record violates **Validation Rules**, the journey status will show as **Soft Error**, and no updates will occur.

## 3. When Two or More Matching Records Are Found

Behavior is determined by the selected handling option for “Multiple Matching Records Fand ound”:

![]()

### Option 1: “Do Not Update”

![]()

- The journey status will show as **Success**, and no action will be taken in CRM.

### Option 2: “Update Last Modified Record”

![]()

- In the journey, the status is set to “Success,” and the record with the most recent Last Modified Date on the CRM side is updated.

### Option 3: “Create New Record”

![]()

- The journey status will show as **Success**, and a new record will be created in CRM.

**Important Notes:**

- Lookup by Salesforce ID will not produce multiple matches because Salesforce IDs in CRM are unique, meaning this scenario occurs only when the lookup is performed using criteria other than Salesforce ID.
- If the new record triggers **Potential Duplicate** rules, the journey status will show as **Soft Error**, and no new record will be created. For objects where duplicate rules are not enforced, records may be created repeatedly.
- If the record violates **Validation Rules**, the journey status will show as **Soft Error**, and no updates or creations will occur.

## Conclusion

By understanding these behaviors, you can better leverage Object Activity in Journey Builder to ensure accurate CRM updates while avoiding common pitfalls.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
