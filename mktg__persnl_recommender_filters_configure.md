# Add Recommendation Filters

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Add Recommendation Filters

Use filters to control exactly which items appear in your recommendations.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommendation filters:	Change and Edit Recommenders
In the App Launcher, find and select Recommenders.
Open your recommender and click Edit.
Click Next until you reach the Filters page. 
Select the Include or Exclude filter tab.
Choose when the filter applies: All conditions are met or Any condition is met.
Click Add Condition.
Select an item data graph resource.
Personalization uses this to decide if an item is a good fit for a recommendation. You can pick a direct attribute, a related attribute, or a calculated insight. When you select an option, use the subcategories to narrow your choice.
Select a filter type.
OPTION	DESCRIPTION
Decision Context	Matches attributes to the item a visitor is currently viewing. For example, if you choose the Color resource, Personalization includes or excludes items that match the color of the visitor's current item.
Static	

Filters items using specific attributes like price, category, or date. For example, include items under $10 or exclude those published before a certain date.

You can also filter by dynamic context variables included in your request. To configure dynamic context variables, see Filter Recommendations Using Dynamic Context Variables.


Profile Data Graph	

Uses visitor behavior, such as purchase history, based on calculated insights. For example, you can hide items a user already bought or show specific items only to returning visitors.

Prerequisite: Before you choose this option, create a calculated insight associated with your selected profile data graph.

Select an operator to evaluate the filter. Available operators depend on the filter type and field data type. For details on available operators, see Recommendation Filter Operators.
Define the filter value or resource anchor:
Static: Enter the specific value to filter against.
Decision Context: Choose an attribute to act as the context anchor (your point of reference).
Profile Data Graph: Filter recommendations based on visitor behavior and history. Select a direct attribute, related attribute, or calculated insight. To narrow results, apply optional metrics for loyalty targeting (such as specific brands) or value constraints. As a prerequisite, create a calculated insight for your selected profile data graph before using this option.
(Optional) Add another filter condition.
Click Save.
Personalization creates the recommender, and you can use it as a personalization point decision.
