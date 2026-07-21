# SFMC Tips #239 : Agentforce: Changes to Data Library Retriever Queries

**Source:** https://medium.com/@marketingcloudtips/agentforce-changes-to-data-library-retriever-queries-6be94d2e91fd

---

# SFMC Tips #239 : Agentforce: Changes to Data Library Retriever Queries

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6be94d2e91fd---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6be94d2e91fd---------------------------------------)

4 min read

·

Jan 22, 2026

--

Photo by [Maxence Pira](https://unsplash.com/@maxence_pira?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Since mid-January 2026, if you create a new data library, or if you modify content items of a retriever that uses an old query in an existing data library, you may have noticed that the retriever query is automatically changed to a new format.

**Old query**

**New query**

To conclude first, this is not a bug but expected behavior, and it is a new specification.

## Fixed-Value Query (Old Specification)

The conventional query was, so to speak, a “**fixed-value query**”.  
Because the search conditions and the number of records to retrieve were written directly in the query, it was easy to see at a glance which conditions and which data were being used.

```
SELECT  
    "v"."hybrid_score__c"      AS "Score",  
    "c"."Chunk__c"             AS "Chunk",  
    "c"."SourceRecordId__c"    AS "SourceRecordId",  
    "c"."DataSource__c"        AS "DataSource",  
    "c"."DataSourceObject__c"  AS "DataSourceObject"  
FROM  
    hybrid_search(  
        TABLE("KA_Knowledge_Data_Library_176_index__dlm"),  
        '{!$_SEARCH_STRING}',  
        'Language__c=''{!$_LANGUAGE}''  
         AND KnowledgePublicationStatus__c=''Online''  
         AND DataSource__c IN (''Question2_c__c'', ''Answer2_c__c'')',  
        30  
    ) AS "v"  
INNER JOIN  
    "KA_Knowledge_Data_Library_176_chunk__dlm" AS "c"  
        ON "c"."RecordId__c" = "v"."RecordId__c"  
INNER JOIN  
    "ssot__KnowledgeArticleVersion__dlm" AS "kav"  
        ON "c"."SourceRecordId__c" = "kav"."ssot__Id__c"  
ORDER BY  
    "Score" DESC  
LIMIT 10
```

## Runtime Parameter Query (New Specification)

On the other hand, the new query is a “**runtime parameter**” version.  
The search string, filter conditions, and number of records to retrieve are all replaced with placeholders and are designed to be passed dynamically at runtime.

```
SELECT  
    "v"."hybrid_score__c"      AS "Score",  
    "c"."Chunk__c"             AS "Chunk",  
    "c"."SourceRecordId__c"    AS "SourceRecordId",  
    "c"."DataSource__c"        AS "DataSource",  
    "c"."DataSourceObject__c"  AS "DataSourceObject"  
FROM  
    hybrid_search(  
        TABLE("KA_Knowledge_Data_Library_176_index__dlm"),  
        :"_SEARCH_STRING",  
        :"_PREFILTER_EXPRESSION",  
        :"_NUM_OF_RESULTS"  
    ) AS "v"  
INNER JOIN  
    "KA_Knowledge_Data_Library_176_chunk__dlm" AS "c"  
        ON "c"."RecordId__c" = "v"."RecordId__c"  
INNER JOIN  
    "ssot__KnowledgeArticleVersion__dlm" AS "kav"  
        ON "c"."SourceRecordId__c" = "kav"."ssot__Id__c"  
ORDER BY  
    "Score" DESC  
LIMIT {!$_NUM_OF_RESULTS}
```

This change itself is an improvement that allows the Agent to use optimal search conditions depending on the situation, and as long as the content does not change, there are no functional issues.

## Points That Became Harder to Understand

With the fixed-value query, the conditions were explicitly written as shown below, so it was intuitively clear “which data sources are targeted” and “how many records are retrieved”.

```
hybrid_search(  
    TABLE(KA_Service_Agent_1766068136_index__dlm),  
    '{!$_SEARCH_STRING}',  
    'Language__c=''{!$_LANGUAGE}''  
     AND KnowledgePublicationStatus__c=''Online''  
     AND DataSource__c IN (''Question2_c__c'', ''Answer2_c__c'')',  
    30  
) v
```

In the new specification, all of these are replaced with placeholders, so you can no longer tell the details just by looking at the query.

```
hybrid_search(  
    TABLE("KA_Service_Agent_1766068136_index__dlm"),  
    :"_SEARCH_STRING",  
    :"_PREFILTER_EXPRESSION",  
    :"_NUM_OF_RESULTS"  
) AS v
```

## How to Check the Contents of Placeholders

Therefore, you can check the actual values used at runtime with the following steps.

### Steps

1. Open the retriever detail page (the screen where the query is displayed).

2. Press the F12 key to launch the browser’s built-in “**Developer Tools**”.

3. Select the “**Network**” tab.

4. Click the “**Clear Network Log**” button (the circle icon with a diagonal line) to clear the log once.

![]()

5. Reload the retriever detail page with F5, and data will start flowing in.

6. Enter “**EDC.getRetrieverConfiguration**” in the filter.

![]()

7. One of the displayed items is “**EDC.getRetrieverConfiguration=1**”, so click that one. \*Do not double-click here.

> *Note: Another line is “EDC.getRetrieverConfigurations=1” (with an “s”), which is not the one you want. You can tell which is which by hovering the mouse over them.*

![]()

8. Next, open the “**Response**” tab.

![]()

9. You can then check the settings in the form of the conventional query.

It is hard to read on the screen, so it is better to copy it into a text editor to review.

```
{  
  "placeholderName": ":\"_PREFILTER_EXPRESSION\"",  
  "placeholderType": "NamedParameter",  
  "placeholderDataType": "Text",  
  "placeholderValue": "  
    Language__c = '{!$_LANGUAGE}'  
    AND KnowledgePublicationStatus__c = 'Online'  
    AND DataSource__c IN (  
        'ssot__ArticleNumber__c',  
        'Answer2_c__c',  
        'Question2_c__c'  
    )  
  "  
}
```

10. From this, you can see that ArticleNumber\_\_c, Answer2\_c\_\_c, and Question2\_c\_\_c are being used, and this also matches the settings of the current content items of the data retriever.

## Conclusion

Some of you may have been confused by the sudden change in query format, but this is a specification change to enable more flexible and intelligent searches for the Agent.  
By understanding the mechanism and checking the contents of placeholders as needed, you can respond accordingly.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
