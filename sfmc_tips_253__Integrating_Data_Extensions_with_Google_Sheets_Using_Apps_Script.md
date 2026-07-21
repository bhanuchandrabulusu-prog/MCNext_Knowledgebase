# SFMC Tips #253 : Integrating Data Extensions with Google Sheets Using Apps Script

**Source:** https://medium.com/@marketingcloudtips/integrating-data-extensions-with-google-sheets-using-apps-script-7f7c1eb9e1a2

---

# SFMC Tips #253 : Integrating Data Extensions with Google Sheets Using Apps Script

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7f7c1eb9e1a2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7f7c1eb9e1a2---------------------------------------)

8 min read

·

Feb 20, 2026

--

Photo by [Museum of New Zealand Te Papa Tongarewa](https://unsplash.com/@tepapa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I will explain how to automatically integrate records stored in **Data Extensions** in Marketing Cloud Engagement into Google Sheets.

Google Sheets provides a mechanism called **Apps Script (Google Apps Script)**, which allows you to implement processing in a way similar to a “Script Activity” in Automation Studio.

By accessing the Marketing Cloud Engagement REST API from Apps Script, you can retrieve data from a Data Extension and write it into a spreadsheet.

## Prerequisites

First, the following setup is required on the Marketing Cloud Engagement side.

**① Create an Installed Package**

- Create an **Installed Package**
- Configure **API Integration (Server-to-Server)**
- Obtain the **Client ID / Client Secret**

**② Required Scope (Permissions)**

For this use case, since we are retrieving Data Extension records:

- **Data > Data Extensions: Read**

This permission is sufficient.

## Other Required Information

The following information is required when implementing Apps Script:

- Data Extension **External Key**

- Google Sheets **Sheet Name**

## Configuration Steps

In this article, I will explain in detail the steps from creating the Installed Package to calling the Marketing Cloud Engagement API using Apps Script and automatically integrating the data into a spreadsheet.

## Marketing Cloud Engagement Setup

1. From the left menu in Marketing Cloud Setup, select:  
Platform Tools ＞ Apps ＞ **Installed Packages**.

2. Click the **“New”** button in the upper right corner.

3. Enter a package name and save it.  
This package name becomes the definition name for the API integration interface. This time, I named it “**Apps Script**”.

4. Click **“Add Component”.**

5. Select **“API Integration”** and click Next.

![]()

6. Select **“Server-to-Server”** and click Next.

![]()

7. Finally, configure the scope (permissions available via API).  
For this article, check the following and save:

- **Data > Data Extensions: Read**

![]()

8. After saving, the **Client Secret** will be displayed in a popup only once.  
Be sure to make a note of it.

![]()

9. On the next screen, you can obtain the **Client ID** and **Subdomain**, so copy those as well.

10. You should now have noted the following three pieces of information.  
These will be used later in Apps Script, so keep them saved.

- **Client ID**
- **Client Secret**
- **Subdomain (REST Base URI subdomain)**

## Spreadsheet Setup

1. Open the spreadsheet and rename the sheet.

2. In this example, I prepared the following two sheets.  
(They do not need to match the Data Extension name.)

- **“OrderDetail\_1K” (stores 1,000 records)**
- **“OrderDetail\_100K” (stores 100,000 records)**

3. Next, open the “**Extensions**” tab from the menu bar and click **“Apps Script”.**

4. A project named “**Untitled project**” will open. Rename it.  
\*One project is assigned per spreadsheet (not per sheet within the spreadsheet).

5. You will now see the code input screen.  
Delete the existing content and paste the following code.

> *Note: Due to performance considerations, the maximum is set to 100,000 records. Expand as needed.  
> The current code supports overwrite (clear all → rewrite).*

```
// ===== Global settings (declare ONCE) =====  
const MC_SUBDOMAIN = "mcxkknz3m0zj3jqsxn4hm3dp3q-4";  
const MC_CLIENT_ID = "t1onsb1ax48kuv7sc2kvie6s";  
const MC_CLIENT_SECRET = "1HwUFfftSNa6SfTIjyWaq3ow";  
  
const PAGE_SIZE = 2500;  
const MAX_RECORDS_100K = 100000;       // 100,000 records target  
const WRITE_CHUNK_ROWS = 5000;         // write to sheet in chunks  
  
// ===== 5 patterns (edit here) =====  
const PATTERNS_100K = {  
  P1: { deKey: "57EFBC00-1564-409F-8979-6A9F878169E2", sheetName: "OrderDetail_1K" },  
  P2: { deKey: "800851CB-9CE8-44F4-856C-16587AACA5C0", sheetName: "OrderDetail_100K" },  
  P3: { deKey: "YOUR_DE_KEY_3", sheetName: "Sheet_P3" },  
  P4: { deKey: "YOUR_DE_KEY_4", sheetName: "Sheet_P4" },  
  P5: { deKey: "YOUR_DE_KEY_5", sheetName: "Sheet_P5" }  
};  
  
// ===== Core functions =====  
function getAccessToken_() {  
  const url = `https://${MC_SUBDOMAIN}.auth.marketingcloudapis.com/v2/token`;  
  const payload = {  
    grant_type: "client_credentials",  
    client_id: MC_CLIENT_ID,  
    client_secret: MC_CLIENT_SECRET  
  };  
  
  const response = UrlFetchApp.fetch(url, {  
    method: "post",  
    contentType: "application/json",  
    payload: JSON.stringify(payload),  
    muteHttpExceptions: true  
  });  
  
  const body = response.getContentText();  
  if (response.getResponseCode() >= 300) {  
    throw new Error(`Token request failed: ${response.getResponseCode()} / ${body}`);  
  }  
  return JSON.parse(body).access_token;  
}  
  
function fetchRowsetPage_(token, deKey, page) {  
  const url =  
    `https://${MC_SUBDOMAIN}.rest.marketingcloudapis.com/data/v1/customobjectdata/key/` +  
    `${encodeURIComponent(deKey)}/rowset?$page=${page}&$pagesize=${PAGE_SIZE}`;  
  
  const response = UrlFetchApp.fetch(url, {  
    method: "get",  
    headers: { Authorization: `Bearer ${token}` },  
    muteHttpExceptions: true  
  });  
  
  const body = response.getContentText();  
  if (response.getResponseCode() >= 300) {  
    throw new Error(`DE retrieval failed (deKey=${deKey}, page=${page}): ${response.getResponseCode()} / ${body}`);  
  }  
  
  const json = JSON.parse(body);  
  return json.items || [];  
}  
  
function writeRows_(sheet, headers, rowsObj, alreadyWritten) {  
  if (!rowsObj || rowsObj.length === 0) return 0;  
  
  const values = rowsObj.map(obj => headers.map(h => (obj[h] ?? "")));  
  const startRow = 2 + alreadyWritten; // row 1 is header  
  sheet.getRange(startRow, 1, values.length, headers.length).setValues(values);  
  return values.length;  
}  
  
// patternKey: "P1" | "P2" | ...  
function exportPattern100K_(patternKey) {  
  const lock = LockService.getScriptLock();  
  // Wait up to 30 seconds for other executions to finish  
  if (!lock.tryLock(30000)) {  
    throw new Error("Another export is currently running. Try again later or stagger triggers.");  
  }  
  
  try {  
    const pattern = PATTERNS_100K[patternKey];  
    if (!pattern) throw new Error(`Unknown patternKey: ${patternKey}`);  
  
    const token = getAccessToken_();  
  
    const ss = SpreadsheetApp.getActiveSpreadsheet();  
    const sheet = ss.getSheetByName(pattern.sheetName) || ss.insertSheet(pattern.sheetName);  
    sheet.clearContents();  
  
    const maxPages = Math.ceil(MAX_RECORDS_100K / PAGE_SIZE); // 100,000 => 40 pages  
  
    let headers = null;  
    let buffer = [];  
    let writtenRows = 0;  
  
    for (let page = 1; page <= maxPages; page++) {  
      const items = fetchRowsetPage_(token, pattern.deKey, page);  
      if (items.length === 0) break;  
  
      for (const item of items) buffer.push(item.values || {});  
  
      if (!headers && buffer.length > 0) {  
        headers = Object.keys(buffer[0]);  
        sheet.getRange(1, 1, 1, headers.length).setValues([headers]);  
      }  
  
      if (buffer.length >= WRITE_CHUNK_ROWS) {  
        writtenRows += writeRows_(sheet, headers, buffer, writtenRows);  
        buffer = [];  
      }  
  
      if (writtenRows >= MAX_RECORDS_100K) {  
        buffer = [];  
        break;  
      }  
    }  
  
    if (buffer.length > 0) {  
      if (!headers) {  
        headers = Object.keys(buffer[0]);  
        sheet.getRange(1, 1, 1, headers.length).setValues([headers]);  
      }  
      writtenRows += writeRows_(sheet, headers, buffer, writtenRows);  
    }  
  
    Logger.log(`Export completed: pattern=${patternKey}, rows=${writtenRows}, sheet=${pattern.sheetName}`);  
  } finally {  
    lock.releaseLock();  
  }  
}  
  
// ===== Wrapper functions for each pattern (easy to set triggers) =====  
function export_P1_100K() { exportPattern100K_("P1"); }  
function export_P2_100K() { exportPattern100K_("P2"); }  
function export_P3_100K() { exportPattern100K_("P3"); }  
function export_P4_100K() { exportPattern100K_("P4"); }  
function export_P5_100K() { exportPattern100K_("P5"); }
```

## Update the Following Information

Replace the following with your own information:

```
// ===== Global settings (declare ONCE) =====  
const MC_SUBDOMAIN = "mcxkknz3m0zj3jqsxn4hm3dp3q-4";  
const MC_CLIENT_ID = "t1onsb1ax48kuv7sc2kvie6s";  
const MC_CLIENT_SECRET = "1HwUFfftSNa6SfTIjyWaq3ow";
```

- **Subdomain**
- **Client ID**
- **Client Secret**

```
// ===== 5 patterns (edit here) =====  
const PATTERNS_100K = {  
  P1: { deKey: "57EFBC00-1564-409F-8979-6A9F878169E2", sheetName: "OrderDetail_1K" },  
  P2: { deKey: "800851CB-9CE8-44F4-856C-16587AACA5C0", sheetName: "OrderDetail_100K" },  
  P3: { deKey: "YOUR_DE_KEY_3", sheetName: "Sheet_P3" },  
  P4: { deKey: "YOUR_DE_KEY_4", sheetName: "Sheet_P4" },  
  P5: { deKey: "YOUR_DE_KEY_5", sheetName: "Sheet_P5" }  
};
```

Next, for each sheet, set:

- The target Data Extension **External Key**
- The destination spreadsheet **Sheet Name**

> *Note: This sample only prepares up to 5 sheets.  
> If you want to expand to 10 sheets, you can provide this sample code to ChatGPT and request “expand to 10 sheets”, and it can be extended in the same format.*

6. After entering your information, click **Save**.

7. You should now see executable functions.

8. First, execute Sheet 1.

9. Grant access permissions when prompted.

![]()

10. Execution will complete shortly.

11. Check Sheet 1 — the data has been inserted. Success!

12. Return to the Apps Script screen and execute Sheet 2.

13. This may take slightly longer than the first one, but you will see completion.

> *Note: Apps Script must complete within 6 minutes.*

14. Check Sheet 2 — the data has been inserted successfully!

## Setting Up Automation Triggers

So far, this was a manual execution example.  
However, you can automate this like Automation Studio.  
This time, we will try “**Scheduled Execution**”.

1. Select **“Triggers”** from the left menu.

2. Select **“Add Trigger”.**

3. Select the function you want to automate.

4. Since this is scheduled execution, select **“Time-driven”.**

5. Set the execution timing and save.

6. The scheduled execution has now been registered.  
All setup is complete. When the scheduled time arrives, check whether data has been inserted into the sheet.  
\*Schedule each sheet individually.

## Conclusion

Previously, information stored in Data Extensions could only be checked by directly accessing Marketing Cloud.  
By using this approach, users with viewing permission to the spreadsheet can check the data without logging in.

This makes it highly effective for cross-department sharing and simple reporting purposes.

For simplicity, this article demonstrated hard-coding the Client ID and Client Secret.  
If security requirements exist in a production environment, it is recommended to use **PropertiesService** or a similar method to avoid directly writing credentials in the code.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
