# SFMC Tips #234 : Agentforce: Custom Lightning Types (Editor + Renderer Override)

**Source:** https://medium.com/@marketingcloudtips/agentforce-custom-lightning-types-editor-renderer-override-c4e408bc7819

---

# SFMC Tips #234 : Agentforce: Custom Lightning Types (Editor + Renderer Override)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c4e408bc7819---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c4e408bc7819---------------------------------------)

11 min read

·

Jan 13, 2026

--

Photo by [Varun Gaba](https://unsplash.com/@varunkgaba?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I introduced how to display a rich UI in Agentforce by using **Custom Lightning Types** with a collection renderer override.

[## SFMC Tips #233 : Agentforce: Custom Lightning Types (Collection Renderer Override)

### In Agentforce, standard Lightning Types are typically used by default, so the UI tends to be simple.

medium.com](/@marketingcloudtips/sfmc-tips-233-agentforce-custom-lightning-types-collection-renderer-override-c3b7ad840303?source=post_page-----c4e408bc7819---------------------------------------)

![]()

In this article, I will actually try another sample scenario provided by Salesforce.

There are two types of official samples available.   
In the previous article, I covered ②.   
This time, I will focus on scenario ①.

**Official Samples (2 Types)**

**① Override Editor + Renderer**  
(Full control from input to output)  
<https://developer.salesforce.com/docs/ai/agentforce/guide/lightning-types-example-full-editor-renderer.html>

**② Override Collection Renderer**  
(Specialized for displaying multiple records)  
<https://developer.salesforce.com/docs/ai/agentforce/guide/lightning-types-example-collection-renderer.html>

These official samples have the retrieved data hard-coded in advance, so there is no need to create new objects or records for verification. They are very suitable when you simply want to check the behavior first.

> *As of the time of writing this article, the agents that support Custom Lightning Types are as follows:*

- **Agentforce Service Agent (Enhanced Chat v2)**
- **Agentforce Employee Agent**

## Differences Between the Two Approaches

**① (Editor + Renderer)**  
While you can comprehensively control both the input UI and the display UI, you need to design everything from input through output.  
As a result, the degree of freedom in design and implementation is high, but the difficulty level is also higher.

**② (Collection Renderer)**  
This approach is specialized for displaying multiple records (collections) and mainly customizes the “output side”.  
In many cases, it does not go as far as customizing the input UI, making it relatively easier to work with.

In this article, I will organize the implementation steps   
for **① Editor + Renderer Override**.

By following the actual steps, I hope you can use this as reference material to judge:

- “How much design and implementation cost is required?”
- “Whether it seems applicable to your own project”

## Overall Flow

The overall steps are as follows:

**① Install Salesforce CLI**

**② Install VS Code + Salesforce Extension Pack**

**③ Log in to a Salesforce Org (Authentication)**

**④ Create a project**

**⑤ Place the following under** `force-app/main/default/`

1. **Apex**
2. **LWC**
3. **LightningTypeBundle**

**⑥ Deploy**

**⑦ Configure the Agentforce Action**

Let’s go through each step one by one.

## ① Install Salesforce CLI

To perform Salesforce development, first install [**Salesforce CLI**](https://developer.salesforce.com/tools/salesforcecli).

After installation is complete, open a terminal  
(Windows: PowerShell / macOS・Linux: Terminal)  
and verify that it is installed correctly.

```
sf --version
```

## ② Install VS Code + Salesforce Extensions

Next, install [**Visual Studio Code (VS Code)**](https://code.visualstudio.com/download) as the development environment.

After installing VS Code, launch it and install the **Salesforce Extension Pack**.

**Steps**

1. Click **Extensions** from the left menu
2. Enter “**Salesforce Extension Pack**” in the search box and install the displayed extension

This extension pack includes the following:

- **Apex**
- **Lightning Web Components (LWC)**
- **Salesforce CLI integration (SFDX)**

> *※ There is no need to search for and configure individual extensions.*

## ③ Log In to Salesforce Org (Authentication)

Next, log in (authenticate) to a Salesforce Org from Salesforce CLI.  
The login destination is assumed to be a Sandbox or Dev Org.

![]()

## Steps

1. Launch VS Code
2. From the menu, select:  
   **Terminal → New Terminal**
3. Run the following command in the terminal to open the login screen:

**For Sandbox login**

```
sf org login web --instance-url https://test.salesforce.com
```

**For Production or Dev Org login**

```
sf org login web
```

When the login screen opens, log in to Salesforce as usual.  
Once authentication succeeds, Org information will be displayed in the terminal.  
(*It may take about one minute for it to appear.*)

![]()

You can also confirm a successful login with the following command:

```
sf org list
```

If the logged-in Org is displayed in the list, the setup is complete.

## ④ Create a Salesforce Project

### Create a Working Folder

1. Create a working folder on your local PC.  
(Example below is for Windows.)

![]()

2. Open the VS Code terminal and enter the following command to move to the working folder (`work`).

```
C:\work
```

### Generate a Salesforce Project

1. While in the working folder (`work`), run the following command in the VS Code terminal.

```
sf project generate --name agentforce-flight
```

2. The generated structure will look like this:

```
C:\work\  
 └─ agentforce-flight\  
     ├─ force-app\  
     ├─ sfdx-project.json  
     └─ ...
```

3. This command automatically generates a full Salesforce development project under the `work` directory.

![]()

### Open the Project in VS Code

1. Enter the following command to move into the project folder.

```
cd agentforce-flight
```

2. Enter the following command to open the project in VS Code

```
code .
```

3. VS Code will open with the project as the working directory.  
We will place the sample code here.

```
agentforce-hotel/  
 ├─ force-app/  
 │   └─ main/  
 │       └─ default/  
 ├─ sfdx-project.json  
 └─ ...
```

### ⑤-1 Place Apex Under `force-app/main/default/`

Drag and drop the files downloaded from the official page into the local `classes` folder.

Once placed, VS Code will automatically reflect them, and the class files will be recognized within the project.

> *The sample can be downloaded from* [*here (apexClass.zip)*](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/apexClassExample.zip)*.*

### ⑤-2 Place LWC Under `force-app/main/default/`

From the official page, download the following under the `lwc` directory:

- `flightDetails` folder (for output)
- `flightRequestFilter` folder (for input)

Drag and drop them directly into the `lwc` folder.

Once the folders are placed, VS Code will automatically recognize the files without any additional actions.

> *Sample data can be downloaded from* [*here (flightResponseCLTandLWC.zip / output)*](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/flightResponseCLTAndLWCExample.zip) *and* [*here (flightFiltersCLTandLWC.zip / input)*](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/flightFilterCLTAndLWCExample.zip)*.*

Confirm that both folders (output and input) are stored.

### ⑤-3 Place `lightningTypes` Under `force-app/main/default/`

Since the `lightningTypes` folder does not yet exist, first create a new folder named `lightningTypes` under `default`.

Next, from the official page, download the following under `lightningTypes`:

- `flightResponse` folder (for output)
- `flightFilter` folder (for input)

Drag and drop them directly into the `lightningTypes` folder you just created.

Once placed, VS Code will automatically reflect them, and the added Lightning Types will be recognized in the project.

> *Sample data can be downloaded from* [*here (flightResponseCLTandLWC.zip / output)*](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/flightResponseCLTAndLWCExample.zip) *and* [*here (flightFiltersCLTandLWC.zip / input)*](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/flightFilterCLTAndLWCExample.zip)*.*  
> ※ These are the same ZIP files as the LWC samples.

Confirm that both folders (output and input) are stored.

At this point, the input-side display does not change much.  
Of course, it does change, but it will likely feel like “What actually changed?”

![]()

**Before change**

So, let’s modify the HTML and CSS.

Overwrite and save `flightRequestFilter.html` under `lwc` in VS Code with the following:

```
<template>  
    <lightning-card class="price-card">  
        <div class="header">  
            💰 <span class="title">Price & Discount</span>  
        </div>  
  
        <div class="content">  
            <lightning-input   
                label="Price (between 1,000 and 20,000)"  
                name="price"  
                value={price}  
                type="number"  
                min="1000"  
                max="20000"  
                step="1"  
                onchange={handleInputChange}  
                read-only={readOnly}>  
            </lightning-input>  
  
            <lightning-input   
                label="Discount Percentage (0% to 100%)"  
                name="discountPercentage"  
                value={discountPercentage}  
                type="number"  
                min="0"  
                max="100"  
                step="1"  
                onchange={handleInputChange}  
                read-only={readOnly}>  
            </lightning-input>  
        </div>  
    </lightning-card>  
</template>
```

Overwrite and save `flightRequestFilter.css` under `lwc` in VS Code with the following:

```
.price-card {  
    border-radius: 12px;  
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);  
}  
  
.header {  
    font-size: 1.1rem;  
    font-weight: 600;  
    padding: 12px 16px;  
    background: linear-gradient(90deg, #e3f2fd, #f9fbff);  
    border-bottom: 1px solid #d8dde6;  
}  
  
.content {  
    padding: 16px;  
}
```

### ⑥ Deploy to Salesforce

After placing all code, run the following command.  
Replace `[username]` with the username currently logged in to the Salesforce Org.  
Do not include the brackets.

```
sf project deploy start --verbose -o [username]
```

This starts the deployment. When deployment succeeds:

- **Apex**
- **LWC**
- **LightningTypeBundle**

will all be registered in the org.

### ⑦ Configure Agentforce Action

1. First, launch **Agentforce Employee Agent** and create a new topic.

2. As the topic description, enter: **I’d like to use this topic to find flights.**

3. This time, do not customize anything. Click **Next** to create the topic.

4. Finish.

## Add an Action

1. Open the created topic, and from the **Actions** tab, add a new action.

2. Select **Apex** as the reference action type.  
※ The Apex class used here has already been deployed from VS Code.

3. Select **Invocable Method** as the reference action category.

4. Select **Find Flights** as the reference action and click **Next**.

## Agent Action Configuration

### Agent Action Instructions

Use this action to find available hotels when the user provides a city, a check-in date, and a check-out date.

### Loading Text

Searching for available hotels…

### checkInDate — Instructions (Input)

Enter the check-in date for your stay in YYYY-MM-DD format.

- ☑ Require input
- ☑ Collect data from user

### checkOutDate — Instructions (Input)

Enter the check-out date for your stay in YYYY-MM-DD format.

- ☑ Require input
- ☑ Collect data from user

### city — Instructions (Input)

Enter the name of the city where you want to search for hotels.

- ☑ Require input
- ☑ Collect data from user

### hotels — Instructions (Output)

Returns a list of available hotels that match the specified criteria.

- ☑ Show in conversation

## Verify Behavior with Standard Lightning Types

1. First, leave **Output Rendering** set to the default:  
`@apexClassType/c__AvailableFlight`.

> *This is to confirm the display using standard Lightning Types.  
> A display like the one on the* ***left*** *is expected.*

2. Also leave **Input Rendering** on the input side set to the default  
`@apexClassType/c__FlightRequestFilter`.

**Why use this input form in the first place?**

Without Custom Lightning Types:  
 → The LLM may decide to “ask via text”.

With Custom Lightning Types:  
 → The LLM understands “this is a form input”,  
 and inputs are collected via UI components instead of text.

As a result, without going through the LLM’s interpretation, structured data is passed directly to Apex,  
and the UX shifts from “understanding sentences” to “entering accurate values”.

3. After saving the settings, refresh the screen once with **F5** and display the preview.  
Enter **Find Flights** in the input field.

4. The input form appears. Enter the following values:

- **originCity**  
  Tokyo
- **destinationCity**  
  New York
- **dateOfTravel**  
  2026/03/15

5. You can also confirm that the filter section is displayed as an input form, but this is still not using Custom Lightning Types.  
Enter the following values and click **Submit**:

- **discountPercentage**  
  20
- **price**  
  (blank)

> *In this sample, the results are hard-coded and returned regardless of the search criteria.*

> ***Note:*** *This form display is enabled only when* ***Collect data from user*** *is checked.  
> If it is not checked, the UI will switch to a text-based question format.*

6. As a result, flight information is displayed, but the output is still not using Custom Lightning Types.

## Switch to Custom Lightning Types

1. Next, to override the output display with Custom Lightning Types, delete this action once and recreate it.

2. The action creation steps are the same as before, but for **aFlight Output Rendering**, select **FlightResponse**.  
With this setting, the output is overridden using a renderer.

> *With this change, a display like the one on the* ***right*** *is expected.*

3. Also, for **filters** on the input side, select **FlightFilter** to override the input using an editor.

## Final Verification

1. After saving the settings, refresh the screen again with **F5** and check the preview.  
Enter **Find Flights** as before.

2. Enter the same values as before:

- **originCity**  
  Tokyo
- **destinationCity**  
  New York
- **dateOfTravel**  
  2026/03/15

You should see that the filter section display has changed and now appears as a slightly richer UI.  
Enter the following values and click **Submit**:

- **discountPercentage**  
  20
- **price**  
  (blank)

(If you overwrote the HTML and CSS as arranged by me, you should see “Price & Discount” displayed as shown below.)

![]()

3. You can now confirm that the output is also displayed with the intended custom design.  
This means the configuration was successful.

## Conclusion

In this article, we confirmed how to fully control Agentforce from input to output by using Custom Lightning Types with editor and renderer overrides.

By using Custom Lightning Types:

- You can obtain accurate values from structured UI without relying on text input
- You can display output with the intended design

Although the design and implementation difficulty is higher,  
this is a very effective approach for business use cases and scenarios that require accuracy.

First, try running the official samples,  
and determine whether this approach can be applied to your own use case.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
