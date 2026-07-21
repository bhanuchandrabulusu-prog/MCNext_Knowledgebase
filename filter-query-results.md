# Filter Your Query Results | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/filter-query-results.html

---

A query can return many rows, depending on the amount of data stored in Data 360. You can filter the retrieved rows by using a WHERE clause.

This example shows a field expression in the WHERE clause containing one field. It filters the result set to return only one Individual record with the specified ID value.

This query returns exactly one record that matches the specified ID.

ssot__FirstName__c	ssot__LastName__c	ssot__Salutation__c
Edna	Frank	Ms.

The previous query filters on the ID field. You can add more than one filter condition in the WHERE clause by combining them with the AND and OR logical operators. For example, instead of retrieving only one record, you can retrieve all individuals whose last name is either Frank or Green and whose birth date field isn’t null.

This query output shows sample results.

ssot__Id__c	ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
003Hu00003SELnIIAX	Avi	Green	1937-03-12T00:00:00.000Z
003Hu00003SELnNIAX	Edna	Frank	1945-10-23T00:00:00.000Z

Another possible scenario is that you want to retrieve all the Generation X individuals with birth dates from 1965 through 1980. To specify a date range to filter on, the WHERE clause uses the BETWEEN operator. The BETWEEN operator compares the birth date against a range defined by two values and includes the beginning and ending values. In addition to the BETWEEN operator, this query uses the TIMESTAMP operator to convert the string values to timestamps so that they can be compared.

This query output shows sample results.

ssot__Id__c	ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
003Hu00003SELn6IAH	Rose	Gonzalez	1971-08-13T00:00:00.000Z
003Hu00003SELnMIAX	Liz	D'Cruz	1965-05-18T00:00:00.000Z

Sometimes, you want to search for records based on some character patterns. For example, you want to get all individuals whose first name starts with the letter ‘E’. Use the LIKE operator to compare patterns in string values. Pattern matching is case-sensitive. You can use these symbols in the string pattern.

An underscore (_) stands for any single character.
A percent sign (%) matches any sequence of zero or more characters.

This query returns all individuals whose first name starts with ‘E’. For example, a sample result could include individuals with the first names of Eugena and Edna.

This query output shows sample results. Eugena has no birth date value, so the ssot__BirthDate__c column for Eugena is empty.

ssot__Id__c	ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
003Hu00003SELnNIAX	Edna	Frank	1945-10-23T00:00:00.000Z
00QHu00003W7JISMA3	Eugena	Luce	

This query uses two underscores in the LIKE pattern. It finds all individuals whose first name starts with ‘J’, ends with ‘e’, and is four characters long. A sample result can include individuals with the first names of Jake and Jane.

This query output shows sample results. The two matching records are for Jake and Jane. Jake has no birthdate value, so the ssot__BirthDate__c column for Jake is empty.

ssot__Id__c	ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
003Hu00003SELnPIAX	Jake	Llorrac	
003Hu00003SELnGIAX	Jane	Grey	1947-10-01T00:00:00.000Z

Besides the already discussed LIKE and BETWEEN operators, SQL also supports the commonly known comparison operators:

>
>=
<
<=
=
<>, not equals
!=, an alternative syntax for <>
