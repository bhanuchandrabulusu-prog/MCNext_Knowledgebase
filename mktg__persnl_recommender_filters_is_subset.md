# Filter Items with the Is Subset Operator

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters_is_subset.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Filter Items with the Is Subset Operator

Create strict eligibility rules before showing a recommendation or promotion.

The Is Subset operator confirms that all the attributes defined on a catalog item are contained within the resource. Use this operator when a recommendation must satisfy all the criteria to be valid.

Technical Requirements

To use this operator, your data must meet these criteria.

Filter types: Use this operator only with the Profile Data Graph filter (to match against visitor behavior) or Decision Context filter (to match against the item being viewed).
Objects: The object must support multiple values per record.
One-to-many (1:N) relationships: The attributes included in the filter must have a one-to-many relationship with their primary record, such as a specific Product or Individual.
Direct attributes: You can’t use this operator with a direct attribute because it has a one-to-one (1:1) relationship with the primary record.
System limits: The resource and the catalog field can’t have more than 100 attributes per dataset.
Examples

Entitlement Check (Profile Data Graph)

Goal: Before showing a promotion, confirm that a customer belongs to all the required segments.

Catalog Item (Promotion): The attributes defined on the item are the Loyal Customer AND High Spender segments.
User A (Match): User A’s profile contains Loyal Customer, High Spender, and Newsletter Subscriber. Because the item’s attributes are completely contained within the user’s values, the promotion is recommended.
User B (No Match): User B’s profile contains only Loyal Customer. Because High Spender isn’t contained in the user’s values, the promotion isn’t shown.

Streaming Compatibility (Decision Context)

Goal: Recommend premium movies only if the visitor’s device and account plan meet every technical and subscription requirement.

Catalog Item (Movie): A Premium 4K Title requires the user’s device and plan to have a Premium Plan AND 4K Hardware.
Context Item A (Match): The user has a Premium Plan and is watching on a 4K Smart TV. The movie is recommended because the context satisfies all its requirements.
Context Item B (No Match): The user has a Premium Plan and is using a 1080p mobile phone. The movie isn’t recommended because the context doesn’t contain the required 4K attribute.
Tips
Empty fields: If a catalog field is empty, it’s considered a match for all users because an empty set is always a subset.
Alternative logic: To recommend items when a visitor matches at least one requirement instead of all, use the Match Any operator.
SEE ALSO
Add Recommendation Filters
