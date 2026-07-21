# Configure the Example Objective-Based Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_example_objective_based_recommender_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure the Example Objective-Based Recommender

The object-based recommender provides Maximize Revenue recommendations based on increased checkout frequency, increased cart value at checkout, or both.

Define the recommender properties and click Next.

PARAMETER	EXAMPLE SETTING
Data Space	default
Profile Data Graph	RealtimeProfile
Item Data Graph	Products
Recommender Name	Maximize Revenue
Recommender API Name	Maximize_Revenue
Description	AI-driven recommender
Select Objective-Based Recommendations as the recommender type and click Next.
Select Maximize Revenue as the objective and click Next.
Define filters to select what items you want the recommender to display.

TAB	CONDITION	PARAMETER	EXAMPLE SETTING
Include	Condition1	Item Data Graph Resource	Attributes>Category1
 	 	Filter Type	Static
 	 	Operator	Is Equal To
 	 	Value	Men
Save your work.
SEE ALSO
Experiment Prerequisite Configurations
Recommender Comparison Example Configuration
