# Join Records from Different DMOs and DLOs | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/query-joins.html

---

Data resides in various data lake objects (DLOs) and data model objects (DMOs), which this page refers to as DMOs for consistency. To combine customer data stored in separate DMOs, use a join query. A join uses relationships among DMOs based on keys to match a record in one DMO with a corresponding record in another.

For example, the ssot__Individual__dlm DMO contains basic customer information, including first name, last name, and birth date. The customer’s phone number is stored in ssot__ContactPointPhone__dlm, the email in ssot__ContactPointEmail__dlm, and the address in ssot__ContactPointAddress__dlm. To combine this data, use a join query.

Inner join: returns only records with matching field values from both DMOs.
Full outer join: returns all records from both DMOs. Missing values are NULL.
Left outer join: returns all records from the left DMO and matching records from the right DMO. Missing values are NULL.
Right outer join: returns all records from the right DMO and matching records from the left DMO. Missing values are NULL.

To retrieve customer email addresses, use an inner join between ssot__Individual__dlm and ssot__ContactPointEmail__dlm. This retrieves emails by matching Individual records with records in ssot__ContactPointEmail__dlm based on ssot__Id__c and KQ_Id__c. The KQ_Id__c is the fully qualified key that ensures the query can accurately identify the difference between the keys.

This table displays sample query results.

ssot__Id__c	FirstName	LastName	Email
00QHu00003W7JIDMA3	Patricia	Feager	patricia_feager@is.com
00QHu00003W7JIRMA3	Bill	Dadio Jr	bill_dadio@zenith.com
003Hu00003SELnNIAX	Edna	Frank	efrank@genepoint.com

Records with NULL key fields don’t match when you join using =. Use IS NOT DISTINCT FROM instead. In the example, KQ_Id__c uses IS NOT DISTINCT FROM because it can be NULL. For more information about fully qualified keys, see Salesforce Help: Fully Qualified Keys.

This query joins UnifiedIndividual__dlm and UnifiedContactPointEmail__dlm. Unified DMOs lack KQ_Id__c because there are no duplicate record IDs.

The query uses aliases. The AS keyword is optional.

This example joins the Individual DMO with multiple Commerce DMOs (such as the SalesOrder DMO).

To retrieve all records, including non-matching ones, use a full outer join. NULL values indicate missing matches.

This query is similar to the first query for the inner join but, it performs an outer join by using the FULL OUTER JOIN keyword. It joins the ssot__ContactPointEmail__dlm DMO with the ssot__ContactPointEmail__dlm DMO based on the Individual ID value and the fully qualified key (KQ_Id__c), which are in both DMOs. In addition to the matching records, it also returns the non-matching records from each DMO.

This output shows sample query results, which include matching and non-matching records. The row for Janet Lorre has no email value because this record has no corresponding entry in ssot__ContactPointEmail__dlm.

ssot__Id__c	FirstName	LastName	Email
003Hu00003SELnCIAX	John	Bond	bond_john@grandhotels.com
003Hu00003SELnPIAX	Janet	Lorre	
003Hu00003SELnLIAX	Tom	Ripley	tripley@uog.com
