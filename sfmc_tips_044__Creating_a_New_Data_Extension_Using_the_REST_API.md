# SFMC Tips #44 : Creating a New Data Extension Using the REST API

**Source:** https://medium.com/@marketingcloudtips/creating-a-new-data-extension-using-the-rest-api-e83c38213127

---

# SFMC Tips #44 : Creating a New Data Extension Using the REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e83c38213127---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e83c38213127---------------------------------------)

7 min read

·

Jun 9, 2024

--

Photo by [Nikhil Mitra](https://unsplash.com/@nikhilmitra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the Summer ’24 release of Salesforce Marketing Cloud, **a Custom Object REST API was introduced to manage data extensions**.

[## SFMC Tips #42 : Summer ’24 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Summer ’24, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/summer-24-release-highlights-notable-new-features-in-marketing-cloud-0d9ba139c988?source=post_page-----e83c38213127---------------------------------------)

Until now, data extensions in Marketing Cloud were managed using SOAP API or SSJS. **Moving forward, you can easily and quickly manage data extensions using the REST API**.

*As a rough estimate, it took about 1 minute to create a data extension with 100 fields using SSJS, whereas it took only about 3 seconds using the REST API.*

Please refer to the following help document where the ‘use cases’ provided by Salesforce are listed.

[## Salesforce Developers

### Custom Objects

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_objects?meta=Summary&source=post_page-----e83c38213127---------------------------------------)

[## Salesforce Developers

### Data Extension Data

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_object_data?meta=Summary&source=post_page-----e83c38213127---------------------------------------)

## ■ Setting the Stage

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----e83c38213127---------------------------------------)

```
--- METHOD   
POST  
  
--- ENDPOINT  
https://[Authentication Base URL].auth.marketingcloudapis.com/v2/token  
  
--- HEADERS   
Content-Type：application/json  
  
--- BODY  
{  
 "grant_type": "client_credentials",  
 "client_id": "[Client Id]",  
 "client_secret": "[Client Secret]",  
 "account_id": "[MID]"  
}
```

In the **Scope** of this API configuration, the following is required:

**■ DATA — Data Extensions — Write**

\*This is for the example of ‘creating a new data extension’ in this case.

[## Salesforce Developers

### REST API Permission IDs and Scopes

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_rest_permission_scopes/rest-permissions-and-scopes.html?source=post_page-----e83c38213127---------------------------------------)

Now let’s get into the explanation!

## ■ Creating a New Data Extension

When creating a new data extension, the first thing to consider is whether it is sendable or not. Based on this, the body script is divided as follows.

```
--- METHOD   
POST  
  
--- ENDPOINT  
https://[REST Base URL].rest.marketingcloudapis.com/data/v1/customobjects  
  
--- HEADERS   
Content-Type: application/json  
Authorization: Bearer [Access Token]
```

### - Sample Body for a Sendable Data Extension

```
{  
  "name": "NewDE_Sendable",  
  "key": "",  
  "isSendable": true,  
  "sendableCustomObjectField": "Text",  
  "sendableSubscriberField": "_SubscriberKey",  
  "categoryId": 93800,  
  "fields": [  
    { "name": "Text", "type": "Text", "length": 50, "ordinal": 1, "IsPrimaryKey": true, "isNullable": false, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "EmailAddress", "type": "EmailAddress", "length": 254, "ordinal": 2, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Number", "type": "Number", "ordinal": 3, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Date", "type": "Date", "ordinal": 4, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Boolean", "type": "Boolean", "ordinal": 5, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Phone", "type": "Phone", "ordinal": 6, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Decimal", "type": "Decimal", "length": 25, "scale": 1, "ordinal": 7, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Locale", "type": "Locale", "ordinal": 8, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false}  
  ]  
}
```

### - Sample Body for a Non-Sendable Data Extension

```
{  
  "name": "NewDE_Non_Sendable",  
  "key": "",  
  "categoryId": 93800,  
  "fields": [  
    { "name": "Text", "type": "Text", "length": 50, "ordinal": 1, "IsPrimaryKey": true, "isNullable": false, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "EmailAddress", "type": "EmailAddress", "length": 254, "ordinal": 2, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Number", "type": "Number", "ordinal": 3, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Date", "type": "Date", "ordinal": 4, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Boolean", "type": "Boolean", "ordinal": 5, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Phone", "type": "Phone", "ordinal": 6, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Decimal", "type": "Decimal", "length": 25, "scale": 1, "ordinal": 7, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false},  
    { "name": "Locale", "type": "Locale", "ordinal": 8, "IsPrimaryKey": false, "isNullable": true, "isTemplateField": false, "isInheritable": true, "isOverridable": true, "isHidden": false, "isReadOnly": false, "mustOverride": false}  
  ]  
}
```

### Important Points to Note

- The initial `name` is the name of the new data extension.
- The `key` is mandatory but can be left blank to generate a random key.
- **The** `categoryId` **is the ID of the folder where the data extension will be stored**.
- The primary key field must be a required field.
- **Replace** `sendableCustomObjectField` **with your specific sendable key**.
- The `sendableSubscriberField` is fixed as `_SubscriberKey`.
- Fields from `isTemplateField` onwards are required and should not be changed.
- **Upper and lower case are strictly distinguished**.

### How to Find `categoryId`

To find the `categoryId` (folder ID), open any data extension stored in the folder. Click the link in the breadcrumb at the top left to navigate to the folder you want to check.

The `categoryId` will be in the URL, as shown below where the `categoryId` is 93800.

![]()

***Note: If you specify a non-existent*** `categoryId`***, you will not be able to access the created data extension****. If you know how to access it, please leave a comment!*

### Additional Settings

You can also set “data retention policies”. For more details, refer to the link below. My sample bodies provided here are simplified for clarity.

[## Salesforce Developers

### Custom Objects

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_objects?meta=createDataExtension&source=post_page-----e83c38213127---------------------------------------)

### ★★★ Excel Tool (download) ★★★

I created an Excel sheet to simplify building the fields. Use the “Copy & Paste” section in column “H” and paste it into the template below.

![]()

<https://image.s12.sfmc-content.com/lib/fe2c11737164047d721379/m/1/DE_creation_REST_API_Nobuyuki_Watanabe.xlsx>

***Note: After pasting, manually remove “the trailing comma” from the last field.***

### - Template for Sendable Data Extension

```
{  
  "name": "NewDE_Sendable",  
  "key": "",  
  "isSendable": true,  
  "sendableCustomObjectField": "XXXXX",  
  "sendableSubscriberField": "_SubscriberKey",  
  "categoryId": XXXXX,  
  "fields": [  
  
Copy & Paste  
  
  ]  
}
```

### - Template for Non-Sendable Data Extension

```
{  
  "name": "NewDE_Non_Sendable",  
  "key": "",  
  "categoryId": XXXXX,  
  "fields": [  
  
Copy & Paste  
  
  ]  
}
```

That concludes the article on creating data extensions.

*The other day, there was a question about an example of retrieving record values in a data extension, so I am sharing the sample I tried.*

## ■ Retrieving data from a Data Extension

[## Salesforce Developers

### Data Extension Data

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-custom_object_data?meta=Get%2Bdata%2Bby%2Bdata%2Bextension%2Bkey&source=post_page-----e83c38213127---------------------------------------)

In the **Scope** of this API configuration, the following is required:

**■ DATA — Data Extensions — Read**

\*This is for the example of ‘Retrieving data from a Data Extension’.

```
--- Method  
GET  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/data/v1/customobjectdata/key/XXXXXXXXXXXXXXX/rowset?$filter=XXX_Flag%20eq%20'True'  
  
--- Header  
Authorization: Bearer [Access Token]
```

The above example retrieves records where the field name is “XXX\_Flag” and the Boolean value is “True”.

- **The method is GET**, so no body is required.
- **Replace “XXXXXXXXXXXXXXX” with the external key of the data extension**.
- **Up to 2500 records can be retrieved per page**. (Page switching can be handled with the parameter “?$page=2”.)
- **Filtering, sorting, and paging are only supported with sendable data extensions**.
- Requests to retrieve data **from non-sendable data extensions can return a maximum of 200 rows**.
- Refer to the link below for the **“filter operators”** used in the endpoint.

[## Salesforce Developers

### Assets

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_assets/assetSimpleQuery.html?source=post_page-----e83c38213127---------------------------------------)

## ■ Conclusion

I have previously created data extensions with numerous fields using SSJS (Script Activities). Will this REST API feature replace it?

[## SFMC Tips #39 : Efficient Data Extension Creation with Automation Studio Scripting

### Are you manually entering data for a data extension with lots of fields, starting from scratch each time?

medium.com](/@marketingcloudtips/efficient-data-extension-creation-with-automation-studio-scripting-8257c4e9b324?source=post_page-----e83c38213127---------------------------------------)

**One of the benefits of using script activities is that you can leave a trace of the script as a record**. On the other hand, while REST API is convenient, it seems that the code needs to be either discarded after use or managed with tools like Excel or Notepad.

Nonetheless, being able to handle data extensions with REST API comes with many other benefits, so I think it’s a wonderful feature addition.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
