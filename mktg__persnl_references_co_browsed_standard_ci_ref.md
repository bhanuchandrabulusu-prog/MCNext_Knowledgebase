# Co-Browsed Standard Insight for Articles

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_references_co_browsed_standard_ci_ref.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Co-Browsed Standard Insight for Articles

This insight determines the articles most co-browsed in reference to the current article.

When creating this insight, use the instructions in Create a Calculated Insight Using SQL in Data 360 documentation. You can then add the insight to the Salesforce Personalization near real-time item data graph.

SELECT 
     ssot__KnowledgeArticleVersion__dlm.ssot__Id__c as article1__c,
     Table2.knowledgeArticle_id as article2__c,
     SUM(Table2.count__c) as count_Article2__c
FROM
(
     SELECT 
          ssot__KnowledgeArticleEngagement__dlm.ssot__IndividualId__c individual_id,
          ssot__KnowledgeArticleEngagement__dlm.ssot__KnowledgeArticleVersionId__c  
          knowledgeArticle_id,
          count (ssot__KnowledgeArticleEngagement__dlm.ssot__Id__c) count__c
     FROM 
          ssot__KnowledgeArticleEngagement__dlm
     WHERE 
          ssot__KnowledgeArticleEngagement__dlm.ssot__EngagementChannelAction__c IN ( 
          'catalog-object-click-start' )
     GROUP BY 
          ssot__KnowledgeArticleEngagement__dlm.ssot__IndividualId__c,
          ssot__KnowledgeArticleEngagement__dlm.ssot__KnowledgeArticleVersionId__c
) as Table1
     JOIN
     (
          SELECT 
               ssot__KnowledgeArticleEngagement__dlm.ssot__IndividualId__c individual_id,
               ssot__KnowledgeArticleEngagement__dlm.ssot__KnowledgeArticleVersionId__c   
               knowledgeArticle_id,
               count (ssot__KnowledgeArticleEngagement__dlm.ssot__Id__c) count__c
          FROM 
               ssot__KnowledgeArticleEngagement__dlm
          WHERE    
               ssot__KnowledgeArticleEngagement__dlm.ssot__EngagementChannelAction__c IN ( 
               'catalog-object-click-start' )
          GROUP BY 
               ssot__KnowledgeArticleEngagement__dlm.ssot__IndividualId__c,
               ssot__KnowledgeArticleEngagement__dlm.ssot__KnowledgeArticleVersionId__c
     ) as Table2
          ON 
               Table1.individual_id = Table2.individual_id
     JOIN 
          ssot__KnowledgeArticleVersion__dlm
          ON 
               ssot__KnowledgeArticleVersion__dlm.ssot__Id__c = Table1.knowledgeArticle_id
WHERE 
     Table1.knowledgeArticle_id <> Table2.knowledgeArticle_id
GROUP BY 
     ssot__KnowledgeArticleVersion__dlm.ssot__Id__c,
     Table2.knowledgeArticle_id
