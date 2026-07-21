# SFMC Tips #223 : Agentforce: How to Verify Whether a Customer’s Email Address Is Valid

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-223-agentforce-how-to-verify-whether-a-customers-email-address-is-valid-1c41a3e2021b

---

# SFMC Tips #223 : Agentforce: How to Verify Whether a Customer’s Email Address Is Valid

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1c41a3e2021b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1c41a3e2021b---------------------------------------)

16 min read

·

Dec 27, 2025

--

Photo by [Blake Hunter](https://unsplash.com/@blakeh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This time, using Salesforce’s [**free Developer Edition environment**](https://www.salesforce.com/form/developer-signup/), we will create a mechanism from scratch to check whether **a customer’s email address is valid**.

The configuration for email address verification can be broadly divided into the following two parts:

- **A flow that sends a verification code, and its Agent Action**
- **A flow that receives and validates the verification code, and its Agent Action**

In this scenario, when a **Service Agent** handling general FAQs receives a question that they **cannot answer**, even if the user is not an existing customer, the agent will:

1. Ask for the user’s email address
2. Automatically create a case
3. Escalate the issue so that **customer service staff** can respond later

This serves as a type of **escalation flow**.

Since we will be using a **Service Agent**, please create one based on the following article.  
(*Follow the instructions in the referenced article in order.*)

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----1c41a3e2021b---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----1c41a3e2021b---------------------------------------)

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----1c41a3e2021b---------------------------------------)

> *Even if you don’t have an external website such as* ***CloudPages****, you can verify everything inside the* ***Agentforce Builder preview****, so in that case it’s fine to only create the agent without deploying it to an external site.*

## Initial Setup in Developer Edition

In Developer Edition, you must start by enabling **Data Cloud** and **Knowledge**.  
If you run into issues at the beginning, refer to the following:

- **Enable Data Cloud**

- **Enable Knowledge**

After following the remaining steps, I displayed the Service Agent on an external website (CloudPages in Marketing Cloud Engagement).  
It looks like this:

Currently, this agent only handles FAQs using simple Knowledge responses.

![]()

## Process Overview

So, let’s move into the steps for this article. Roughly speaking, the overall flow will be as follows:

1. **Create a flow to send a verification code**
2. **Create a flow to receive and validate the code**
3. **Create a flow to create a case**
4. **Create an Agent Action for the “send code” flow**
5. **Create an Agent Action for the “verify code” flow**
6. **Create an Agent Action for the “create case” flow**
7. **Update instructions in the General FAQ topic**
8. **Update instructions in the Case Management topic**

## 1. Create the Flow to Send a Verification Code

**Preparation:**  
In a newly created Developer Edition environment, no sender email address is configured, so in Setup, go to **Organization-Wide Addresses** and configure an email address there.

## Configuration steps:

1. The three flows we are about to create will all be flows that are triggered from the Agent, so create all of them as **Autolaunched Flows (no trigger)**.

2. First, create the following variables.

> *Some of these variable names will also be used in “Instructions” later, so if you give them the same names here, it will be easier afterwards.*

- **emailAddress**: Variable (Text) → Available for input
- **verifCode**: Variable (Text) → Available for output
- **authKey**: Variable (Text) → Available for output
- **verifMessage**: Variable (Text) → Available for output

3. After creating the variables, place an Action and search for **“Generate Verification Code”**, then select it.   
For the Action Name, using **“Generate Verification Code”** as-is makes it easy to understand.

As for this “Generate Verification Code” action, it is an action that only generates a Verification Code, so once you place it, you are done with its configuration.

The following two items will be generated:

![]()

4. Next, place another Action, search for **“Send Email”**, and select it. This is the standard email-sending action.

5. The Action Name can be anything, but something like **“Send Verification Code”** should be fine.

- Recipient Addresses → `emailAddress`
- Sender Type → `OrgWideEmailAddress`
- Sender Email Address → Select the previously registered address

6. Next, for the email subject and body, pull in the resource **“The six digit generated verification code”** returned by the previous action. Also, enable rich text and allow line breaks.

You can use the following as a reference.

```
Subject:  
Your One-Time PasswordBody:  
Thank you for using our service.Please use the following One-Time Password (OTP) to complete your verification.━━━━━━━━━━━━━━━━━━  
One-Time Password  
{!Generate_Verification_Code.verificationCode}  
━━━━━━━━━━━━━━━━━━If you did not request this code, please ignore this email.  
For security reasons, do not share this code with anyone.If you need assistance, please contact our support team.――――――――――Support Team
```

7. Next, place an Assignment element and name it **“Set Verification Code”**. Here, you will assign the generated key and code to the existing variables (**verifCode**, **authKey**).

8. Then, set the existing **verifMessage** variable and directly enter the text **“I sent the code in your inbox”.** This can remain in English.

9. That’s all for the configuration, so please save the flow at this point. The name is up to you, but we will also use this name later in the instructions. I named it **“Send Verification Code Flow”.**

10. After saving, activate it.

## 2. Create the Flow to Validate the Verification Code

1. Once again, create a new **Autolaunched Flow (no trigger)**.

2. The variables we will use next are as follows, so please create them first.

Note that previously (**verifCode**, **authKey**) were used as **outputs**, but this time they are on the receiving side, so they will be used as **inputs**. Please be careful about this.

- **isVerified**: Variable (Boolean) → Available for output
- **verifCode**: Variable (Text) → Available for input
- **authKey**: Variable (Text) → Available for input
- **verifMessage**: Variable (Text) → Available for output

3. After creating the variables, place an Action and search for **“Verify Customer Code”**, then select it.

4. For the Action Name, using **“Verify Customer Code”** as-is makes it easy to understand. In this action, set the **Authentication Key** field to the **authKey** variable, and the **Customer Code** field to the **verifCode** variable.

5. Next, place a Decision element and name it **“Customer Verified”.**  
Set the left path to **“True”** and the right path to **“False”.** For the condition, select **“Is Verified”**, which is obtained from the output of the action you just configured.

6. For the value, select **True**.

7. Next, place an Assignment element and name it **“Set Success”.** For the variable, select the existing variable **“isVerified”.**

8. For the value, set it to the output value **Is Verified**. Since we have already branched on True beforehand, this value will always be True.

9. Then, for the variable, select **verifMessage**.

10. For the value, directly enter the text **“Success”.**

11. Next, on the opposite path, place a copy of the Success assignment element you just created.

12. In that copied assignment, change the Success part to **Failure**.

13. That completes the configuration, so give the flow a name and save it. I think **“Verify Customer Code Flow”** is a good name for this one.

14. Once you have successfully saved it, activate the flow.

## 3. Create the Flow to Create a Case

1. Next is the flow that creates the case. Again, create a new **Autolaunched Flow (no trigger).**

2. The variables we will use are as follows, so please create them first.

- **caseDescription**: Variable (Text) → Available for input
- **caseSubject**: Variable (Text) → Available for input
- **caseRecord**: Variable (Record) — Case object → Available for output

> ***caseRecord*** *is a “record” variable that has not appeared so far. For the object, select* ***Case****.*

3. Next, place a **Create Records** element, name it **“Create Case Record”**, change the configuration mode to **“Manual”**, and select the **Case** object.

4. For the Case **Subject** field, enter the existing **caseSubject** variable. Then, for the **Description** field, enter the existing **caseDescription** variable.

5. Next, place a **Get Records** element, name it **“Get Case Record”**, select the **Case** object, and for the field, select **“Case ID”.**

6. For the value, select the **Case ID** that was just created by the Create Records element above.

7. Next, since we want to display (output) the information for this newly created case to the customer in the chat, we will populate the record variable **caseRecord** with values. Scroll further down and configure it as follows.

![]()

8. In addition to the **Id** field, which is displayed by default, add the following five fields:

- Subject
- Description
- CreatedDate
- Status
- CaseNumber

![]()

9. With that, you are done, so save this flow. I think **“Create Case Flow”** is an appropriate name.

10. Once you have saved it, activate the flow.

## 4. Create the Agent Action for Sending the Verification Code

1. Next, we will configure the agent.  
Open the agent you previously created, disable it so that it becomes editable, and then select **Topics** to add a new topic.

2. Select **Case Management**.

3. Once the Case Management topic has been added, open the linked actions and delete all of them for now.

4. Then, add a new action.

5. For the action type, select **Flow**.

6. Here, the flows you created earlier will be displayed. Select **Send Verification Code Flow**.

7. Remove “Flow” from the end of the Agent Action label to make it cleaner, then continue.

8. After that, fill in the instructions.  
Below is an example. It is fine to enter the text exactly as written here.

- **Agent Action Instructions**  
   Sends a generated verification code to the user’s email address.
- **emailAddress (Input)**  
   Pass the email address provided by the user.
- **authKey (Output)**  
   Stores the authentication key used to generate the verification code.
- **verifCode (Output)**  
   Stores the generated verification code.
- **verifMessage (Output)**  
   Stores a generic message that will be displayed to the user.

9. Other settings:  
“Show loading text for this action” can remain **OFF**.  
For input / output settings:

- **emailAddress (Input)**  
   → Check Require input  
   → Check Collect data from user
- **authKey (Output)**  
   → Check Filter from agent action  
   → Do not check Show in conversation
- **verifCode (Output)**  
   → Check Filter from agent action  
   → Do not check Show in conversation
- **verifMessage (Output)**  
   → Do not check Filter from agent action  
   → Check Show in conversation

**Reference explanation from the original text:**

- **Require input** means the action cannot be executed without the required input value.
- **Collect data from user** means the value must be obtained directly from the customer (e.g., email address or order number).
- **Filter from agent action** excludes values from agent reasoning and prevents them from being used in responses.
- **Show in conversation** allows the value to be shown to the customer.

10. Once everything is set, click **Done**.

11. When the action has been created, click on it to open it.

12. Click **Edit**, then map:  
➡ `authKey = authenticationKey`Save.

## 5. Create Agent Action for Validating the Code

1. Again, within **Case Management**, create a new action.

2. As before, select **Flow** and choose **Verify Customer Code Flow**.

3. In the Action Name, remove “Flow”, rename it as needed, and save.

4. Below are the instructions to enter:

- **Agent Action Instructions**  
  Verifies whether the verification code entered by the user matches the code sent to the user’s email address.
- **authKey (Input)**  
  Pass the authentication key used to generate the verification code.
- **verifCode (Input)**  
  Pass the verification code entered by the user.
- **isVerified (Output)**  
  Stores the result indicating whether the verification code is valid.
- **verifMessage (Output)**  
  Stores the message to display based on the verification result.

5. Other settings:  
“Show loading text for this action” can remain **OFF**.  
For input / output settings:

- **authKey (Input)**  
  → Require input  
  → Do not check Collect data from user
- **verifCode (Input)**  
  → Require input  
  → Collect data from user (because the user will provide the value)
- **isVerified (Output)**  
  → Filter from agent action  
  → Do not check Show in conversation
- **verifMessage (Output)**  
  → Do not check Filter from agent action  
  → Show in conversation

6. Once all settings are complete, click **Done**.

7. After it has been created, click the action to open it.

8. Click **Edit**, then map:

- `authKey = authenticationKey`
- `isVerified = isVerified`

Only these two mappings are needed. Save.

## 6. Create Agent Action for Creating a Case

1. Finally, configure the Agent Action that uses the **Create Case Flow**, following the same steps.

2. Open the creation screen for the Create Case Flow.

3. Enter the following instructions.

- **Agent Action Instructions**  
  Creates a new case using the information provided by the user.  
  This action receives the subject and description, and registers a case record in Service Cloud.
- **caseDescription (Input)**  
  Stores the details of the user’s inquiry for case creation.
- **caseSubject (Input)**  
  Stores the subject of the case to be created.
- **caseRecord (Output)**  
  Stores the case record that was created for the customer.

4. Other settings:  
 (“Show loading text for this action” can remain **OFF**)

- caseDescription (Input)  
  → Require input  
  → Do not check Collect data from user  
  (The agent will automatically generate this through summarization)
- **caseSubject (Input)**  
  → Require input  
  → Do not check Collect data from user  
  (The agent will generate the subject text)
- **caseRecord (Output)**  
  → Do not check Filter from agent action  
  → Show in conversation

\* This Agent Action does not require variable mapping.  
Configuration is now complete.

## 7. Rewrite Instructions in the “General FAQ” Topic

1. Next, configure the **General FAQ** topic.  
Please overwrite the existing content with the following.

**Classification Description**  
This topic is intended to answer customer questions by searching knowledge articles and responding based on the information contained in those articles.

**Scope**  
Your role is strictly limited to answering questions about the company, its products, business procedures, or policies by searching and using knowledge articles.

**Instruction ①**  
Highest Priority：For any question that can be answered using information stored in knowledge articles, you must always respond using the “Answer Questions with Knowledge” action.

**Instruction ②**  
When Knowledge Is Not Available：If no relevant knowledge article can be found and you are unable to provide an answer, politely apologize to the customer and clearly inform them that the information is not available.

**Instruction ③**  
Prohibited Actions：Unless the response is based on information retrieved from knowledge articles, you must not provide general information, assumptions, advice, or troubleshooting steps.

**Instruction ④**  
Transition to Case Creation：After providing an answer — or if you are unable to answer — always ask the user whether they would like to proceed with creating a case.  
\*Do not ask for a verification email address or any personal information upfront.

**Instruction ⑤**  
Creating a Case：Only if the user explicitly requests to create a case, switch to the “Case Management” topic and proceed accordingly.

2. Once complete, save the configuration.

## 8. Rewrite Instructions in the “Case Management” Topic

1. This is the final topic to update.  
Please overwrite the existing content with the following.

**Classification Description**  
This topic is intended to handle customer interactions related to support cases.  
It covers case-related actions such as providing case information and creating new cases.

**Scope**  
Your role is strictly limited to retrieving and sharing case information and creating new cases based on customer requests.  
Do not perform any actions outside of this scope.

**Instruction ①  
Knowledge Questions First：**  
For any questions related to knowledge, always respond using the **“Answer Questions with Knowledge”** action.  
If the required information is not available in knowledge articles, politely apologize and ask the customer whether they would like to proceed with creating a case.  
**Do not ask for an email address at this stage.**

**Instruction ②  
Authentication (Required)：**  
Before performing any case-related actions (retrieve, update, or create), you must verify the customer’s identity.Use the **“Send Verification Code”** action to start the authentication process.  
Use the email address provided by the customer as the input value **“emailAddress”** for this action.

**Instruction ③  
Authentication Constraints：**  
If the verification code is entered incorrectly **twice consecutively**, ask the customer to re-enter their email address.  
Then, re-run the **“Send Verification Code”** action to restart the authentication process from the beginning.  
Upon successful authentication, display the verification completion message contained in **“verifMessage”.**  
Once a user has been authenticated, switching to another user within the same conversation session is **not permitted under any circumstances**.  
During the authentication process, **do not display or disclose the verification code to the customer**.  
This information must always be treated as confidential.

**Instruction ④  
Sharing Case Information：**  
When sharing case details with the customer, display the following fields as a bulleted list:  
- Case number  
- Subject  
- Description  
- Status  
\*The **Description** field must store the email address (**emailAddress**) used for authentication.

**Instruction ⑤  
Creating a New Case：**  
When a customer requests case creation, perform the following steps:  
- Summarize the conversation so far.  
- **Subject**: Provide a concise, high-level summary of the customer’s inquiry.  
- **Description**: Include  
“What the customer asked”  
“Any important data”  
“Any information necessary for a customer service representative to understand the context”  
When creating the case, always include the email address specified in **“emailAddress”** in the case record’s **Description** field.

**Instruction ⑥  
Language and Communication：**  
- GuidelinesDo not use the term **“support team”.** Always refer to **“customer service representatives”.**  
- If the response requires additional time, clearly inform the customer that **the reply may be provided on the following day or later**.

2. Once finished, save the configuration.

## 9. Testing the Completed Setup

All configurations are now complete.  
Let’s actually test the Service Agent on the external website.

> *⚠️ Make sure the agent is* ***enabled*** *before testing.*

1. Start by asking a question that is not available in Knowledge, for example: *“I would like to cancel my membership. What should I do?”*

Because there is no Knowledge article regarding cancellation, the agent will prompt to create a case.

![]()

2. Respond with **“Yes”**, and the agent will ask for an email address for verification.  
Enter the email address and submit.

![]()

3. A verification code will be sent to the entered email address.

![]()

4. When you check your email inbox, you should see the verification code.

![]()

5. Enter the verification code and submit.  
You will then see a message indicating that a case has been created.

![]()

6. When you check the Case object, you will confirm that the case was successfully created.

## Conclusion

By using only the standard flow actions, you can build a fully functioning agent **without any custom development**.  
Although Agentforce configuration can feel lengthy, this is a great opportunity to try it out.

That’s all for now.  
Thank you for reading — and happy building!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
