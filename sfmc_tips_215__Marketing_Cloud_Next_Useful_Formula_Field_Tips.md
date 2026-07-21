# SFMC Tips #215 : Marketing Cloud Next: Useful Formula Field Tips

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-useful-formula-field-tips-720203a8af53

---

# SFMC Tips #215 : Marketing Cloud Next: Useful Formula Field Tips

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--720203a8af53---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--720203a8af53---------------------------------------)

4 min read

·

Dec 13, 2025

--

Photo by [Martin Widenka](https://unsplash.com/@widenka?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When using **Marketing Cloud Next Growth & Advanced Edition**, there are several **formula field tips** that are helpful to know.  
 In this article, I’ll introduce some of the most commonly used and practical points from real-world use cases.

## Table of Contents

1. Treat Boolean fields as Text
2. Truncate decimal places from numeric fields
3. Adjust date and time values for display

## 1. Treat Boolean Fields as Text

Some data types — such as **Boolean** and **URL** — are **not supported in Marketing Cloud Next content features (within the CMS workspace)**.  
 As a result, even if these fields are connected through the data graph, they may not appear or be usable in the UI.

Examples where this limitation applies:

- Merge fields
- **Expression** components
- **Repeater** components

> *Note: Since segments and data graphs are* ***Data Cloud features****, they can still use these fields without issue. The same applies to* ***Flows****, where these data types work normally.*

In such cases, the standard workaround is to **convert the value into a Text-type formula field**.

## How to do this

1. Create a new **formula field** and set its type to **Text**.
2. Select the target field from the attribute list.
3. Save it **without any additional logic**.

Next, create a corresponding **Text field in the DMO** and map it to this formula field.  
That’s all — your Boolean field can now be used as a Text value.

When using it, you can simply specify `true` or `false`.  
However, **case sensitivity matters**, so be sure to check how the value is stored on the DMO side.

For Boolean values coming from **CRM**, the value is always stored as lowercase `true`.

## 2. Truncate Decimal Places from Numeric Fields

Due to system behavior, numeric values such as `2400` are displayed as `2400.0` in content.

![]()

Unfortunately, this behavior cannot be changed directly.  
However, if this looks awkward for display purposes — such as prices — you can apply the same approach as in section 1: create a **Text-type formula field** and use the following formula.

> *Replace* `Price` *with your actual field name as needed.*

```
IF(  
  LEN(sourceField['Price']) <= 3,  
  sourceField['Price'],  
  
  IF(  
    LEN(sourceField['Price']) <= 6,  
    LEFT(sourceField['Price'], LEN(sourceField['Price']) - 3)  
    + ',' +  
    RIGHT(sourceField['Price'], 3),  
  
    IF(  
      LEN(sourceField['Price']) <= 9,  
      LEFT(sourceField['Price'], LEN(sourceField['Price']) - 6)  
      + ',' +  
      RIGHT(LEFT(sourceField['Price'], LEN(sourceField['Price']) - 3), 3)  
      + ',' +  
      RIGHT(sourceField['Price'], 3),  
      LEFT(sourceField['Price'], LEN(sourceField['Price']) - 9)  
      + ',' +  
      RIGHT(LEFT(sourceField['Price'], LEN(sourceField['Price']) - 6), 3)  
      + ',' +  
      RIGHT(LEFT(sourceField['Price'], LEN(sourceField['Price']) - 3), 3)  
      + ',' +  
      RIGHT(sourceField['Price'], 3)  
    )  
  )  
)
```

> *This formula supports* ***comma-separated formatting up to 999.9 billion****.*

![]()

If you don’t need comma separators, you can simply truncate the decimal portion using a much simpler formula.  
Be sure to set this as a **Text-type formula field** as well.

```
ROUND(sourceField['Price'])
```

## 3. Adjust Date/Time Values for Display

When displaying date and time values in content, you can apply formatting and time zone adjustments in advance.

For example, to display a timestamp in **Japan Standard Time (JST)** as  
 “YYYY年MM月DD日 HH時MM分”, configure a **Text-type formula field** as follows:

```
FORMATDATE(  
  DATEADD('h', 9, sourceField['LastModifiedate']),  
  'yyyy年M月d日 H時m分'  
)
```

## Tip

Datetime values from **CRM** are stored in **UTC**.  
Without time zone conversion, the displayed time in Japan will be **9 hours earlier** than expected.

If CRM contains the following datetime value:

![]()

When the data is synced to Data Cloud, it is stored in UTC — meaning the time appears 9 hours earlier.  
That’s why adding 9 hours is necessary.  
You can see that the value created via the formula field matches the original CRM data.

## Important Note

Extra care is required when displaying **Marketing Cloud Engagement Date fields** (which are effectively treated as Datetime) in Marketing Cloud Next content.

- **MCE system time**: CST (JST − 15 hours)
- **Data Cloud / MC Next system time**: UTC (JST − 9 hours)

This results in a **6-hour difference**.  
 To account for this, apply the following adjustment:

```
FORMATDATE(  
  DATEADD('h', -6, sourceField['LastModifiedate']),  
  'yyyy年M月d日 H時m分'  
)
```

Without this correction, the displayed time will be **6 hours ahead**.

## Conclusion

The techniques introduced here are among the **most frequently used formula field tips** in Marketing Cloud Next.  
If there are other important patterns worth sharing, I’ll add them over time.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
