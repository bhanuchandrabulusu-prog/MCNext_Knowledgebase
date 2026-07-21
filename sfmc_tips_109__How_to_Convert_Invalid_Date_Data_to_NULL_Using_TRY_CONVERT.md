# SFMC Tips #109 : How to Convert Invalid Date Data to NULL Using TRY_CONVERT

**Source:** https://medium.com/@marketingcloudtips/how-to-convert-invalid-date-data-to-null-using-try-convert-602dd7df849f

---

# SFMC Tips #109 : How to Convert Invalid Date Data to NULL Using TRY\_CONVERT

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--602dd7df849f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--602dd7df849f---------------------------------------)

1 min read

·

May 2, 2025

--

Photo by [Girl with red hat](https://unsplash.com/@girlwithredhat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When managing customer profiles, some organizations store date information like “Birthday” in three separate numeric fields: “**Year**” (Birth\_Year), “**Month**” (Birth\_Month), and “**Day**” (Birth\_Day).

However, when attempting to combine this data into a single date field, there’s a risk of creating invalid dates — such as February 30th — which can cause **automation errors** in Salesforce Marketing Cloud.

This is where the **TRY\_CONVERT** function comes in handy. This function allows you to convert invalid dates into NULL values, preventing errors.

Here’s how you can use it:

```
CASE    
    WHEN birth_year BETWEEN 1900 AND 2050 THEN    
        TRY_CONVERT(    
            DATE,    
            CONCAT(    
                CONVERT(VARCHAR(4), Birth_Year), '-',    
                RIGHT('00' + CONVERT(VARCHAR(2), Birth_Month), 2), '-',    
                RIGHT('00' + CONVERT(VARCHAR(2), Birth_Day), 2)    
            ),    
            111    
        )    
    ELSE NULL    
END AS [Birth_Date]
```

Sometimes, sharing small SQL tips like this might come in handy for you.

That’s all for today!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
