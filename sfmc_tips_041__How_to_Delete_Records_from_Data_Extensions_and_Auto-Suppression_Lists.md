# SFMC Tips #41 : How to Delete Records from Data Extensions and Auto-Suppression Lists

**Source:** https://medium.com/@marketingcloudtips/how-to-delete-records-from-data-extensions-and-auto-suppression-lists-8bf0d5639a44

---

# SFMC Tips #41 : How to Delete Records from Data Extensions and Auto-Suppression Lists

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8bf0d5639a44---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8bf0d5639a44---------------------------------------)

4 min read

·

May 26, 2024

--

Photo by [Fahrul Azmi](https://unsplash.com/@fahrulazmi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When managing records in Salesforce Marketing Cloud, you might encounter situations where **you need to delete specific records from a data extension**. Here’s how you can handle it.

One approach could be to export all records from the data extension, remove the specific records you don’t need, and then re-import the cleaned data.

However, due to security concerns, you might not be able to export data containing personal information to your local environment. Additionally, some data, like Auto-Suppression Lists, cannot be exported at all.

In such cases, **you can use the Script Activity in Automation Studio to partially delete records from a data extension**.

Let’s explore the process for deleting single and multiple records.

## ■ Deleting a Single Record

To delete a record, use the `DeleteData` function.

[## Salesforce Developers

### Deletes information from a data extension as indicated by the array containing the listed column name and value pairs…

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_platformDataExtensionDeleteData.html?source=post_page-----8bf0d5639a44---------------------------------------)

In the script below, specify the “data extension name”, “field name”, and “value”, then execute it once in Automation Studio:

```
<script runat="server">  
    var rows = Platform.Function.DeleteData('DataExtensionName', ['FieldName'], ['Value']);  
</script>
```

- Multiple pairs of “field name” and “value” can be included in one call, but even if there is only one pair, do not remove the brackets [ ].

**For Auto-Suppression Lists, which are treated as data extensions, the above script also works**. **Auto-Suppression Lists manage “email addresses” instead of subscriber keys**. To specify an email address, use the following format:

```
<script runat="server">  
    var rows = Platform.Function.DeleteData('AutoSuppressionList_Name', ['Email Address'], ['xxx@gmail.com']);  
</script>
```

- **Ensure there is a space between “Email” and “Address**”.

## ■ Bulk Deletion of Multiple Records

To delete multiple records at once, you can add a boolean field for deletion purposes, set it to “True” for the records you want to delete, and then delete records where this field is “True”.

First, create a data extension with a boolean field such as “DeleteFlag”.

Next, prepare a CSV file for import to update the “DeleteFlag” for the records you wish to delete (e.g., those with odd IDs).

![]()

After importing the CSV:

Run the following script against this data extension:

```
<script runat="server">  
    var rows = Platform.Function.DeleteData('DeleteExtension', ['DeleteFlag'], ['True']);  
</script>
```

This will delete records with odd IDs from the data extension, as shown in the example below:

**You can also add fields to an auto-suppression list**. Add a boolean field similarly and set its default value to “False”.

Then, **use the Import Activity in Automation Studio to import the “True” values using “Email Address” as the key**. This enables deletion using the same method.

**When importing, remember that “Date Added” is also a required field in addition to “Email Address”**, so ensure your CSV includes this information.

![]()

```
<script runat="server">  
    var rows = Platform.Function.DeleteData('AutoSuppressionList_Name', ['Flag'], ['True']);  
</script>
```

## ■ Conclusion

By understanding and utilizing these methods, you can more flexibly control the records within your data extensions. Give it a try and see how it improves your data management processes in Salesforce Marketing Cloud.

Thank you for reading.

### Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
