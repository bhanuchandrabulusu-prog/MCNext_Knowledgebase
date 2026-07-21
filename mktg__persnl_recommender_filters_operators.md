# Recommendation Filter Operators

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters_operators.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Recommendation Filter Operators

Select the appropriate operator to compare catalog fields against static values, customer profile attributes, or session context to refine recommendation logic.

Static Filter Operators

A static operator compares a catalog field against a fixed value that you enter manually. The evaluation uses your Salesforce org’s time zone setting.

OPERATOR	DESCRIPTION	DATA TYPE	USAGE TIPS
Has Value	Matches fields that contain any data.	Text, Number, Date	Use to require that a recommended item has critical data, like a description or image URL.
Has No Value	Identifies fields that are null or missing.	Text, Number, Date	Use to exclude items with incomplete catalog data from being shown to visitors.
Is Equal To	Matches the catalog value exactly to the provided resource value.	Text, Number	Best for filtering by specific attributes, such as an In Stock status or a specific brand.
Is Not Equal To	Excludes items that match the provided resource value.	Text, Number	Use to filter out product types, such as excluding clearance items from a full-price gallery.
Is Less Than	Matches values that are lower than the specified number.	Number	Ideal for budget friendly sections where items must be under a specific price point.
Is Less Than Or Equal To	Matches values that are lower than or equal to the specified number.	Number	Use to set inclusive upper limits for numeric attributes, such as maximum weight or price.
Is Greater Than	Matches values that are higher than the specified number.	Number	Useful for identifying high-performance items with a rating above a certain score.
Is Greater Than Or Equal To	Matches values that are higher than or equal to the specified number.	Number	Use for minimum requirements, such as items with a 4-star and up customer rating.
Is Between	Matches values or dates within an inclusive range.	Number, Date, DateTime	Ideal for seasonal or holiday promotions.
Is Today	Matches the catalog date to the current calendar date.	Date, DateTime	Use for Deal of the Day.
Last Number of Days	Filters for items with a date within a set number of days in the past.	Date, DateTime	Use for recently added New Arrivals sections.
Next Number of Days	Filters for items with a date within a set number of days in the future.	Date, DateTime	Use to promote upcoming Events or pre-orders.
Is Before Current DateTime	Matches items with a catalog date that occurs before the present moment.	Date, DateTime	
Include Filter: Use with StartDate to show active items.
Exclude Filter: Use with EndDate to hide expired items.

Is After Current DateTime	Matches items with a catalog date that occurs after the present moment.	Date, DateTime	
Include Filter: Use with EndDate to show non-expired items.
Exclude Filter: Use with StartDate to hide future launches.
Decision Context and Profile Data Graph Filter Operators

These operators compare catalog fields against dynamic values, such as customer profile attributes, calculated insights, or the item a visitor is viewing.

You can’t use date operators because you can’t compare catalog date fields against dynamic values.

OPERATOR	DESCRIPTION	DATA TYPE	REQUIREMENT
Is Subset	Matches if every value in the catalog attribute is contained within the resource.	Text	Both left- and right-hand sides of the filter’s resource must have 1:N relationships. See Filter Items with the Is Subset Operator.
Match Any	Includes items if any catalog value is found within the resource.	Text	The right-hand resource must be mapped as a 1:N relationship.
Does Not Match	Excludes items if any catalog value is listed within the resource.	Text	The right-hand resource must be mapped as a 1:N relationship.
Is Equal To	Matches the catalog value exactly to the provided resource value.	Text, Number	Requires a value. Doesn’t evaluate nulls.
Is Not Equal To	Excludes items that match the provided resource value.	Text, Number	 
Is Less Than	Matches items with a numeric value lower than the resource.	Number	 
Is Less Than Or Equal To	Matches items with a numeric value lower than or equal to the resource.	Number	 
Is Greater Than	Matches items with a numeric value higher than the resource.	Number	 
Is Greater Than Or Equal To	Match items with a numeric value higher than or equal to the resource.	Number	 
Filter Use Cases

Review these common business scenarios to create personalized recommendation logic.

Static Filter Use Cases

Show Only In-Stock Items

Prevent orders for unavailable products by showing only items that are in stock.

Condition tab: Include
Item Data Graph Resource: Availability
Filter type: Static
Operator: Is Equal To
Value: In Stock

Hide Expired Items

Show shoppers only active promotions by removing products that have passed the expiration date.

Condition tab: Exclude
Item Attribute: Expiration Date
Filter type: Static
Operator: Is Before Current DateTime
Value: [leave blank for system time]
Dynamic Filter Use Cases

Recommend Items by Color

Create a visually consistent experience, such as a More in this Color gallery, by recommending products that are the same color as the item the visitor is viewing.

Condition tab: Include
Item Data Graph Resource: Color
Filter type: Decision Context
Operator: Match Any
Decision Context Resource: Color

Boost Cross-Category Discovery

Encourage customers to explore new product lines by recommending items from categories that they haven’t interacted with.

Condition tab: Include
Item Data Graph Resource: Category
Filter type: Profile Data Graph
Operator: Does Not Match
Profile Data Graph Resource: Profile > Recent_Interaction_Categories

Exclude Previously Purchased Items

Increase recommendation variety by excluding products that the customer has already bought.

NOTE Before configuring this filter, create a calculated insight in Data 360 that aggregates product IDs from past sales order data.
Condition tab: Exclude
Item Data Graph Resource: Product ID
Filter type: Profile Data Graph
Operator: Is Equal To
Profile Data Graph Resource: Profile > Recent_Purchases_IDs
SEE ALSO
Add Recommendation Filters
