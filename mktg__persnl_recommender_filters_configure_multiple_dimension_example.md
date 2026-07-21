# Co-Bought Recommender with Multiple Dimension Filters Configuration Example

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters_configure_multiple_dimension_example.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Co-Bought Recommender with Multiple Dimension Filters Configuration Example

Use calculated insights and the power of filters to configure a recommender to generate a list of products that have frequently been purchased together.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommendation filters:	Change and Edit Recommenders

Before configuring this example, make sure to perform these tasks:

Create a calculated insight with two product dimensions (for example, p1 and p2 representing two product dimensions) and a metric (for example, count), which is a collection of the number of times the two products have been purchased together. ‌To create calculated insights, see Calculated Insights. When creating the insight, you can use the expression found in Co-Bought Standard Insight for Products.
Configure a profile data graph based on Unified Individual ID as the primary DMO, and which relates to other DMOs mapped to product and sales engagement. To create data graphs, see Create a Data Graph.
Configure an item data graph based on Goods Product as the primary DMO, and contains the created co-bought standard calculated insight. To create data graphs, see Create a Data Graph.
Create a rule-based recommender using the steps in Configure a Recommender, ensuring that you select the co-bought standard calculated insight, and that you select count as the Sort Measure.

To add multiple dimension filters to an existing recommender:

From the Recommenders page, open the recommender that you want to add filters to.
Click Edit.
Click Next to progress through the Recommender Properties pages until you reach the Filters page. 
Click Add Condition.
Select Calculated Insights from Item Data Graph Resource, select the created calculated insight, and then the product attribute that you want to compare on the web page.
Select Decision Context as the filter type.
Select Matches as the operator.
Select Direct Attributes as the Decision Context Resource, and then select the product whose attribute you want to compare with the Data Graph Resource selection.
Click Save.
Personalization creates the recommender, and you can use it as a personalization point decision.
SEE ALSO
Co-Bought Standard Insight for Products
