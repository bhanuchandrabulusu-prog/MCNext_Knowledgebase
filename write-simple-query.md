# Write a Simple Query | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/write-simple-query.html

---

Let’s start with a simple query. View all individual customer records with a query that selects all fields from ssot__Individual__dlm DMO.

The SELECT clause uses the asterisk (*) wildcard character to get all fields from ssot__Individual__dlm.

To specify a subset of fields to retrieve, list the field names in the SELECT clause. To specify the type of object to retrieve the details from, use the FROM clause.

For example, this query retrieves only the first name, last name, the individual’s ID, and the key qualifier (KQ_Id__c).

This query output shows sample results.

ssot__FirstName__c	ssot__LastName__c	ssot__Id__c	KQ_Id__c
Phyllis	Cotton	00QHu00003W7JIAMA3	CRM
John	Bond	003Hu00003SELnCIAX	CRM
Mike	Braund	00QHu00003W7JICMA3	CRM

What’s the key qualifier (KQ_Id__c)? Data ingested from different data sources can result in records having duplicate IDs. In our example query, the ssot__Id__c column sometimes contains duplicates. The key qualifier, combined with the record ID, uniquely identifies each record. Together, the key ssot__Id__c and the key qualifier KQ_Id__c form the unique, fully qualified key. To make sure that joins in Data 360 are correct, perform all joins on both the Id and the key qualifier columns. See Data Interpretation with Fully Qualified Keys in Salesforce Help.

Now let’s view a calculated insight with its measure field and dimension field.

For example, say we have a calculated insight that computes the number of contact point addresses for each unified individual. The insight has a measure of count1__c and a dimension of ind_id__c, which is the ID of the Individual DMO. The query results for this calculated insight are similar to this output.

count1__c	ind_id__c
1	8608b9f028a77452a4c434ec97ea96bd
2	864d017d1c4b3fe454cc5b8eab6420bc
1	903c9f06924bcb170bf3c896ead0656d
