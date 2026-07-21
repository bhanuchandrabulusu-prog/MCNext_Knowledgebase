# SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Audiences from a Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-forcefully-exit-contacts-from-a-flow-bfb9bd74e071

---

# SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Audiences from a Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--bfb9bd74e071---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--bfb9bd74e071---------------------------------------)

8 min read

·

Feb 10, 2026

--

Photo by [Adrien King](https://unsplash.com/@adrienisking?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, you can use various flows such as **Segment-Triggered Flows, Event-Triggered Flows, and On-Demand Flows** to enable real-time actions and automation.

However, during operations, have you ever encountered cases like these?

- ✅ Reminder emails keep being sent even though the purchase is already completed
- ✅ Follow-ups don’t stop even though the case has already been handled
- ✅ You want to end the flow because processing was completed in an external system

To dynamically exclude these **“individuals who no longer need to remain in the flow”,** the **Exit Individuals from a Flow Action (REST API)** was introduced in the [**Spring ’26 new feature release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb).

By using this API, you can:  
**Immediately remove a specific Individual from a running flow.**

## Use Case Example

### 🛒 **Purchase Reminder Flow**

1. Cart abandonment
2. Reminder after 1 day
3. Re-notification after 3 days
4. Coupon after 7 days

**Purchase completed** midway on an external EC site

If left as is:  
 ❌ “Haven’t you purchased yet?” email gets sent

⇒ Therefore, exclude from the flow using the **Exit Individuals API**

## Supported Flow Types

This action can be used with the following flows:

- **Segment-Triggered Flow**
- **Event-Triggered Flow**
- **On-Demand Flow**

## API Specifications

This API works with [**API version 66.0 (Spring ’26)**](https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/api_action.pdf) or later.

```
--- Method  
POST   
  
--- Endpoint  
https://[My Domain].my.salesforce.com/services/data/v66.0/actions/custom/exitIndividualsFromFlow/[flow_API_name]  
  
---Header  
Content-Type：application/json   
Authorization：Bearer [Access Token]   
  
--- Body  
{  
  "inputs": [  
    {  
      "individualId": "003R000000ExAmPlE",  
      "flowVersionId": "301R000000AbCdEfG",  
      "description": "Customer completed purchase via external portal."  
    }  
  ]  
}
```

- “**flowVersionId**” is optional.  
  If not specified, the individual exits from all versions.
- “**description**” is also optional.

## Implementation Image (Usage Patterns)

### Pattern ① External EC completion trigger

EC → Webhook → Lambda → REST API → Exit Flow

### Pattern ② CRM update trigger

Opportunity Closed Won → Apex → Callout → Exit Flow

### Pattern ③ Support completion

Case Closed → Event-Triggered Flow → Exit Flow

## Create a Forced Exit Screen on the Contact Page

Finally, create a **Screen Flow** to build a contact exit screen.

### Flow:

- Contact record  
   ↓ (Quick Action)
- Screen Flow  
   ↓
- Get Contact → IndividualId  
   ↓
- Manually input Flow API Name  
   ↓
- Apex (Invocable)  
   ↓
- POST /actions/custom/exitIndividualsFromFlow/{flowApiName}

## Configuration Steps

## 1. Create a Named Credential

For the creation method, please refer to the following two articles.

- In the articles below, proceed until you obtain the **Consumer Key** and **Consumer Secret**.

[## SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

### Previously, I wrote an article on how to obtain an access token when using the REST API in Marketing Cloud Engagement.

medium.com](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584?source=post_page-----bfb9bd74e071---------------------------------------)

- Using the **Consumer Key** and **Consumer Secret** obtained above, create a Named Credential.
- In the **“Schedule Execution of Data Graph”** section, execute **steps 1 through 24**.  
  If you use the Apex code below as-is, name the Named Credential **Name (API Name)** as **“SelfOrg”**.

[## SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

### In Marketing Cloud Next Growth & Advanced Edition, Identity Resolution and Data Graph cannot be executed on a schedule…

medium.com](/@marketingcloudtips/marketing-cloud-next-scheduling-identity-resolution-and-data-graph-a63aecf1904a?source=post_page-----bfb9bd74e071---------------------------------------)

## 2. Register the Apex Class

Please register the following Apex Code.

- Reconfirm that the **Name (API Name)** of the Named Credential registered in the settings is **“SelfOrg”**.

```
public with sharing class ExitIndividualsFromFlowAction {  
  
    public class Request {  
        @InvocableVariable(required=true)  
        public String individualId;  
  
        @InvocableVariable(required=true)  
        public String flowApiName;  
    }  
  
    public class Result {  
        @InvocableVariable public Boolean success;  
        @InvocableVariable public Integer statusCode;  
        @InvocableVariable public String message;  
        @InvocableVariable public String responseBody;  
    }  
  
    @InvocableMethod(label='Exit Individual From Flow')  
    public static List<Result> run(List<Request> requests) {  
  
        List<Result> results = new List<Result>();  
  
        for (Request req : requests) {  
            Result r = new Result();  
  
            try {  
                String apiName = (req.flowApiName == null) ? '' : req.flowApiName.trim();  
  
                HttpRequest httpReq = new HttpRequest();  
                httpReq.setMethod('POST');  
                httpReq.setEndpoint(  
                    'callout:SelfOrg/services/data/v66.0/actions/custom/exitIndividualsFromFlow/' +  
                    EncodingUtil.urlEncode(apiName, 'UTF-8')  
                );  
                httpReq.setHeader('Content-Type', 'application/json');  
                httpReq.setTimeout(120000);  
  
                Map<String,Object> body = new Map<String,Object>{  
                    'inputs' => new List<Object>{  
                        new Map<String,Object>{ 'individualId' => req.individualId }  
                    }  
                };  
                httpReq.setBody(JSON.serialize(body));  
  
                HttpResponse res = new Http().send(httpReq);  
  
                r.statusCode = res.getStatusCode();  
                r.responseBody = res.getBody();  
                r.success = (r.statusCode >= 200 && r.statusCode < 300);  
  
                if (r.success) {  
                    r.message = 'Successfully exited';  
                } else {  
                    r.message = r.responseBody;  
  
                    if (r.statusCode == 400 && !String.isBlank(r.responseBody)) {  
                        String errCode = extractFirstErrorStatusCode(r.responseBody);  
  
                        if (errCode == 'INDIVIDUAL_NOT_IN_FLOW') {  
                            r.message = 'This individual is not currently in the flow (no exit required)';  
                        }  
                    }  
                }  
  
            } catch (Exception e) {  
                r.success = false;  
                r.message = 'Exception: ' + e.getMessage();  
            }  
  
            results.add(r);  
        }  
  
        return results;  
    }  
  
    private static String extractFirstErrorStatusCode(String jsonText) {  
        try {  
            Object root = JSON.deserializeUntyped(jsonText);  
  
            if (!(root instanceof List<Object>)) return null;  
            List<Object> rootList = (List<Object>)root;  
            if (rootList.isEmpty()) return null;  
  
            Object first = rootList[0];  
            if (!(first instanceof Map<String,Object>)) return null;  
            Map<String,Object> firstMap = (Map<String,Object>)first;  
  
            Object errorsObj = firstMap.get('errors');  
            if (!(errorsObj instanceof List<Object>)) return null;  
            List<Object> errors = (List<Object>)errorsObj;  
            if (errors.isEmpty()) return null;  
  
            Object e0 = errors[0];  
            if (!(e0 instanceof Map<String,Object>)) return null;  
            Map<String,Object> e0Map = (Map<String,Object>)e0;  
  
            Object statusCodeObj = e0Map.get('statusCode');  
            return (statusCodeObj == null) ? null : String.valueOf(statusCodeObj);  
  
        } catch (Exception ignore) {  
            return null;  
        }  
    }  
}
```

## 3. Create a Screen Flow

### 1. Create a new Screen Flow.

### 2. Create the following five variables.

**(1) recordId**

- **API Name:** recordId
- **Data Type:** Text
- **Available for input:** ON

**(2) varIndividualId**

- **API Name:** varIndividualId
- **Data Type:** Text

**(3) varMessage**

- **API Name:** varMessage
- **Data Type:** Text

**(4) varStatusCode**

- **API Name:** varStatusCode
- **Data Type:** Number
- **Decimal Places:** 0

**(5) varSuccess**

- **API Name:** varSuccess
- **Data Type:** Boolean

### 3. Configure the Get Records element.

- **Label:** Get Contact
- **API Name:** Get\_Contact
- **Object:** Contact
- **Condition Requirements:** All Conditions Are Met (AND)
- **Field:** Contact Id
- **Operator:** Equals
- **Value:** {!recordId} (variable)
- **How Many Records to Store:** Only the first record (default)
- **How to Store Record Data:** Automatically store all fields (default)

### 4. Configure Assignment.

- **Label:** Set IndividualId
- **API Name:** Set\_IndividualId
- **Set Variable Values:**  
  varIndividualId (variable) = {!Get\_Contact.Id}

### 5. Place a Screen element and enter the following.

- **Label:** Input Flow API Name
- **API Name:** Input\_Flow\_API\_Name

### 6. Drag and drop a Text component, enter the following, and save the element.

- **Label:** Flow API Name
- **API Name:** varFlowApiName  
  (\*The entered Flow API Name is stored in this variable.)
- **Required:** ON

## 4. Apex Action

### 1. Place an Action and select the created Apex (Exit Individual From Flow).

### 2. Set the label and API name, and map the following two values.

- **Label:** Exit Individual From Flow
- **API Name:** Exit\_Individual\_From\_Flow
- **Set Input Values:**  
  flowApiName = {!varFlowApiName} (variable from screen)  
  individualId = {!varIndividualId} (variable)

> *At this point, the implementation is complete, but the following screens are created to display the result.*

## 5. Assign Output Responses

Assign the output responses from Apex to the remaining three variables created initially.  
Place an **Assignment** element.

- **Label:** Set Result
- **API Name:** Set\_Result
- **Set Variable Values:**  
  varSuccess = {!Exit\_Individual\_From\_Flow.success}  
  varStatusCode = {!Exit\_Individual\_From\_Flow.statusCode}  
  varMessage = {!Exit\_Individual\_From\_Flow.message}

## 6. Create Success and Failure Branches

Place a **Decision** element.

- **Label:** Check Success
- **API Name:** Check\_Success
- **Left path name:** Success
- **Right path name:** Failure
- **Left condition:**  
  {!Exit\_Individual\_From\_Flow.success} = True

## 7. Create the Success Screen

Place a **Screen** element on the left path and set the label and API name.

- **Label:** Success Exit Completed
- **API Name:** Success\_Exit\_Completed

Next, place **Display Text**, enter the following, and save.

- **API Name:** Success\_Display
- **Text:**  
  ✅ **Exit successful  
  -** Status: {!varStatusCode}

## 8. Create the Failure Screen

Place a **Screen** element on the right path and enter the following.

- **Label:** Error Exit Flow
- **API Name:** Error\_Exit\_Flow

Also place **Display Text**, enter the following, and save.

- **API Name:** Failure\_Display
- **Text:**  
  ❌ **Exit failed  
  -** Status: {!varStatusCode}  
  - Details: {!varMessage}

## 9. Save and Activate the Flow

Save and activate the flow.

- **Flow Name:** Exit Individual From Flow
- **API Name:** Exit\_Individual\_From\_Flow

## 10. Configure as a Contact Action

1. From Setup > Object Manager, select Contact, then Buttons, Links, and Actions, and click New Action.

2. Enter the following.

- **Action Type:** Flow
- **Flow:** Exit Individual From Flow
- **Label:** Exit Flow
- **API Name:** Exit\_Flow

3. After saving the new action, add it to the Contact Page Layout.

## 11. Operation Check

1. Open a Contact record that exists in a flow and click the “Exit Flow” quick action.

2. The Exit Flow screen opens. Enter the “**Flow API Name**” (❌ “Label Name”) and proceed.

> *Example: my On-demand flow’s “****Order\_Confirmation\_Flow”***

3. “**Exit successful**” is displayed.

4. The flow does not proceed further. Success!!

5. If the Contact record does not exist in the flow, “**Exit failed**” is displayed as shown below.

## Conclusion

In **Marketing Cloud Next**, not only “starting” but also **controlling “stopping midway”** is extremely important.

The **Exit Individuals API** can be considered an **essential technique** for operating flows more intelligently.

If you are running real-time initiatives or external integrations, please make use of it.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
