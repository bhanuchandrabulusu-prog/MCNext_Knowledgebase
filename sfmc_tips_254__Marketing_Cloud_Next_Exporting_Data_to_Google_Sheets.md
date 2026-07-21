# SFMC Tips #254 : Marketing Cloud Next: Exporting Data to Google Sheets

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-exporting-data-to-google-sheets-cb672a47228a

---

# SFMC Tips #254 : Marketing Cloud Next: Exporting Data to Google Sheets

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cb672a47228a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cb672a47228a---------------------------------------)

9 min read

·

Feb 22, 2026

--

Photo by [JOSHUA COLEMAN](https://unsplash.com/@joshstyle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Since the article I wrote previously about [automatically integrating **Data Extension data in Marketing Cloud Engagement** with **Google Sheets**](/@marketingcloudtips/integrating-data-extensions-with-google-sheets-using-apps-script-7f7c1eb9e1a2) was well received, this time I would like to explain how to integrate data from **Marketing Cloud Next (that is, Data Cloud)** with spreadsheets.

> *This technique uses the* ***Data Cloud Query API****.  
> If you are able to perform searches in the standard* ***Data Cloud Query Editor****, you should understand that it is possible to use those queries for output.*

In the case of Marketing Cloud Next, the steps are as follows:

1. **Create a key pair for JWT**
2. **Create an External Client App**
3. **Pre-Authorization for the user**
4. **Set up the Apps Script environment**

## Configuration Steps

## 1. Create a Key Pair for JWT

### 1. Install Git for Windows

Git for Windows (Git Bash) includes OpenSSL, which makes it ideal for generating the key pair required in this setup.

[## Install

### Click here to download the latest ( 2.53.0) x64 version of Git for Windows. This is the most recent maintained build…

git-scm.com](https://git-scm.com/install/windows?source=post_page-----cb672a47228a---------------------------------------)

### 2. Create a Folder to Store the Keys

After opening Git Bash, enter the following two lines together to create a folder to store the keys and move to that folder.

```
mkdir -p ~/projects/jwt  
cd ~/projects/jwt
```

![]()

### 3. Create the Private Key

Next, create the **private key** in the moved folder.

```
openssl genpkey -algorithm RSA -out server_pkcs8.key -pkeyopt rsa_keygen_bits:2048
```

![]()

If successful, **server\_pkcs8.key** will be created.  
This **private key** will be embedded in the **Apps Script** code.

### 4. Create the Public Certificate

Next, create the **public certificate**.

```
openssl req -new -x509 -key server_pkcs8.key -out server.crt -days 3650 -sha256
```

![]()

You will need to enter values such as **Country Name**, but it works even if you enter them arbitrarily.

![]()

If successful, **server.crt** will be created.  
This **public certificate** will be used when creating the following **External Client App**.

![]()

## 2. Create an External Client App

1. Search for **Setup ＞ External Client App Manager** and create a new **External Client App**.

2. Decide the **Name** and **API Name**.  
In my example, it is **“Data Cloud Query JWT Integration”.**

3. Open **API (Enable OAuth Settings)** and enable **OAuth**.

The **Callback URL** is required, but it is not actually used, so enter an appropriate value such as:

```
http://localhost:3000/oauth/callback
```

For the following **OAuth scopes**, select the two below:

- **Manage user data via APIs (api)**
- **Perform requests at any time (refresh\_token, offline\_access)**

4. Next, enable **JWT Bearer Flow** and select the public certificate (**server.crt**).  
It is fine to turn all security settings off.

Once everything is configured, click the **Create** button.

## 3. Pre-Authorization for the User

1. Click the **Edit** button in the **Policies** tab.

2. Under **Permitted Users**, select:

**Admin approved users are pre-authorized**

3. Return to **App Policies** and select either:

- The **profile of the execution user**, or
- The **permission set assigned to the execution user**

After that, click **Save**.

4. Move to the **Settings** tab.

5. In the middle section, click the **Consumer Key and Secret** button.

6. Login will be executed.

![]()

7. Copy only the **Consumer Key (Client ID)**.  
This will be used in the following **Apps Script** code.

## 4. Set Up the Apps Script Environment

1. Move to **Google Sheets** to begin working.

Open the spreadsheet, then from the menu bar open the **Extensions** tab and click **Apps Script**.

2. The code input screen will appear.  
Delete the existing content and paste the following code.

```
const SF_LOGIN_URL = "https://login.salesforce.com"; // Sandbox: https://test.salesforce.com  
const CLIENT_ID = "3MVG9GIRg253.lotxyT7qsSZdhj8gAEDPVk6.9Z4NsPAuxUAfTfanzFuk3MV4iTm22RhAYt_rxlIC4hyLKIL";  
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
xY53m5DJwquL0nJUzzQZ9M=  
-----END PRIVATE KEY-----`;  
  
const SHEET_NAME = "Data_Cloud_Query";  
const LIMIT_ROWS = 100000;  
  
function run_DataCloudQuery_JWT_toSheets() {  
  const token = getAccessTokenByJwt_();  
  const accessToken = token.access_token;  
  const instanceUrl = token.instance_url;  
  
  const sql = `  
  
SELECT  
    a.ssot__IndividualId__c AS Id,  
    a.ssot__SendtimeEmailAddress__c AS Email,  
    i.ssot__FirstName__c AS FirstName,  
    i.ssot__LastName__c AS LastName,  
    a.ssot__EngagementDateTm__c + interval '9 hour' AS EngagementDateTime,  
    a.ssot__EngagementChannelActionId__c AS ActionName,  
    a.ssot__EmailRecipientSendStatus__c AS SendStatus,  
    c.ssot__Name__c AS EmailElementAPIName,  
    e.ssot__Name__c AS FlowName,  
    d.ssot__VersionNumber__c AS VersionNumber,  
    h.ssot__Name__c AS SegmentName,  
    a.ssot__EngagementActionReasonText__c AS ActionReason,  
    a.ssot__EmailBounceType__c AS BounceType,  
    a.ssot__BounceReasonText__c AS BounceReason,  
    a.ssot__UnsubscribeSourceText__c AS UnsubscribeSource,  
    a.ssot__ResolvedURL__c AS LinkURL,  
    g.ssot__Subject__c AS EmailSubject,  
    g.ssot__FromAddress__c AS FromAddress,  
    g.ssot__MessagePurpose__c AS MessagePurpose  
FROM ssot__EmailEngagement__dlm a  
JOIN ssot__FlowElementRun__dlm b ON a.ssot__FlowElementRunId__c = b.ssot__Id__c  
JOIN ssot__FlowElement__dlm c ON b.ssot__FlowElementId__c = c.ssot__Id__c  
JOIN ssot__FlowVersion__dlm d ON c.ssot__FlowVersionId__c = d.ssot__Id__c  
JOIN ssot__Flow__dlm e ON d.ssot__FlowId__c = e.ssot__Id__c  
JOIN ssot__BulkEmailMessage__dlm g ON a.ssot__BulkEmailMessageId__c = g.ssot__Id__c  
LEFT OUTER JOIN ssot__MarketSegment__dlm h ON g.ssot__MarketSegmentId__c = h.ssot__Id__c  
JOIN ssot__Individual__dlm i ON a.ssot__IndividualId__c = i.ssot__Id__c  
ORDER BY a.ssot__EngagementDateTm__c DESC  
  
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

3. Modify the following information with your own details:

```
const SF_LOGIN_URL = "https://login.salesforce.com"; // Sandbox: https://test.salesforce.com  
const CLIENT_ID = "3MVG9GIRg253.lotxyT7qsSZdhj8gAEDPVk6.9Z4NsPAuxUAfTfanfzFuk3MV4iTm22RhAYt_rxlIC4hyLKIL";  
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
xY53m5DJwquL0nJUzzQZ9M=  
-----END PRIVATE KEY-----`;
```

- **Client ID (= Consumer Key)**
- **Execution username** (your username with permissions granted)
- **Private key**

4. The most important part is the **query section**.  
As mentioned above, anything that can be executed in the **Query Editor** can be used as-is.

> *The example below retrieves data related to* ***Email Engagement****.  
> You should be able to confirm that this exists in the sample code.*

```
SELECT  
    a.ssot__IndividualId__c AS Id,  
    a.ssot__SendtimeEmailAddress__c AS Email,  
    i.ssot__FirstName__c AS FirstName,  
    i.ssot__LastName__c AS LastName,  
    a.ssot__EngagementDateTm__c + interval '9 hour' AS EngagementDateTime,  
    a.ssot__EngagementChannelActionId__c AS ActionName,  
    a.ssot__EmailRecipientSendStatus__c AS SendStatus,  
    c.ssot__Name__c AS EmailElementAPIName,  
    e.ssot__Name__c AS FlowName,  
    d.ssot__VersionNumber__c AS VersionNumber,  
    h.ssot__Name__c AS SegmentName,  
    a.ssot__EngagementActionReasonText__c AS ActionReason,  
    a.ssot__EmailBounceType__c AS BounceType,  
    a.ssot__BounceReasonText__c AS BounceReason,  
    a.ssot__UnsubscribeSourceText__c AS UnsubscribeSource,  
    a.ssot__ResolvedURL__c AS LinkURL,  
    g.ssot__Subject__c AS EmailSubject,  
    g.ssot__FromAddress__c AS FromAddress,  
    g.ssot__MessagePurpose__c AS MessagePurpose  
FROM ssot__EmailEngagement__dlm a  
JOIN ssot__FlowElementRun__dlm b ON a.ssot__FlowElementRunId__c = b.ssot__Id__c  
JOIN ssot__FlowElement__dlm c ON b.ssot__FlowElementId__c = c.ssot__Id__c  
JOIN ssot__FlowVersion__dlm d ON c.ssot__FlowVersionId__c = d.ssot__Id__c  
JOIN ssot__Flow__dlm e ON d.ssot__FlowId__c = e.ssot__Id__c  
JOIN ssot__BulkEmailMessage__dlm g ON a.ssot__BulkEmailMessageId__c = g.ssot__Id__c  
LEFT OUTER JOIN ssot__MarketSegment__dlm h ON g.ssot__MarketSegmentId__c = h.ssot__Id__c  
JOIN ssot__Individual__dlm i ON a.ssot__IndividualId__c = i.ssot__Id__c  
ORDER BY a.ssot__EngagementDateTm__c DESC
```

> ***Tips:*** *By assigning aliases using* ***AS****, it is possible to maintain consistency in column names in the spreadsheet, so be sure to use* ***AS****.*

5. Execute the function.

6. Grant access permissions.

![]()

7. Loading will begin, so wait for completion.

8. When you check the spreadsheet, you can confirm the data. **Success!!**

9. This result is the same as the result obtained when running the same query in the Query Editor.

## Conclusion

By performing this task once, you will be able to view the desired data in **Data Cloud** on a spreadsheet whenever you need it.

However, while it may be fine in something like a **demo environment**, when performing this in an actual **production environment**, there are concerns such as leakage of personal information, so it is not something that can be done casually.  
Please exercise **extreme caution**. ⚠️

> *I have published a few sample queries like the ones shown here in the article below. Please refer to those as well.*

[## SFMC Tips #255 : Marketing Cloud Next: Ready-to-Use Queries for Query Editor

### The Query Editor in Marketing Cloud Next Growth & Advanced Edition is useful for investigating data within Data Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-255-marketing-cloud-next-ready-to-use-queries-for-query-editor-72d1675c06d8?source=post_page-----cb672a47228a---------------------------------------)

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
