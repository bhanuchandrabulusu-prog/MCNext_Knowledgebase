# SFMC Tips #31 : How to Add Records to a Filtered Data Extension

**Source:** https://medium.com/@marketingcloudtips/how-to-add-records-to-a-filtered-data-extension-64857d3fc4ff

---

# SFMC Tips #31 : How to Add Records to a Filtered Data Extension

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--64857d3fc4ff---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--64857d3fc4ff---------------------------------------)

4 min read

·

Feb 29, 2024

--

Photo by [Nastya Dulhiier](https://unsplash.com/@dulhiier?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud’s filtered data extensions allow you to set specific criteria and store records that meet those criteria within the data extension. Once a filtered data extension is created, its records cannot be modified unless the filter criteria themselves are changed.

When you open the tab for filtered data extension records in Email Studio or Contact Builder, you will notice that there is no “Import” button available. Similarly, in Automation Studio’s SQL Query Activity, filtered data extensions cannot be selected as the target data extension.

However, I have discovered a method to add records from another data extension to a filtered data extension. 💡

**The method involves using the “Import Values” feature in Contact Builder**.

Contact Builder’s import functionality allows records to be imported between data extensions, and **this feature lets you select a “filtered data extension” on both the source and target sides**.

### **Key points:**

- **You can combine a filtered DE with a standard DE.**
- **You can also combine two filtered DEs.**

*\*You can overwrite, update, or add records freely.*

**🤔 Question: When is this technique useful?**

**😉 Answer: The filter feature in Email Studio has been unable to perform UNION operations like SQL does, but with this technique, UNION operations become possible.**

*\*As you know, filtered data extensions are designed to contain data that strictly matches the filter criteria. Therefore, this tip deviates from the intended use of filtered data extensions. Using this method might introduce unintended data, which could cause confusion,* ***especially in large organizations where sharing among team members is challenging****. Please use this technique cautiously.*

*Special thanks to* ***Vladimir Silak*** *and* ***Sascha Huwald*** *for pointing out this issue.*

Let’s go through the steps. In this article, we will attempt to merge two filtered data extensions.

First, prepare two filtered data extensions.

- “Filtered\_DE\_100” with 100 records.
- “Filtered\_DE\_50” with 50 records.

\*There are no duplicate records between these data extensions.

Next, navigate to the “Import” tab in Contact Builder and create an import definition. From the dropdown, select “Existing Data Extension” and choose the data extension you want to add records from.

We select “Filtered\_DE\_100” with 100 records. **This shows that you can select a filtered data extension as the source**.

Next, choose the target data extension.

We select “Filtered\_DE\_50” with 50 records. **This demonstrates that you can also select a filtered data extension as the target**.

Now, execute the import with the “Add & Update” action type. Success is achieved if “Filtered\_DE\_50” contains 150 records after the operation.

As shown below, the filtered data extension “Filtered\_DE\_50” now has 150 records. Success!

If you manually refresh the filtered data extension after it contains 150 records…

Naturally, it reverts to the original 50 records. Therefore, be cautious when implementing this in automatically updated data extensions.

The technique introduced this time will prove to be very useful in certain situations. 🕶️💻 Keep it in the back of your mind.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
