# Filter Recommendations Using Dynamic Context Variables

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filter_using_dynamic_variable.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Filter Recommendations Using Dynamic Context Variables

Include or exclude items based on the dynamic variables passed when a user makes a personalization request. For example, you can configure a filter to include items that match the category value passed in the personalization request.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommendation filters:	Change and Edit Recommenders

When configuring a filter, keep these considerations in mind.

Specify the dynamic context variable in the Salesforce Merge Language (SML) format. The syntax consists of an open curly brace and an exclamation mark, followed by the variable name, and a closing curly brace. For example, if you want to filter the items based on the value passed for the category field, then enter {!category}.
When a user makes a personalization request, the recommender replaces the SML variable in the filter with the corresponding context attribute value on the personalization request. If there’s no value for the variable in the personalization request, the recommender discards the filter. For information about passing context variables in personalization requests, see Request Personalization.
The variable can have up to 64 characters, including alphanumeric characters and underscores, but can’t have a prefix or suffix. For example, you can’t use {!myCategory}-category.
A static filter can have only one dynamic context variable. To add multiple variables, create a static filter for each variable.
On the Recommenders page, open the recommender that you want to add filters to, and click Edit.
Click Next to progress through the Recommender Properties pages until you reach the Filters page.
On the Filters page, click Add Condition.
Select an item data graph resource.
For the filter type, select Static.
For the operator, select Matches.
Enter the dynamic context variable in SML format, for example, {!category}.
Click Save.
SEE ALSO
Set Up Dynamic Context Variables
Request Personalization
