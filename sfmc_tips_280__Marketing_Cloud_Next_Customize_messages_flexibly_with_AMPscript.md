# SFMC Tips #280 : Marketing Cloud Next: Customize messages flexibly with AMPscript

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-summer-26-ampscript-support-has-arrived-18272b5f6a1e

---

# SFMC Tips #280 : Marketing Cloud Next: Customize messages flexibly with AMPscript

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--18272b5f6a1e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--18272b5f6a1e---------------------------------------)

6 min read

·

Apr 22, 2026

--

Photo by [Nathan Dumlao](https://unsplash.com/@nate_dumlao?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

One of the biggest topics in the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions is undoubtedly the **long-awaited support for AMPscript** (Marketing Cloud’s proprietary scripting language).

This makes it possible to achieve the same flexible message customization on Marketing Cloud Next as was previously available in Marketing Cloud Engagement. It is also a major point of interest for those considering migration from Marketing Cloud Engagement.

**Another important point is that AMPscript can be used not only in the code editor, but also directly within the visual editor**.

The experience of content creation and personalization is likely to change significantly more than ever before.

## AMPscript Functions Available in Marketing Cloud Next

The AMPscript functions available in Marketing Cloud Next have been announced.

Compared to Marketing Cloud Engagement, there are significant limitations, so please refer to the following documentation for details.

<https://developer.salesforce.com/docs/marketing/marketing-cloud-ampscript/references/mc-ampscript-references/mc-ampscript-references.html>

## ① Math (5 Functions)

- **Add()**  
  Adds two numeric values.
- **Subtract()**  
  Subtracts the second numeric value from the first.
- **Multiply()**  
  Multiplies two numeric values.
- **Divide()**  
  Divides the first numeric value by the second.
- **Mod()**  
  Returns the remainder after division.

## ② Date & Time (6 Functions)

- **Now()**  
  Returns the current date and time.
- **DateAdd()**  
  Adds a specified period to a date.
- **DateDiff()**  
  Returns the difference between two dates.
- **DateParse()**  
  Converts a string to a date type.
- **FormatDate()**  
  Converts a date to a specified format.
- **StringToDate()**  
  Converts a string to a date object.

## ③ String (11 Functions)

- **Concat()**  
  Concatenates multiple strings.
- **Length()**  
  Returns the length of a string.
- **Trim()**  
  Removes leading and trailing spaces.
- **Lowercase()**  
  Converts text to lowercase.
- **Uppercase()**  
  Converts text to uppercase.
- **ProperCase()**  
  Capitalizes the first letter of each word.
- **SubString()**  
  Extracts a substring from a specified position.
- **Replace()**  
  Replaces text within a string.
- **ReplaceList()**  
  Replaces multiple strings in a single operation.
- **IndexOf()**  
  Returns the position of a specified string.
- **Format()**  
  Formats a string.

## ④ Utilities (10 Functions)

- **Empty()**  
  Determines whether a value is empty.
- **IsNull()**  
  Determines whether a value is null.
- **Iif()**  
  Returns a value based on a condition.
- **Random()**  
  Returns a random number within a specified range.
- **FormatNumber()**  
  Formats a number using a specified format.
- **FormatCurrency()**  
  Formats a value as currency.
- **Output()**  
  Outputs the result of AMPscript.
- **OutputLine()**  
  Outputs the result of AMPscript with a line break.
- **RaiseError()**  
  Raises an error.
- **v()**  
  Outputs the value of a variable.

## ⑤ Data Access (5 Functions)

- **Lookup()**  
  Retrieves a value from a Marketing Object.
- **Field()**  
  Retrieves a field value from a row.
- **Row()**  
  Retrieves one row from a rowset.
- **RowCount()**  
  Returns the number of rows in a rowset.
- **BuildRowsetFromJson()**  
  Converts JSON into a rowset.

## ⑥ Salesforce (1 Function)

- **RetrieveSalesforceObjects()**  
  Retrieves records from Salesforce objects.

## ⑦ Content (3 Functions)

- **ContentBlockById()**  
  Retrieves a content block by ID.
- **ContentBlockByKey()**  
  Retrieves a content block by key.
- **ContentBlockByName()**  
  Retrieves a content block by name.

At this time, a total of **41 AMPscript functions** have been confirmed to be supported in Marketing Cloud Next.

## AMPscript Functions Not Available in Marketing Cloud Next

Next, here are the AMPscript functions that are currently unavailable.

Understanding the AMPscript functions that are no longer available helps clarify the limitations of Marketing Cloud Next.

## ① Data Extension Operations (17 Functions)

These functions were used to directly access and update Data Extensions.

- ClaimRow()
- ClaimRowValue()
- DataExtensionRowCount()
- DeleteData()
- DeleteDE()
- ExecuteFilter()
- ExecuteFilterOrderedRows()
- InsertData()
- InsertDE()
- LookupOrderedRows()
- LookupOrderedRowsCS()
- LookupRows()
- LookupRowsCS()
- UpdateData()
- UpdateDE()
- UpsertData()
- UpsertDE()

*Lookup() can reference the new Marketing Object.*

## ② CloudPages / Web Form Functions (13 Functions)

CloudPages does not exist in Next.

- CloudPagesURL()
- IsNullDefault()
- LiveContentMicrositeURL()
- MicrositeURL()
- QueryParameter()
- Redirect()
- RequestParameter()
- AuthenticatedEmployeeId()
- AuthenticatedEmployeeNotificationAddress()
- AuthenticatedEmployeeUserName()
- AuthenticatedEnterpriseID()
- AuthenticatedMemberID()
- AuthenticatedMemberName()

## ③ HTTP / External Integration Functions (8 Functions)

API integration with external systems is no longer allowed.

- HttpGet()
- HttpPost()
- HttpPost2()
- IsChtmlBrowser()
- RedirectTo()
- RequestHeader()
- UrlEncode()
- WrapLongURL()

## ④ Salesforce Update Functions (4 Functions)

Read access is allowed, but updates are not.

- CreateSalesforceObject()
- UpdateSingleSalesforceObject()
- LongSfid()
- RetrieveSalesforceJobSources()

## ⑤ SOAP API Functions (9 Functions)

AMPscript is no longer used to invoke APIs directly.

- AddObjectArrayItem()
- CreateObject()
- InvokeCreate()
- InvokeDelete()
- InvokeExecute()
- InvokePerform()
- InvokeRetrieve()
- InvokeUpdate()
- SetObjectProperty()

## ⑥ Encryption and Authentication Functions (8 Functions)

Security processing cannot be performed with AMPscript.

- MD5()
- SHA1()
- SHA256()
- SHA512()
- EncryptSymmetric()
- DecryptSymmetric()
- GetJwt()
- GetJwtByKeyName()

## ⑦ SMS Functions (8 Functions)

SMS-related AMPscript functions are not supported.

- CreateSmsConversation()
- EndSmsConversation()
- MMS\_Content\_URL()
- Msg()
- Noun()
- Nouns
- SetSmsConversationNextKeyword()
- Verb

## ⑧ Dynamics CRM Functions (9 Functions)

Microsoft integrations have been completely removed.

- AddMscrmListMember()
- CreateMscrmRecord()
- DescribeMscrmEntities()
- DescribeMscrmEntityAttributes()
- RetrieveMscrmRecords()
- RetrieveMscrmRecordsFetchXml()
- SetStateMscrmRecord()
- UpdateMscrmRecords()
- UpsertMscrmRecord()

## ⑨ Content Management Functions (16 Functions)

Legacy Content Builder functions are no longer available.

- AttachFile()
- BarcodeUrl()
- BeginImpressionRegion()
- BuildOptionList()
- ContentArea()
- ContentAreaByName()
- EndImpressionRegion()
- GetPortfolioItem()
- Image()
- ImageById()
- ImageByKey()
- TransformXml()
- TreatAsContent()
- TreatAsContentArea()
- WAT()
- WATP()

## ⑩ Social Functions (3 Functions)

- GetPublishedSocialContent()
- GetSocialPublishUrl()
- GetSocialPublishUrlByName()

## ⑪ Contact Operations (1 Function)

- UpsertContact()

## ⑫ Date Conversion Functions (4 Functions)

- DatePart()
- GetSendTime()
- LocalDateToSystemDate()
- SystemDateToLocalDate()

## ⑬ String Processing Functions (5 Functions)

- BuildRowsetFromString()
- BuildRowsetFromXml()
- Char()
- RegExMatch()
- StringToHex()

## ⑭ Other Utility Functions (5 Functions)

- AttributeValue()
- Domain()
- Guid()
- IsEmailAddress()
- IsPhoneNumber()

From this, it is clear that AMPscript in Marketing Cloud Next has been redesigned as a:

**“Personalization display tool”**

rather than a:

**“Data update tool”**

To put it simply, it feels like:

**“A lightweight AMPscript used only to display values in email content.”**

- Next Supported: **41**
- Next Unsupported: **109**
- Total: **150**

As a result, approximately **30% of AMPscript functions are available** in Marketing Cloud Next.

## About Marketing Object

Marketing Objects are containers (data stores) designed to store data used for marketing initiatives.

They serve a role similar to Data Extensions in Marketing Cloud Engagement and allow data to be imported through CSV files. At this time, only manual CSV file imports are supported.

The imported data can then be used for email personalization through AMPscript Lookup functions.

[## SFMC Tips #313 : Marketing Cloud Next: How to Configure Marketing Objects

### Marketing Objects, introduced in the Marketing Cloud Next Growth & Advanced Editions Summer ’26 release, are containers…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-marketing-objects-ec7213fda266?source=post_page-----18272b5f6a1e---------------------------------------)

## **Quick AMPscript Testing**

You can test AMPscript using the following example without connecting to any data source.

- Display the current time

```
%%=Now()=%%
```

*\*The system timezone is UTC.*

- Display Japan time

```
%%=FormatDate(DateAdd(Now(),9,"H"), "yyyy年MM月dd日 HH時mm分")=%%
```

- Display a random number

```
%%=Random(1,100)=%%
```

- Convert a string to uppercase

```
%%=Uppercase("marketing cloud")=%%
```

- Concatenate strings

```
%%=Concat("Hello", " ", "World")=%%
```

- Get string length

```
%%=Length("Salesforce")=%%
```

- Change date format

```
%%=FormatDate(Now(), "yyyy/MM/dd")=%%
```

- Pseudo conditional branching

```
%%=Iif(Random(1,10) > 5, "YES", "NO")=%%
```

When previewed, it is displayed as follows.

For explanations of other AMPscript functions, please refer to the articles by Salesforce MVP Zuzanna Jarczynska-san, where they are covered in detail.

[## Testing AMPscript in Marketing Cloud Next: 35 Functions Confirmed

### Salesforce introduced AMPscript to Marketing Cloud Next during the Summer '26 release, bringing one of the most useful…

sfmarketing.cloud](https://sfmarketing.cloud/2026/07/14/testing-ampscript-in-marketing-cloud-next-35-functions-confirmed/?source=post_page-----18272b5f6a1e---------------------------------------)

## Conclusion

Examples of AMPscript that use data sources (such as Marketing Objects or customer data) are covered in detail in the [following article](/@marketingcloudtips/marketing-cloud-next-how-to-configure-marketing-objects-ec7213fda266).

Once you actually start using it, you may find that there are more limitations than you initially expected. However, there is no doubt that it now enables more advanced personalization and greater flexibility in content creation. With the right ideas and use cases, the possibilities for leveraging this functionality can expand significantly.

Marketing Cloud Next is still an evolving platform overall, with many features continuing to mature. I plan to keep exploring and testing new capabilities while keeping a close eye on future updates and feature releases.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
