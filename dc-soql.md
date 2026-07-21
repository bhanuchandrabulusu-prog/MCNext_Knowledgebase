# SOQL With Apex | Query Data in Data 360 | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/dc-soql.html

---

Similar to how you use SOQL to query Salesforce objects, you can also use SOQL to query Data 360 objects, such as DLOs and DMOs, with some limitations. SOQL is Salesforce’s proprietary query language to query Salesforce objects. You can run SOQL in Apex or by using tools such as the Query Editor and SOQL Builder.

To learn about querying DMOs in Apex with SOQL, see Data 360 in Apex in the Apex Developer Guide. Also see Mock SOQL Tests for Data 360 Data Model Objects in the Apex Developer Guide.

SOQL is similar to SQL, but here are a few differences between the two.

SOQL statements can execute in Apex on the Salesforce Platform, and not only using an API.
SOQL doesn’t support the asterisk (*) character to retrieve all fields in the SELECT statement. To retrieve all fields, use the FIELDS(ALL) keyword or retrieve specific fields.
SOQL provides parent and child relationships instead of JOIN statements. These relationships aren’t supported in the current implementation of SOQL in Data 360.

For the SOQL language reference, see Salesforce Object Query Language (SOQL). To learn about the use of SOQL in general with Salesforce objects, see the SOQL for Admins Trailhead module.

See Also

SOQL and SOSL Reference: SOQL Object Limits and Limitations
Apex Developer Guide: SOQL and SOSL Queries
Salesforce Help: Developer Console
Salesforce Extensions for Visual Studio Code: SOQL Builder
Data 360 Object-Specific APIs
