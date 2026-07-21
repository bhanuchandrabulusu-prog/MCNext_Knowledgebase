# SFMC Tips #274 : Data Cloud: Explanation of Segment Operators

**Source:** https://medium.com/@marketingcloudtips/data-cloud-explanation-of-segment-operators-9dce94e06322

---

# SFMC Tips #274 : Data Cloud: Explanation of Segment Operators

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9dce94e06322---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9dce94e06322---------------------------------------)

8 min read

·

Apr 3, 2026

--

Photo by [Nguyen TP Hai](https://unsplash.com/@phonghai649?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Data Cloud (Data 360), when you drag attributes onto the segment canvas, you can select **“operators” depending on the data type**. By accurately understanding these, it becomes possible to precisely narrow down the audience.

Operators are classified into the following four types:

- **Date (Date / DateTime)**
- **Numeric**
- **Text**
- **Boolean**

In this article, I will explain **how each operator functions**.

## Date (Date / DateTime) Operators

These are operators that can be used for **date-type attributes**.

### Important

On this segment screen, **date and time data after timezone conversion is used**. Therefore, the timezone set in the Salesforce organization is applied.

## ① Has No Value

Find audiences where the value of the date-type attribute is **Null**.

## ② Has Value

Find audiences where the value of the date-type attribute is **not Null and has a value**.

## ③ Is On

Find audiences where an event occurred **on the specified date (the day itself)** in the calendar.

## ④ Is Before

Find audiences where an event occurred **before the specified date**. The specified date itself is **not included**.

## ⑤ Is After

Find audiences where an event occurred **after the specified date**. The specified date itself is **not included**.

## ⑥ Is Between

Find audiences where an event occurred from **the start date (00:00:00) to the end date (23:59:59)** specified in the calendar. The specified dates are **included**.

## ⑦ Is Anniversary Of

Find audiences where the **month and day** of the attribute’s date match **today’s month and day**. The **year is ignored**. For example, it extracts people whose birthday is today or whose wedding anniversary is today.

## ⑧ Is Not Anniversary Of

Find audiences where the **month and day** of the attribute’s date do not match today’s month and day. The **year is ignored**.

## ⑨ Greater Than Last Number Of Days

The meaning of “greater” here refers to something **older in time**.

It goes back the specified number of days from today’s date and finds events that occurred **before that date**. The resulting date itself is **not included**.

For example, it can be used when you want to narrow down to only people whose membership date is **more than 180 days ago** (people who have been members for over half a year).

**Example:**  
 When recalculating at any time on November 30, 2025, if you specify **5**, all events before **November 25, 00:00:00** (5 days ago) will be extracted. The data of the 5th day itself is **not included**.

## ⑩ Last Number Of Days

Find audiences where events occurred in the **most recent past X days up to the current time**.

For example, when searching for people who joined within **3 months (90 days)**.

**Example:**  
 Specify **6** and recalculate at **November 30, 2025, 15:00**:

- From: **November 24, 2025, 00:00:00**
- To: **November 30, 2025, 15:00:00**

## Tips

There is no dedicated operator to retrieve **“only X days ago from today”**, but it can be achieved by combining:

- **⑨ Last Number Of Days**
- **⑩ Greater Than Last Number Of Days**

For example, in a case where the segment is recalculated on **November 30**, and you want to retrieve **only the data from 6 days ago (＝ November 24)**:

- **⑨ Last Number Of Days: 6** → data on or after November 24 is retrieved
- **⑩ Greater Than Last Number Of Days: 5** → data on or before November 24 is retrieved

By overlapping these two conditions, the result is narrowed down to **only the data from November 24**.

This technique is also very effective in scenarios such as **“sending an email on the Xth day after the membership date”.**

## ⑪ Next Number Of Days

Find events that will occur from the current time until **the end (23:59:59) of the next X days**.

**Example:**  
 Specify **2** and recalculate at **November 30, 2025, 15:00**:

- From: **November 30, 2025, 15:00**
- To: **December 2, 2025, 23:59:59**

## ⑫ Last Number Of Months

Find audiences where events occurred in the past **X months**.

- The current month is **not included**

**Example:**  
 Specify **2** and recalculate on **November 30, 2025**:

- Target: **September–October 2025**
- November is **not included**

## ⑬ Next Number Of Months

Find audiences where events are scheduled to occur in the next **X months**.

- The current month is **not included**

**Example:**  
 Specify **1** and recalculate on **November 30, 2025**:

- Target: **December 2025 (next month)**
- The current month is **not included**

## ⑭ Last Year

Find audiences where events occurred in **the entire previous year**.

## ⑮ This Year

Find audiences where events occurred in **the entire current year**.

## ⑯ Next Year

Find audiences where events will occur in **the entire next year**.

## ⑰ Day Of Week

Find audiences where events occurred on the specified **day of the week**.

## ⑱ Day Of Month

Find audiences where events occurred on the specified **day (1–31)**.

## ⑲ Not Day Of Month

Find audiences where events occurred on days **other than the specified day (1–31)**.

## ⑳ Before Day Of Month

This operator compares **only the “day” part of the date**.

- It does not compare the month or year
- It uses only the **day of the date**

**Example:**  
 Before Day Of Month = **10**

- Only records with dates from **the 1st to the 9th** are targeted
- The month and year are ignored

## ㉑ After Day Of Month

This operator compares **only the “day” part of the date**.

- It does not compare the month or year
- It uses only the **day of the date**

**Example:**  
 After Day Of Month = **10**

- Only records with dates from **the 11th to the 31st** are targeted
- The month and year are ignored

※ As a result, **data for the 10th is not included** in either ⑳ or ㉑.

## ㉒ Month Of The Year

Find audiences where events occurred in the specified **month (1–12)**.

## ㉓ Not Month Of The Year

Find audiences where events occurred **outside the specified month (1–12)**.

## ㉔ Is This Month

Find audiences where events occurred **this month**.

## ㉕ Is Next Month

Find audiences where events are scheduled to occur **next month**.

## ㉖ Is Last Month

Find audiences where events occurred **last month**.

## ㉗ Is Today

Find audiences where events occurred **today**.

## ㉘ Is Tomorrow

Find audiences where events are scheduled to occur **tomorrow**.

## ㉙ Is Yesterday

Find audiences where events occurred **yesterday**.

## ㉚ Last Number Of Years

*※ This operator is* ***only available for Calculated Insights****.*

Find audiences where events occurred in a past **calendar year (X years ago)**.

**Example:**  
 If the segment is recalculated in **2025** and **5** is specified:

- All events from **January 2020 to December 2020** are returned

## Numeric Operators

These are operators that can be used for **numeric-type attributes**. Percentage types are also included.

## ① Has Value

Find audiences where the value is **not Null or empty**.

## ② Has No Value

Find audiences where the value is **Null or empty**.

## ③ Is Equal To

Find audiences where the value **matches the specified value**.

## ④ Is Not Equal To

Find audiences where the value **does not match the specified value**.

※ If the target field is **Null**, it is not included in the segment.  
 If you want to include Null, put **“Has No Value” and “Is Not Equal To” in an OR block**.

## ⑤ Is Less Than

Find audiences where the value is **less than the specified value**.

## ⑥ Is Less Than or Equal To

Find audiences where the value is **less than or equal to the specified value**.

## ⑦ Is Greater Than

Find audiences where the value is **greater than the specified value**.

## ⑧ Is Greater Than or Equal To

Find audiences where the value is **greater than or equal to the specified value**.

## ⑨ Is Between

Find audiences where the value is **within the specified range (start value to end value)**.

## ⑩ Is Not Between

Find audiences where the value is **outside the specified range**.

## Text Operators

URLs, emails, and phone numbers are also treated as **text-type**.  
*※* ***Case is not distinguished****.*

## ① Has Value

Find audiences where the value is **not Null or empty**.

## ② Has No Value

Find audiences where the value is **Null or empty**.

## ③ Is Equal To

Find audiences where the value **matches the specified string**.

## ④ Is Not Equal To

Find audiences where the value **does not match the specified string**.

※ If the target field is **Null**, it is not included in the segment.  
If you want to include Null, put **“Has No Value” and “Is Not Equal To” in an OR block**.

## ⑤ Contains

Find audiences where the value **contains the specified string**.

## ⑥ Does Not Contain

Find audiences where the value **does not contain the specified string**.

## ⑦ Matches

Find audiences where the value **matches a regular expression pattern**.

For example, if you want to check whether the value contains **TestSearch**, using a regular expression will return **all data that contains TestSearch**.

**Example:**

- TestSearch Results
- TestingSearching (⇒ partial matches such as Test(ing)Search(ing) are also included)

In this way, not only exact matches but also **values that partially contain the string** can be searched together. This is a useful point of the regular expression operator.

## ⑧ Doesn’t Match

Find audiences where the value **does not match a regular expression pattern**.

## ⑨ Begins With

Find audiences where the value **starts with the specified string**.

## ⑩ Exists As A Whole Word

Determine whether the specified string exists **as a whole word**.

**Example:**  
In “hello world”:

- “hello” exists
- “hel” does not exist

## ⑪ Is Not In

Find audiences where the value **does not match any of the specified multiple values**.

- Up to **100 values** can be specified
- If “Value Suggestions” is enabled, you can select from a dropdown
- Comma-separated input is also possible

Example:  
alpha,beta,gamma,delta,echo,foxtrot,golf,hotel,india,juliet,kilo,lima,mike,november,oscar,papa,quebec,romeo,sierra,tango,uniform,victor,whiskey,xray,yankee,zulu,apple,banana,cherry,date,elderberry,fig,grape,honeydew,ice,juice,kiwi,lemon,mango,nectarine,orange,peach,quince,raspberry,strawberry,tomato,ugli,vanilla,watermelon,xenon,yogurt,zephyr,cloud,storm,rain,snow,wind,sky,river,lake,forest,mountain,valley,desert,ocean,beach

## ⑫ Is In

Find audiences where the value **matches any of the specified multiple values**.

- Up to **100 values** can be specified
- If “Value Suggestions” is enabled, you can select from a dropdown
- Comma-separated input is also possible

## Boolean Operators

## ① Has Value

Find audiences where the value is **not Null**.

## ② Has No Value

Find audiences where the value is **Null**.

## ③ Is True

Find audiences where the value is **not Null and True**.

## ④ Is False

Find audiences where the value is **not Null and False**.

## Summary

For example, it is not possible to directly retrieve **“the past 6 months from today”**, so it is necessary to convert it into days such as **“past 180 days”** and specify it. There are some areas where it does not fully meet expectations, so please be careful.

Data Cloud segmentation operators are **rich and deep functions depending on the data type**. By understanding **which records each operator targets**, it becomes possible to build more accurate audience segments.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
