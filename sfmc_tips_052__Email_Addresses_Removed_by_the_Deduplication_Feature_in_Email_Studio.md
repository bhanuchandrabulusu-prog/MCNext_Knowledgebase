# SFMC Tips #52 : Email Addresses Removed by the Deduplication Feature in Email Studio

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-52-email-addresses-removed-by-the-deduplication-feature-in-email-studio-a1856b8c5447

---

# SFMC Tips #52 : Email Addresses Removed by the Deduplication Feature in Email Studio

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a1856b8c5447---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a1856b8c5447---------------------------------------)

2 min read

·

Aug 25, 2024

--

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud’s Email Studio offers an optional feature called “**De-duplicate subscribers**” during the audience selection process in the send flow.

![]()

**This feature helps avoid duplicate sends when the same email address appears more than once within the same send list (data extension for sending)**.

\*Similar functionality is available in Automation Studio, but it’s not present in the email activities within Journey Builder. Therefore, you’ll need to remove duplicates beforehand using SQL or other methods.

Have you ever wondered about the following questions related to the “De-duplicate subscribers” feature?

### **Question 1:**

If the same email address is duplicated **within the same data extension**, which subscriber record’s email address will be prioritized for sending? Is it random?

### **Question 2:**

When selecting multiple data extensions, if the same email address is duplicated **across different data extensions**, which email address will be prioritized for sending? Is it random?

Does this make you curious?

Actually, there are specific rules, and here are the answers:

### **Answer 1:**

When there are multiple records with the same email address within the same data extension, the priority is determined as follows:

**・Priority 1:**  
The record with a SubscriberID linked to the Subscriber Key that already exists, and **with the smallest SubscriberID value**.

**・Priority 2:**  
The record with a SubscriberID linked to the Subscriber Key that already exists, and **with the largest SubscriberID value**.

**・Priority 3:**  
The record with a SubscriberID linked to the Subscriber Key that does not yet exist.

Note: **If no records fall under Priority 1 or Priority 2** (i.e., all records in the data extension fall under Priority 3), **then the target records for sending will be selected randomly**.

### **Answer 2:**

When the same email address is duplicated across different data extensions, the subscriber record from **the data extension that is positioned at the top of the audience selection screen** (where multiple data extensions are dragged and dropped) will be prioritized.

## Conclusion

You might have thought that email addresses would be randomly removed, but there are specific rules in place.

By the way, SubscriberID is an automatically assigned ID given by the system when a subscriber is registered. **Therefore, a record with a smaller SubscriberID value typically means an older record**.

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
