# Co-Bought Standard Insight for Products

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_co_bought_standard_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Co-Bought Standard Insight for Products

This insight determines products purchased along with the product currently being viewed.

When creating this insight, use the instructions in Create a Calculated Insight Using SQL in Data 360 documentation. You can then add the insight to the Salesforce Personalization near real-time item data graph.

SELECT
     ssot__GoodsProduct__dlm.ssot__Id__c as p1__c,
     Table2.productId__c as p2__c,
     SUM(Table2.count__c) as countP2__c
FROM
(
     SELECT 
          ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c as      
          productId__c,
          ssot__ProductOrderEngagement__dlm.ssot__Id__c as orderNumber__c,
          count(ssot__SalesOrderProductEngagement__dlm.ssot__Id__c) as 
          count__c
FROM 
     ssot__SalesOrderProductEngagement__dlm
JOIN 
     ssot__ProductOrderEngagement__dlm
ON 
     ssot__ProductOrderEngagement__dlm.ssot__Id__c =      
     ssot__SalesOrderProductEngagement__dlm.ssot__ProductOrderEngagementId__c
GROUP BY
     ssot__ProductOrderEngagement__dlm.ssot__Id__c,
     ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c
) as Table1
JOIN
(
     SELECT 
          ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c as 
          productId__c,
          ssot__ProductOrderEngagement__dlm.ssot__Id__c as orderNumber__c,
          count(ssot__SalesOrderProductEngagement__dlm.ssot__Id__c) as 
          count__c
FROM 
     ssot__SalesOrderProductEngagement__dlm
JOIN 
     ssot__ProductOrderEngagement__dlm
ON 
     ssot__ProductOrderEngagement__dlm.ssot__Id__c =    
     ssot__SalesOrderProductEngagement__dlm.ssot__ProductOrderEngagementId__c
GROUP BY
     ssot__ProductOrderEngagement__dlm.ssot__Id__c,
     ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c
) as Table2
ON 
     Table1.orderNumber__c = Table2.orderNumber__c
JOIN 
     ssot__GoodsProduct__dlm
ON 
     ssot__GoodsProduct__dlm.ssot__Id__c = Table1.productId__c
WHERE 
     Table1.productId__c <> Table2.productId__c
GROUP BY 
     ssot__GoodsProduct__dlm.ssot__Id__c,
     Table2.productId__c
