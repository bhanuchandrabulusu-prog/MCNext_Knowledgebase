# SFMC Tips #73 : Automating Extract Not Sent and Storing in a Data Extension

**Source:** https://medium.com/@marketingcloudtips/automating-extract-not-sent-and-storing-in-a-data-extension-5d88794a7f76

---

# SFMC Tips #73 : Automating Extract Not Sent and Storing in a Data Extension

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--5d88794a7f76---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--5d88794a7f76---------------------------------------)

7 min read

·

Jan 16, 2025

--

Photo by [Ovi Alam](https://unsplash.com/@ovi___ivo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I explored how to use the “Extract Not Sent” feature in Automation Studio to retrieve information on subscribers who failed to receive emails in Salesforce Marketing Cloud and identify the reasons for the failed sends.

[## SFMC Tips #13 : How to Identify Reasons for Failed Email Sends in Journey Builder

### In cases where email sends fail in the Journey Builder of Salesforce Marketing Cloud, you may want to investigate the…

medium.com](/@marketingcloudtips/how-to-identify-reasons-for-failed-email-sends-in-journey-builder-3731fde54ec5?source=post_page-----5d88794a7f76---------------------------------------)

Through this feature, we could obtain a **CSV file** with data like the one below, using the **Reason** column to determine why the emails were not sent. This method is suitable for quickly investigating data within the last 90 days.

This time, I’ll go a step further and explain how to automate the process of storing this data daily into a Data Extension.

By pre-storing the data in a Data Extension, you can manage information beyond the 90-day limit, access data quickly using SQL, and troubleshoot more effectively. Once set up, the data will accumulate automatically.

Let’s get started!

## Step 1: Create the Storage Data Extension

First, create a Data Extension for storing the extracted data. Set up the following fields:

```
ClientID  
SendID  
SubscriberKey  
EmailAddress  
SubscriberID  
ListID  
EventDate  
EventType  
BatchID  
TriggeredSendExternalKey ※ NULL allowed  
Reason
```

- **EmailAddress Field**: Use the Text type instead of Email Address. When an email cannot be sent due to issues like an invalid email address or List Detective flags, the field might store a **Subscriber Key** instead of an email address.
- **TriggeredSendExternalKey**: Allow NULL values since it remains blank for Email Studio sends.

Below is a script you can execute in a Script Activity to create this Data Extension. Once executed, a “NotSent” Data Extension will be created in the top-level folder. Move it to your desired folder for use.

```
<script runat="server">  
    Platform.Load("Core", "1");  
  
    var dataExtensionConfig = {  
        "CustomerKey": "",  
        "Name": "NotSent",  
        "Fields": [  
            { "Name": "ClientID", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "SendID", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "SubscriberKey", "FieldType": "Text", "MaxLength": 255, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "EmailAddress", "FieldType": "Text", "MaxLength": 255, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "SubscriberID", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "ListID", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "EventDate", "FieldType": "Date", "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "EventType", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "BatchID", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true },  
            { "Name": "TriggeredSendExternalKey", "FieldType": "Text", "MaxLength": 50, "IsRequired": false },  
            { "Name": "Reason", "FieldType": "Text", "MaxLength": 50, "IsPrimaryKey": true, "IsRequired": true }  
        ]  
    };  
  
    var createdDataExtension = DataExtension.Add(dataExtensionConfig);  
</script>
```

This data extension is created using the following technologies.

[## SFMC Tips #39 : Efficient Data Extension Creation with Automation Studio Scripting

### Are you manually entering data for a data extension with lots of fields, starting from scratch each time?

medium.com](/@marketingcloudtips/efficient-data-extension-creation-with-automation-studio-scripting-8257c4e9b324?source=post_page-----5d88794a7f76---------------------------------------)

## Step 2: Configure Automation Studio

**1. Create a New Automation**  
Navigate to Automation Studio and create a new automation.

**2. Drag and Drop the Data Extract Activity**  
Drag and drop the **Data Extract Activity** onto the first step of the automation.

**3. Configure the Data Extract Activity**  
Create a new Data Extract Activity and configure it with the following settings:

- **File Naming Pattern**: Use a pattern such as `*.zip`. Replace the `*` with an appropriate name and ensure the file has a `.zip` extension.
- **Extract Type**: Select **Tracking Extract**. If this option does not appear, contact Salesforce Technical Support to enable this feature.

***Note****: The* ***Tracking Extract*** *type generates a ZIP file and stores it in an SFTP location, so it is crucial to use a* `.zip` *file extension.*

![]()

**4. Set the Extract Conditions**  
Configure the extraction conditions as follows:

- **Date Range**: The maximum retrievable data is for the last **90 days**.
- **Time Zone**: Set it to the time zone of your country. The date of the `EventDate` will follow that time zone. If no setting is made, it will be displayed in the system default time zone, CST.
- **Extract Type**: Check the box for **Extract Not Sent** on the right-hand side.

***Note****: Although the documentation mentions a limit of 2 months for extraction, it is actually possible to retrieve data for up to 90 days.*

**5. Add the File Transfer Activity for Moving Files**  
Drag and drop the **File Transfer Activity** onto the second step of the automation.

**6. Configure File Transfer for Moving Files**

- **Action**: Select **Move a File from Safehouse**.

- **File Naming Pattern**: Ensure the file name matches the pattern used in the **Data Extract Activity**, including the `.zip` extension.
- **Destination**: Choose the FTP directory where the ZIP file will be stored. Use the **Import** directory, as this file will later be imported into the data extension.

![]()

**7. Add the File Transfer Activity for File Decompression**  
Drag and drop another **File Transfer Activity** onto the third step of the automation.

**8. Configure File Transfer for Decompression**

- **File Action**: Select **Manage File**.

- **File Handling**: Configure the activity to decompress the ZIP file. The decompressed file will be placed in the same FTP **Import** directory with a `.csv` extension.

**9. Verify the CSV File**  
After the File Transfer Activity executes, the FTP **Import** directory will contain a file named `NotSent.csv`.

![]()

**10. Import the CSV File into the Data Extension**

- Drag and drop the **Data Copy or Import Activity** onto the fourth step of the automation.

Configure the activity to import the `NotSent.csv` file into the **NotSent** data extension created earlier.

- **Data Action**: Select **Add and Update**.
- **Field Mapping**: Map the columns from the CSV file to the fields in the data extension using the **Header Row**.

**11. Schedule the Automation**  
Add a **Schedule Activity** to automate the process on a daily basis. Activate the automation once all steps are correctly configured.

**12. Test the Automation**  
Run the automation manually once to verify that the data is successfully stored in the data extension.

### **Precautions for the “Extract Not Sent” List**

Below are some points to keep in mind regarding the “Extract Not Sent” list. Please refer to them.

- The list includes email sends from Email Studio and sends from transactional journeys.
- It may take about a day for the latest unsent records to be reflected in the file after the send.
- SendID corresponds to the Job ID. TriggeredSendExternalKey corresponds to the external key for trigger-based sends.
- In the case of a transactional journey, the value in the TriggeredSendExternalKey field will contain the Event Definition Key.
- For one unsent record, subscriber records may be duplicated with different batch IDs. Be cautious if you are trying to verify the “number of undelivered subscribers”.

### **Reasons Why Emails Were Not Sent**

Finally, here are some common reasons why emails were not sent, which can be found in the “Extract Not Sent” list. Please refer to them.

- **Held**  
  The subscriber status is set to “Held” (Undeliverable) in all subscriber lists.
- **Unsubscribed Master**  
  The subscriber status is set to “Unsubscribed” in all subscriber lists.
- **Account Level Opt Out**  
  The subscriber has globally unsubscribed at the account, enterprise, or business unit level. This usually appears redundantly with the “Unsubscribed Master” entry and can generally be ignored.
- **Send Failure**  
  The email failed to send for some reason. The specific cause is not provided.
- **Invalid Email Address**  
  The email address is invalid for some reason.  
  *Example: An address like “abc@yahoo.co”, where the final “m” is missing.*
- **Build Email Error**  
  An error occurred while attempting to build the email.
- **Excluded by Send Time Filter**  
  The subscriber was excluded by a send-time filter script.
- **Domain Exclusion**  
  The email address belongs to a domain excluded by the domain exclusion feature.
- **Suppression List Exclusion**  
  The email address is excluded due to being on the suppression list or automatic suppression list.
- **List Detective Exclusion**  
  The email address is excluded by the List Detective feature.

For other reasons why emails may not have been sent, please refer to the help documentation below.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_es_email_send_error_codes.htm&type=5&source=post_page-----5d88794a7f76---------------------------------------)

Thank you for reading.

### Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
