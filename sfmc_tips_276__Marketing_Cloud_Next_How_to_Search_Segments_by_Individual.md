# SFMC Tips #276 : Marketing Cloud Next: How to Search Segments by Individual

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-search-segments-by-individual-137deb00519a

---

# SFMC Tips #276 : Marketing Cloud Next: How to Search Segments by Individual

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--137deb00519a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--137deb00519a---------------------------------------)

7 min read

·

Apr 12, 2026

--

Photo by [Rohit Choudhari](https://unsplash.com/@iamrohitchoudhari?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Edition, there are many practical situations where **you need to check which segments a specific individual belongs to**.

For this purpose, the following features have been officially provided:

- [Segment Preview Feature](/p/be716460c70f)
- [Segment Member Verification Agent](/p/18f64f4f22ba)

However, **using queries is a more effective approach for performing searches efficiently**. In this article, I will introduce two methods I actually use in practice to search segments.

## 1. How to Search Using “Query Editor”

First, this is the simplest method.  
Use the Query Editor to search directly on the screen.

### Steps

1. Open the **Query Editor** tab.

2. Paste and execute the following query.

```
SELECT  
    a.Id__c AS UnifiedId,  
    c.ssot__ExternalRecordId__c AS Id,  
    c.ssot__FirstName__c AS FirstName,  
    c.ssot__LastName__c AS LastName,  
    d.ssot__EmailAddress__c AS CurrentEmail,  
    b.ssot__Name__c AS SegmentName,  
    a.Delta_Type__c AS DeltaType,  
    a.Timestamp__c + interval '9 hour' AS PublishDateTime  
FROM Individual_Unified_SM_1755567709613__dlm a /* ← Change to your Unified Individual - Latest DMO API name */  
JOIN ssot__MarketSegment__dlm b  
    ON a.Segment_Id__c = SUBSTRING(b.ssot__Id__c, 1, 15)  
JOIN UnifiedIndividual__dlm c /* ← Change to your Unified Individual DMO API name */  
    ON a.Id__c = c.ssot__Id__c  
LEFT JOIN ssot__ContactPointEmail__dlm d  
    ON c.ssot__ExternalRecordId__c = d.ssot__PartyId__c  
-- WHERE b.ssot__Name__c = '***' /*Segment Name Filter*/  
-- WHERE c.ssot__ExternalRecordId__c = '***' /*Individual ID Filter*/  
-- WHERE c.ssot__FirstName__c = '***' AND c.ssot__LastName__c = '***' /*Full Name Filter*/  
ORDER BY a.Timestamp__c DESC, a.Delta_Type__c DESC  
LIMIT 10
```

### Points That Require Changes

The following parts must be modified according to your environment:

- **Unified Individual — Latest DMO**  
  → Adjust the numeric portion (e.g., 1755567709613) to match your environment
- **Unified Individual DMO**  
  → Adjust according to your rule set ID  
  (If the rule set ID is blank, no change is required)
- **Timestamp\_\_c + interval ‘9 hour’ AS PublishDateTime**→ Since it is currently set to the Japan time zone, adjust it to your own time zone.

### About Search Conditions

By removing the comment-out (`--`) in the WHERE clause, you can filter by:

- **Segment Name** (not API name)
- **Individual ID** (such as Contact ID or Lead ID)
- **Full Name** (if not searching by full name, remove one side)

### Information You Can Retrieve

This query allows you to retrieve the following information:

- **Unified Individual ID**
- **Segment Name**
- **Email Address**
- **Segment Publish DateTime**
- **New/Existing Indicator (Delta Type)**

By executing this, you can identify which segments the target individual currently belongs to.

## 2. How to Search Using a “Spreadsheet”

If you want to search multiple individuals in bulk or share the results with others for analysis, using a spreadsheet is effective.

In this method, you use Google Apps Script to directly retrieve data from Data Cloud. Please refer to the following article for the basic setup.

[## SFMC Tips #254 : Marketing Cloud Next: Exporting Data to Google Sheets

### Since the article I wrote previously about automatically integrating Data Extension data in Marketing Cloud Engagement…

medium.com](/@marketingcloudtips/marketing-cloud-next-exporting-data-to-google-sheets-cb672a47228a?source=post_page-----137deb00519a---------------------------------------)

For the implementation code, please refer to the following.

```
const SF_LOGIN_URL = "https://login.salesforce.com"; // Sandbox: https://test.salesforce.com  
const CLIENT_ID = "3MVG9GIRg253.lotxyT7qsSZdhj8gAEDPVk6.9Z4NsPAuxUAfTfanzFuk3MV4iTm22RhAYt_rxlIC4hyLKIL";  
const USERNAME = "admin@rbacompany.com";  
const API_VERSION = "66.0";  
  
const PRIVATE_KEY_PEM = `-----BEGIN PRIVATE KEY-----  
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCtTcj7mjX2Kguo  
ahVavRHq+cr+35h3b7jBarCzdlaoJZoayVI6I/NNZzMSMcR+DGhfVG0xXOHubQ2q  
kO6K+FSlMj/wyi2alpq7hS6CCoYwimfuPI4+CnNrVIQiksMe026kXmZ8tEpW6yV5  
lGmC/85p99bE8Pm0CgnlNcsfflx7gYtum9nAVzyu4cqJjYEdSudXh4eSnse0C0Tw  
dWs27aMOz9+7/7QX6QxdgSwkoorkR7KplSE8qrxAoVxPQomzP2ITetaHExbRh+LH  
qC8/wzLo/1uQuFi6v9sp3O6DIcv+K7fNg56o3ATCM27Xt7sFPS+sqIU7LW7mhMja  
CCPs64irAgMBAAECggEAERqQL2S01qqno+N0YBQw5IPqqOTgY0k/brdc4RlYzBeJ  
8gLUfrB1nroErFMFFXucAWyPqkOEeMeChcbwA/8mO3eOH/GUNqGOe9tVD7iCLeA7  
CaQoVa8qXPlmYRMi9rPfQ5Gdg8k3XQSwGiOvliIw+Pxg0ecGfeJPv7NjbKRH9FhX  
FZ0h8v67VPmKIAmRvEfOBV2G8Qp6vIWwS+bCGHspUtqzeIdPDbWbqjSsiddEGqeD  
/pDpvcseMIclaKzY0za0DeR9x2iDTnJPIQ/BxE55RAO/vnkjyo/1Wn0UcGe5E5KE  
3lOFe0gpFObtmHqPaQnO25xJ6EjlmJHFZ9mRmjhYoQKBgQDZccMNagVRJW7WOz/H  
A2D3LFVXQ1247ArD4CA9P3BFNJF2GCLMs3vOOGXKCbnVssW892s9zv6DAoFsbuka  
om4vwocBPXuTrqdnIy0K8IuwQnOzGMyHskO629m46WOG0FfdvG4PMOvwZ8HvkQQJ  
QG7e4eAJNlPbkAvSfD+Hz0TTXQKBgQDMCGU+Ui1BrGcduQWfRbT4Cc8Rz5f7qhAl  
LS8arp0d+HtF5AeqjtRpX4NKGX3sr9xBIZVfwla7jWOe0x6jd20Co5KjlGKvWR2w  
i6tRHGMk0/FOxcdQVR7hWw5+DSaLBmwi3AhE8ro8rqsGqVPqnutzP9BXG7Hr8BDe  
jfPucxDTpwKBgQCX5kbSGhw4waOZ+K3nAs88HDZJzX+tbQdgKjObVbPCRKTREK9O  
vJtiRjelWgH97PMBvP2nofBd6OQssZYZyxqaNpRFI4QueLXs8L/Igp2ytdlJZauL  
p9Z0tJx19mRWizi2Z6mi5xQLTxBFoNJm/CH3hWcSSGdwXEJF+hIPd5Wm6QKBgBMe  
UkZVsvHtcrghRzqWcI+xc5rKpgYp+FtTcY+Bfy14xCxXYrSDr7mz/nxqCRetnujn  
ebTAZBos9IHEbKGKpkdSBoKXe+vMYPDTFZmDHHMt/PWRqMyJPVyGiMQc/ViXoHhf  
v9KeH/9hqpr0MO3SOGPTPfV7nd9q3lnMWWgllhUPAoGAesQ2ItKlppmOG7mnLmz8  
9x5nxc3jJIktMusIQ0WxGnXdZDMTBfIsdZ1eCd7UbX4qfUXq8+JaYMEZ2z7GdJ8n  
y6UZ9hdEw61n7UxekFLUNLST7d/JnShaOdPmmX9oDoQuFEJvgGGRflQqBFoX5bsK  
xY53m5DJwquL0JUzzQZ9M=  
-----END PRIVATE KEY-----`;  
  
const SHEET_NAME = "Data_Cloud_Query";  
const LIMIT_ROWS = 100000;  
  
function run_DataCloudQuery_JWT_toSheets() {  
  const token = getAccessTokenByJwt_();  
  const accessToken = token.access_token;  
  const instanceUrl = token.instance_url;  
  
  const sql = `  
  
SELECT  
    a.Id__c AS UnifiedId,  
    c.ssot__ExternalRecordId__c AS Id,  
    c.ssot__FirstName__c AS FirstName,  
    c.ssot__LastName__c AS LastName,  
    d.ssot__EmailAddress__c AS CurrentEmail,  
    b.ssot__Name__c AS SegmentName,  
    a.Delta_Type__c AS DeltaType,  
    a.Timestamp__c + interval '9 hour' AS PublishDateTime  
FROM Individual_Unified_SM_1755567709613__dlm a /* ← Change to your Unified Individual - Latest DMO API name */  
JOIN ssot__MarketSegment__dlm b  
    ON a.Segment_Id__c = SUBSTRING(b.ssot__Id__c, 1, 15)  
JOIN UnifiedIndividual__dlm c /* ← Change to your Unified Individual DMO API name */  
    ON a.Id__c = c.ssot__Id__c  
LEFT JOIN ssot__ContactPointEmail__dlm d  
    ON c.ssot__ExternalRecordId__c = d.ssot__PartyId__c  
-- WHERE b.ssot__Name__c = '***' /*Segment Name Filter*/  
-- WHERE c.ssot__ExternalRecordId__c = '***' /*Individual ID Filter*/  
-- WHERE c.ssot__FirstName__c = '***' AND c.ssot__LastName__c = '***' /*Full Name Filter*/  
ORDER BY a.Timestamp__c DESC, a.Delta_Type__c DESC  
  
LIMIT ${LIMIT_ROWS}  
`.trim();  
  
  const body = postSqlSync_(instanceUrl, accessToken, sql);  
  
  const headers = extractSelectHeaders_(sql);  
  
  writeDataCloudResultToSheet_(SHEET_NAME, body, headers);  
}  
  
function getAccessTokenByJwt_() {  
  const now = Math.floor(Date.now() / 1000);  
  const jwtPayload = {  
    iss: CLIENT_ID,  
    sub: USERNAME,  
    aud: SF_LOGIN_URL,  
    exp: now + 180  
  };  
  
  const assertion = buildJwtRs256_(jwtPayload, PRIVATE_KEY_PEM);  
  
  const url = `${SF_LOGIN_URL}/services/oauth2/token`;  
  const res = UrlFetchApp.fetch(url, {  
    method: "post",  
    payload: {  
      grant_type: "urn:ietf:params:oauth:grant-type:jwt-bearer",  
      assertion  
    },  
    muteHttpExceptions: true  
  });  
  
  const code = res.getResponseCode();  
  const text = res.getContentText();  
  
  Logger.log("=== JWT token ===");  
  Logger.log("HTTP: " + code);  
  Logger.log("Body(first 2000): " + (text ? text.slice(0, 2000) : ""));  
  
  if (code >= 300) throw new Error(`JWT token failed: HTTP ${code} / ${text}`);  
  
  const obj = JSON.parse(text);  
  if (!obj.access_token || !obj.instance_url) {  
    throw new Error("Token response missing access_token/instance_url: " + text);  
  }  
  return obj;  
}  
  
function buildJwtRs256_(payloadObj, privateKeyPem) {  
  const header = { alg: "RS256", typ: "JWT" };  
  const encHeader = base64UrlEncode_(JSON.stringify(header));  
  const encPayload = base64UrlEncode_(JSON.stringify(payloadObj));  
  const signingInput = `${encHeader}.${encPayload}`;  
  
  const signatureBytes = Utilities.computeRsaSha256Signature(signingInput, privateKeyPem);  
  const encSig = base64UrlEncodeBytes_(signatureBytes);  
  
  return `${signingInput}.${encSig}`;  
}  
  
function base64UrlEncode_(str) {  
  return base64UrlEncodeBytes_(Utilities.newBlob(str).getBytes());  
}  
  
function base64UrlEncodeBytes_(bytes) {  
  const b64 = Utilities.base64Encode(bytes);  
  return b64.replace(/\+/g, "-").replace(/\//g, "_").replace(/=+$/g, "");  
}  
  
function postSqlSync_(instanceUrl, accessToken, sql) {  
  const url = `${instanceUrl}/services/data/v${API_VERSION}/ssot/query-sql`;  
  
  const res = UrlFetchApp.fetch(url, {  
    method: "post",  
    contentType: "application/json",  
    headers: { Authorization: `Bearer ${accessToken}` },  
    payload: JSON.stringify({ sql }),  
    muteHttpExceptions: true  
  });  
  
  const code = res.getResponseCode();  
  const text = res.getContentText();  
  
  Logger.log("=== Data Cloud query ===");  
  Logger.log("HTTP: " + code);  
  Logger.log("Body(first 2000): " + (text ? text.slice(0, 2000) : ""));  
  
  if (code >= 300) throw new Error(`Query failed: HTTP ${code} / ${text}`);  
  
  const obj = JSON.parse(text);  
  if (!obj.data) throw new Error("No data in response (unexpected format): " + text.slice(0, 2000));  
  return obj;  
}  
  
function extractSelectHeaders_(sql) {  
  const cleaned = stripSqlComments_(sql).trim();  
  
  const m = cleaned.match(/\bselect\b([\s\S]*?)\bfrom\b/i);  
  if (!m) return null;  
  
  const selectPart = m[1].trim();  
  if (selectPart === "*" || /\*/.test(selectPart)) return null;  
  
  const items = splitByCommaOutsideParens_(selectPart);  
  
  const headers = items.map(expr => headerFromSelectItem_(expr)).filter(Boolean);  
  return headers.length ? headers : null;  
}  
  
function stripSqlComments_(sql) {  
  return sql.replace(/\/\*[\s\S]*?\*\//g, "").replace(/--.*$/gm, "");  
}  
  
function splitByCommaOutsideParens_(s) {  
  const out = [];  
  let buf = "";  
  let depth = 0;  
  
  for (let i = 0; i < s.length; i++) {  
    const ch = s[i];  
    if (ch === "(") depth++;  
    if (ch === ")") depth = Math.max(0, depth - 1);  
  
    if (ch === "," && depth === 0) {  
      out.push(buf.trim());  
      buf = "";  
    } else {  
      buf += ch;  
    }  
  }  
  
  if (buf.trim()) out.push(buf.trim());  
  return out;  
}  
  
function headerFromSelectItem_(item) {  
  const t = item.trim().replace(/\s+/g, " ");  
  
  const asMatch = t.match(/\s+as\s+([A-Za-z0-9_]+)$/i);  
  if (asMatch) return asMatch[1];  
  
  const parts = t.split(" ");  
  if (parts.length >= 2) {  
    const last = parts[parts.length - 1];  
    const beforeLast = parts.slice(0, -1).join(" ");  
    if (!/[().]/.test(last) && /[().]/.test(beforeLast) === false) {  
      return last;  
    }  
  }  
  
  const col = t.replace(/^.*\./, "");  
  return col;  
}  
  
function writeDataCloudResultToSheet_(sheetName, body, explicitHeaders) {  
  const ss = SpreadsheetApp.getActiveSpreadsheet();  
  const sheet = ss.getSheetByName(sheetName) || ss.insertSheet(sheetName);  
  sheet.clearContents();  
  
  const data = body.data;  
  if (!Array.isArray(data) || data.length === 0) {  
    sheet.getRange(1, 1).setValue("No rows.");  
    return;  
  }  
  
  if (Array.isArray(data[0])) {  
    const colCount = data[0].length;  
  
    const headers =  
      Array.isArray(explicitHeaders) && explicitHeaders.length === colCount  
        ? explicitHeaders  
        : Array.from({ length: colCount }, (_, i) => `col_${i + 1}`);  
  
    const CHUNK = 5000;  
    sheet.getRange(1, 1, 1, headers.length).setValues([headers]);  
  
    for (let i = 0; i < data.length; i += CHUNK) {  
      const chunk = data.slice(i, i + CHUNK);  
      sheet.getRange(2 + i, 1, chunk.length, headers.length).setValues(chunk);  
    }  
    return;  
  }  
  
  sheet.getRange(1, 1).setValue("Unexpected data format.");  
  sheet.getRange(2, 1).setValue(JSON.stringify(body).slice(0, 5000));  
}
```

### Required Configuration

Be sure to replace the following values with those from your environment:

- **Client ID** (Consumer Key)
- **Execution Username** (your username with permissions)
- **Private Key** (for JWT authentication)

```
const SF_LOGIN_URL = "https://login.salesforce.com"; // Sandbox: https://test.salesforce.com  
const CLIENT_ID = "3MVG9GIRg253.lotxyT7qsSZdhj8ADPVk6.9Z4NsPAuxUAfTfanfzFuk3MV4iTm22RhAYt_rxlIC4hyLKIL";  
const USERNAME = "admin@nac-care.com";  
const API_VERSION = "66.0";  
  
const PRIVATE_KEY_PEM = `-----BEGIN PRIVATE KEY-----  
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCtTcj7mjX2Kguo  
ahVavRHq+cr+35h3b7jBarCzdlaoJZoayVI6I/NNZzMSMcR+DGhfVG0xXOHubQ2q  
kO6K+FSlMj/wyi2alpq7hS6CCoYwimfuPI4+CnNrVIQiksMe026kXmZ8tEpW6yV5  
lGmC/85p99bE8Pm0CgnlNcsfflx7gYtum9nAVzyu4cqJjYEdSudXh4eSnse0C0Tw  
dWs27aMOz9+7/7QX6QxdgSwkoorkR7KplSE8qrxAoVxPQomzP2ITetaHExbRh+LH  
qC8/wzLo/1uQuFi6v9sp3O6DIcv+K7fNg56o3ATCM27Xt7sFPS+sqIU7LW7mhMja  
CCPs64irAgMBAAECggEAERqQL2S01qqno+N0YBQw5IPqqOTgY0k/brdc4RlYzBeJ  
8gLUfrB1nroErFMFFXucAWyPqkOEeMeChcbwA/8mO3eOH/GUNqGOe9tVD7iCLeA7  
CaQoVa8qXPlmYRMi9rPfQ5Gdg8k3XQSwGiOvliIw+Pxg0ecGfeJPv7NjbKRH9FhX  
FZ0h8v67VPmKIAmRvEfOBV2G8Qp6vIWwS+bCGHspUtqzeIdPDbWbqjSsiddEGqeD  
/pDpvcseMIclaKzY0za0DeR9x2iDTnJPIQ/BxE55RAO/vnkjyo/1Wn0UcGe5E5KE  
3lOFe0gpFObtmHqPaQnO25xJ6EjlmJHFZ9mRmjhYoQKBgQDZccMNagVRJW7WOz/H  
A2D3LFVXQ1247ArD4CA9P3BFNJF2GCLMs3vOOGXKCbnVssW892s9zv6DAoFsbuka  
om4vwocBPXuTrqdnIy0K8IuwQnOzGMyHskO629m46WOG0FfdvG4PMOvwZ8HvkQQJ  
QG7e4eAJNlPbkAvSfD+Hz0TTXQKBgQDMCGU+Ui1BrGcduQWfRbT4Cc8Rz5f7qhAl  
LS8arp0d+HtF5AeqjtRpX4NKGX3sr9xBIZVfwla7jWOe0x6jd20Co5KjlGKvWR2w  
i6tRHGMk0/FOxcdQVR7hWw5+DSaLBmwi3AhE8ro8rqsGqVPqnutzP9BXG7Hr8BDe  
jfPucxDTpwKBgQCX5kbSGhw4waOZ+K3nAs88HDZJzX+tbQdgKjObVbPCRKTREK9O  
vJtiRjelWgH97PMBvP2nofBd6OQssZYZyxqaNpRFI4QueLXs8L/Igp2ytdlJZauL  
p9Z0tJx19mRWizi2Z6mi5xQLTxBFoNJm/CH3hWcSSGdwXEJF+hIPd5Wm6QKBgBMe  
UkZVsvHtcrghRzqWcI+xc5rKpgYp+FtTcY+Bfy14xCxXYrSDr7mz/nxqCRetnujn  
ebTAZBos9IHEbKGKpkdSBoKXe+vMYPDTFZmDHHMt/PWRqMyJPVyGiMQc/ViXoHhf  
v9KeH/9hqpr0MO3SOGPTPfV7nd9q3lnMWWgllhUPAoGAesQ2ItKlppmOG7mnLmz8  
9x5nxc3jJIktMusIQ0WxGnXdZDMTBfIsdZ1eCd7UbX4qfUXq8+JaYMEZ2z7GdJ8n  
y6UZ9hdEw61n7UxekFLUNLST7d/JnShaOdPmmX9oDoQuFEJvgGGRflQqBFoX5bsK  
xY53m5DJwquL0JzQZ9M=  
-----END PRIVATE KEY-----`;
```

### Notes

Since this method handles personal data, please exercise caution:

- **Access control management**
- **Data sharing scope**
- **Storage management**

It is important to design these appropriately before use.

By executing the script, the data will be displayed in the spreadsheet as follows:

## Conclusion

Using the methods introduced in this article, you can visualize which segments an individual belongs to.

This is useful in the following scenarios:

- **Segment validation**
- **Confirmation of target audience for delivery**
- **Prerequisite checks for personalization design**
- **Troubleshooting**

Segments in Marketing Cloud Next Growth & Advanced Edition have a structure where internal states are difficult to see. Therefore, it is important to have a way to directly check the actual data.

Please also try the following features mentioned earlier and determine what works best for you:

- [Segment Preview Feature](/p/be716460c70f)
- [Segment Member Verification Agent](/p/18f64f4f22ba)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
