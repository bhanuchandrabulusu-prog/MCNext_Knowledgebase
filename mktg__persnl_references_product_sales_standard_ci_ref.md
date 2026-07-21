# Product Top Sellers Standard Insight

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_product_sales_standard_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Product Top Sellers Standard Insight

This insight calculates the sum of products that have been sold. Salesforce Personalization uses the output from this insight to create a list of top-selling products. The Maximize Revenue objective-based recommender requires the provided SQL code in the calculated insight.

When creating this insight, use the instructions in Create a Calculated Insight Using SQL in Data 360 documentation. You can then add the insight to the Salesforce Personalization near real-time item data graph.

SELECT
   ssot__GoodsProduct__dlm.ssot__Id__c as ProductId__c, SUM(ssot__SalesOrderProductEngagement__dlm.ssot__OrderedQuantity__c) as TotalSoldUnits__c from ssot__SalesOrderProductEngagement__dlm 
JOIN
   ssot__GoodsProduct__dlm
ON 
   ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c = ssot__GoodsProduct__dlm.ssot__Id__c group by ssot__GoodsProduct__dlm.ssot__Id__c

SEE ALSO
Configure the Top Sellers Standard Insight for Rule-Based Recommenders
