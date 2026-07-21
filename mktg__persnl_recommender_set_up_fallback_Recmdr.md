# Set Up a Fallback Recommender

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_set_up_fallback_Recmdr.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Set Up a Fallback Recommender

Select a fallback recommender to use when your recommender doesn’t return sufficient recommendation items. If restrictive filters or insufficient data prevent a recommender from returning sufficient items, Salesforce Personalization uses the fallback recommender to fill the remaining slots.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommenders:	Change and Edit Recommenders

Fallback recommenders can’t guarantee a full set of recommendations in the following scenarios:

The fallback recommender has restrictive filters.
The fallback recommender doesn't have sufficient information.
The underlying system is not reachable.
On the Recommenders page, open the recommender that you want to add a fallback recommender to, and click Edit.
Turn on fallback recommender.
Select a fallback recommender.

The menu lists only the recommenders that share the same data space, item data graph, and profile data graph as the primary recommender. Additionally, the recommenders must complete at least one successful training session.
