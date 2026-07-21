# SFMC Tips #56 : How to Find Duplicate Records in the Same Field Using SQL

**Source:** https://medium.com/@marketingcloudtips/how-to-find-duplicate-records-in-the-same-field-using-sql-560269365587

---

# SFMC Tips #56 : How to Find Duplicate Records in the Same Field Using SQL

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--560269365587---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--560269365587---------------------------------------)

2 min read

·

Sep 12, 2024

--

Photo by [Sara Rolin](https://unsplash.com/@rolinsndvl?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud, there may be times when you want to investigate whether duplicate records exist in a specific field within a data extension. For example, it’s helpful when you want to check for duplicate email addresses in a data extension.

In such cases, you can easily identify duplicate records by using an SQL query like the one below.

**■ Displaying Duplicate Records (without the duplicates themselves)**

```
SELECT DISTINCT a.[Field_Name]  
FROM [Data_Extension_Name] a  
WHERE (SELECT COUNT(*)  
       FROM [Data_Extension_Name] b  
       WHERE a.[Field_Name] = b.[Field_Name]) >= 2
```

**■ Displaying Duplicate Records (without removing duplicates)**

```
SELECT TOP 10000000 a.[Field_Name]  
FROM [Data_Extension_Name] a  
WHERE (SELECT COUNT(*)  
       FROM [Data_Extension_Name] b  
       WHERE a.[Field_Name] = b.[Field_Name]) >= 2  
ORDER BY a.[Field_Name] ASC
```

**Using the “Upper Query” and “Lower Query”**

- **Upper Query**: This query is ideal for identifying the duplicate records themselves. It’s effective when you want to investigate duplicate data and confirm their existence.
- **Lower Query**: This query doesn’t remove duplicates. Instead, it helps you understand how many times each record is duplicated by counting the number of records retrieved. `DISTINCT TOP` cannot be used in Query Studio.

By effectively using these queries based on your needs, you can efficiently manage data duplication and accurately grasp the necessary information.

Additionally, in Query Studio, you can use the “Find and Replace” feature (Ctrl + “H”) to bulk replace `[Field_Name]` and `[Data_Extension_Name]`, making the process more efficient.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
