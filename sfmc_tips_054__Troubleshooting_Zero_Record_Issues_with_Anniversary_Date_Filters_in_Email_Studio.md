# SFMC Tips #54 : Troubleshooting Zero Record Issues with Anniversary Date Filters in Email Studio

**Source:** https://medium.com/@marketingcloudtips/troubleshooting-zero-record-issues-with-anniversary-date-filters-in-salesforce-marketing-cloud-4dfb45b1f9e3

---

# SFMC Tips #54 : Troubleshooting Zero Record Issues with Anniversary Date Filters in Email Studio

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4dfb45b1f9e3---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4dfb45b1f9e3---------------------------------------)

2 min read

·

Sep 8, 2024

--

Photo by [Lidya Nada](https://unsplash.com/@lidyanada?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud’s Email Studio provides a useful filter function for creating lists from the master list.

Among these filters, the “Anniversary Date” calculation allows you to extract records based on specific dates like birthdays. This calculation ignores the “year” value, so, for instance, if you extract people with a birthday of March 1, 2000, it will return all records with a March 1 birthday, regardless of the year, from the data extension.

However, there are instances where the filter function in Email Studio returns zero records when using the Anniversary Date.

**This issue can occur when trying to extract records for dates spanning from December 1 to January 31**.

**Extracting records with an Anniversary Date condition that spans the end of the year and the beginning of the year is not supported by Email Studio**.

While extraction works fine for the two-month period from November 1 to December 31, it does not function correctly for the two-month span from December 1 to January 31.

To address this issue, you can use the following configuration:

1. **Connect December and January with an “OR” condition**  
   Specifically, set up the conditions for December and January to be connected with an “OR” operator.
2. **Set December 31 and January 1 individually**  
   Since the Email Studio filter function does not support date conditions including “on the day of”, December 31 and January 1 need to be set individually.

Although this requires a bit of extra effort, it enables accurate extraction. Be sure to keep this in mind for future reference.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
