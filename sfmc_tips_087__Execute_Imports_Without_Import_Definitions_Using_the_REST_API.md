# SFMC Tips #87 : Execute Imports Without Import Definitions Using the REST API

**Source:** https://medium.com/@marketingcloudtips/execute-imports-without-import-definitions-using-the-rest-api-c261e04c3d55

---

# SFMC Tips #87 : Execute Imports Without Import Definitions Using the REST API

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c261e04c3d55---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c261e04c3d55---------------------------------------)

5 min read

·

Mar 11, 2025

--

Photo by [Jordan Steranka](https://unsplash.com/@jordansteranka?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud introduced several REST API routes in its Spring ’24 release, significantly enhancing Automation capabilities. These new routes allow one-time imports into Data Extensions without the need to create an import definition in advance.

[## Salesforce Developers

### Data Extension Imports

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc-import_job_api?meta=Summary&source=post_page-----c261e04c3d55---------------------------------------)

## Key Features and Benefits

This functionality enables seamless imports of data stored in external locations directly into Data Extensions, without configuring automation definitions. Supported storage options include:

- Amazon S3
- Google Cloud Storage
- Microsoft Azure Blob Storage
- External SFTP

**Note on Using Salesforce Marketing Cloud’s Dedicated SFTP**  
From my tests, files imported using the SFMC-dedicated SFTP are automatically deleted after a single import. As such, using SFMC SFTP is not recommended unless file deletion is not an issue. Whether the same occurs with external SFTP storage remains unverified.

## Significant Operational Efficiency Gains

This new route is highly beneficial for use cases requiring frequent file updates. For instance, incremental files such as the examples below can be imported efficiently by simply changing the filename:

- `TransactionData_20250301.csv`
- `TransactionData_20250302.csv`
- `TransactionData_20250303.csv`
- `TransactionData_20250304.csv`
- `TransactionData_20250305.csv`  
   ...

When running continuous imports, all requests are processed sequentially, even if a prior import is still running. Pending requests are queued and executed subsequently.

In my experience, importing 30 files (a month’s worth) sequentially took approximately 5 minutes — a remarkable efficiency improvement.

## Enhancements in the Spring ’25 Release

The Spring ’25 new feature release enables the import of **encrypted files** using the “**Asymmetric**” key type through this API, making import operations even more flexible.

With this update, there is no longer a need to transfer and decrypt files before importing them into a Data Extension.

## Preparing to Use REST API for One-Time Imports

### Prerequisites

Before embarking on this journey, ensure you have the following essentials from a previous guide: the “**REST Base URL”** and the all-important “**Access Token”**. If you haven’t obtained them yet, refer to the guide on **“How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend API Tester”**.

[## SFMC Tips #11 : How to Execute Basic Setup for Salesforce Marketing Cloud’s REST API using Talend…

### I often come across examples of executing Salesforce Marketing Cloud’s REST API using POSTMAN. However, I have a…

medium.com](/@marketingcloudtips/how-to-execute-basic-setup-for-salesforce-marketing-clouds-rest-api-using-talend-api-tester-c332b398e970?source=post_page-----c261e04c3d55---------------------------------------)

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

- **AUTOMATION — Automation — Read**
- **AUTOMATION — Automation — Execute**

Refer to: [REST API Permission IDs and Scopes](https://developer.salesforce.com)

### Setting Up the API Request

Use tools like Talend API Tester or Postman to configure the following.

```
--- Method  
POST  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/data/v1/async/import  
  
--- Header  
Content-Type：application/json   
Authorization：Bearer [Access Token]  
  
--- Sample Request Body  
{  
    "source": {  
        "fileInfo": {  
            "specifier": "TransactionData_20250301.csv",  
            "contentType": "CSV",  
            "hasMultipleFiles": false,  
            "standardQuotedStrings": true  
        }  
    },  
    "target": {  
        "type": "DataExtension",  
        "key": "8082AA4B-6E2E-4E93-95AA-2A16B8FB6A88",  
        "updateType": "AddAndUpdate"  
    },  
    "mapping": {  
        "allowErrors": true,  
        "fieldMappingType": "InferFromColumnHeadings"  
    },  
    "transport": {  
        "key": "1DA6211C-1EFE-4F50-82E3-32118B40ACFB"  
    }  
}
```

Customize the request body as follows:

- **source**: File details (e.g., filename).
- **target**: Data Extension details (external key and update type).
- **mapping**: Field mapping details.
- **transport**: External key of the File Location.

## **Detailed Explanation of Each Item**

### 1. Source (Specify Data Source)

**fileInfo:**

- **specifier:** File name (e.g., `TransactionData_20250301.csv`)
- **contentType:** File format (CSV, TAB, etc.)
- **hasMultipleFiles:** Set to `true` if there are multiple files
- **standardQuotedStrings:** Set to `true` to handle quoted strings in a standard way

### 2. Target (Specify Import Destination)

**type:** Specify the destination type (Enter `DataExtension`)

**key:** External key of the target Data Extension

**updateType:**

- **AddAndUpdate:** Add and update records
- **AddAndDoNotUpdate:** Add records only (*no updates will be performed*)
- **UpdateButDoNotAdd:** Update records only (*no additions will be performed*)
- **Overwrite:** Overwrite the existing data

### 3. Mapping (Field Mapping)

**allowErrors:** If set to `true`, the process will not stop even if errors occur

**fieldMappingType:**

- **InferFromColumnHeadings:** Automatically map fields based on column headers
- **MapByOrdinal:** Map fields based on column order

### 4. Transport (File Location)

**key:** External key of the predefined “File Location”

## Verification of Import Results

To verify the import results, a typical Import Activity involves registering an email address to receive notifications. However, when using this API, email registration is not possible, so you will need to retrieve the results using the API.

Once the import request is completed, a response like the following will be returned.

![]()

The `id` displayed here is called the "Task ID" for the import. Make sure to note it down. Next, initiate another request with the following configuration.

```
--- Method  
GET  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/data/v1/async/import/{id}/summary  
  
--- Headers  
Authorization: Bearer [Access Token]
```

Executing this will return information like the following, indicating that one error row occurred during this import.

![]()

## Checking the Error Details

To identify the type of error, configure the following request.

```
--- Method  
GET  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/data/v1/async/import/{id}/validationsummary  
  
--- Headers  
Authorization: Bearer [Access Token]
```

This reveals that there are records missing required fields.

![]()

To further identify the specific records with missing required fields, configure the following request.

```
--- Method  
GET  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/data/v1/async/import/{id}/validationresult  
  
--- Headers  
Authorization: Bearer [Access Token]
```

This will provide the specific records and the names of the problematic fields.

![]()

## Final Thoughts

How did this guide work for you?

The Data Extension Import API offers flexibility and efficiency. By leveraging this feature, you can simplify your import processes and manage data aligned with your business requirements.

Documentation regarding bulk imports and encrypted file imports is expected to be released soon. Once available, I’ll test those features as well.

That’s all for now!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
