# SFMC Tips #233 : Agentforce: Custom Lightning Types (Collection Renderer Override)

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-233-agentforce-custom-lightning-types-collection-renderer-override-c3b7ad840303

---

# SFMC Tips #233 : Agentforce: Custom Lightning Types (Collection Renderer Override)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c3b7ad840303---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c3b7ad840303---------------------------------------)

10 min read

·

Jan 11, 2026

--

Photo by [shche\_ team](https://unsplash.com/@shche_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Agentforce, standard Lightning types are used by default, so the UI tends to be relatively simple.  
However, by overriding the standard UI and using **custom Lightning types**, you can customize the responses of custom agent actions into a richer, more intuitive, and easier-to-understand user interface.

As of the time of writing this article, custom Lightning types are supported by the following agents:

- Agentforce Service Agent (Enhanced Chat v2)
- Agentforce Employee Agent

In terms of the UI concept, the relationship is as follows: the left side represents the standard UI, while the right side represents a custom UI that overrides the standard UI.

<https://developer.salesforce.com/docs/ai/agentforce/guide/lightning-types-custom.html>

## Quickly Try It with Official Samples

This setup can be easily verified using samples provided in Salesforce official documentation.  
Because the sample data is **hard-coded**, there is no need to create new objects or records for testing.

### Official Samples (Two Types)

1. **Override Editor + Renderer**  
   <https://developer.salesforce.com/docs/ai/agentforce/guide/lightning-types-example-full-editor-renderer.html>
2. **Override Collection Renderer**  
   <https://developer.salesforce.com/docs/ai/agentforce/guide/lightning-types-example-collection-renderer.html>

> *Note: Sample data is provided on each site, and we will use it as-is in this article.*

## Differences Between the Two Approaches

### 1. Editor + Renderer Override

This approach allows comprehensive control over both the input UI and the output UI.  
However, it requires designing everything from input to output.  
While it offers a high degree of freedom in design and implementation, the **difficulty level is higher**.

### 2. Collection Renderer Override

This approach focuses on displaying multiple records (collections) and mainly customizes the **output side**.  
It often does not involve customizing the input UI, making it **relatively easier to implement**.

In this article, I will focus on the more approachable option:  
**② Collection Renderer Override**, and walk through its implementation steps.

> *By reviewing these steps, even just understanding the approximate level of difficulty should help when considering whether to implement this approach.*

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

To develop with Salesforce, you first need to install [**Salesforce CLI**](https://developer.salesforce.com/tools/salesforcecli).

After installation, open a terminal  
(Windows: PowerShell / macOS・Linux: Terminal) and verify the installation:

```
sf --version
```

If the version number is displayed, the Salesforce CLI installation is complete.

## ② Install VS Code + Salesforce Extensions

Next, install [**Visual Studio Code (VS Code)**](https://code.visualstudio.com/download) as your development environment.

After installing VS Code, launch it and install the **Salesforce Extension Pack**.

### Steps

1. Click **Extensions** from the left menu
2. Enter **Salesforce Extension Pack** in the search box and install it

This extension pack includes:

- **Apex**
- **Lightning Web Components (LWC)**
- **Salesforce CLI integration (SFDX)**

> *There is no need to search for and configure each extension individually.*

## ③ Log In to a Salesforce Org (Authentication)

Next, log in to a Salesforce Org using Salesforce CLI.  
This example assumes a Sandbox or Dev Org.

![]()

### Steps

1. Launch VS Code
2. From the menu, select:  
   **Terminal → New Terminal**
3. Run the following command in the terminal to open the login screen:

**For Sandbox**

```
sf org login web --instance-url https://test.salesforce.com
```

**For Production or Dev Org**

```
sf org login web
```

When the login screen appears, log in to Salesforce as usual.  
If authentication is successful, Org information will be displayed in the terminal.

![]()

You can also confirm the login with the following command:

```
sf org list
```

If your logged-in Org appears in the list, you are ready to proceed.

## ④ Create a Salesforce Project

### Create a Working Folder

1. Create a working folder on your local PC.  
(Example below is for Windows.)

![]()

2. Open the VS Code terminal and move to the working folder:

```
cd C:\work
```

### Generate a Salesforce Project

1. While in the working folder, run the following command:

```
sf project generate --name agentforce-hotel
```

2. The generated structure will look like this:

```
C:\work\  
 └─ agentforce-hotel\  
     ├─ force-app\  
     ├─ sfdx-project.json  
     └─ ...
```

3. This command automatically generates a full Salesforce development project under the `work` directory.

![]()

### Open the Project in VS Code

1. Move to the project folder:

```
cd agentforce-hotel
```

2. Open the project in VS Code:

```
code .
```

3. VS Code opens with the project workspace.  
We will place the sample code here.

```
agentforce-hotel/  
 ├─ force-app/  
 │   └─ main/  
 │       └─ default/  
 ├─ sfdx-project.json  
 └─ ...
```

## ⑤-1 Place Apex in `force-app/main/default/`

Drag and drop the files downloaded from the official site into the local **classes** folder.

Once placed, they are automatically reflected in VS Code and recognized as class files in the project.

> *The sample can be downloaded from here:* [***apexClass.zip***](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/apexClassesExample.zip)

## ⑤-2 Place LWC in `force-app/main/default/`

Drag and drop the **hotelDetails** folder under LWC from the official download directly into the **lwc** folder.

Once placed, the files are automatically recognized in VS Code without any additional steps.

> *The sample can be downloaded from here:* [***hotelLWCandCLT.zip***](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/hotelLWCAndCLTExample.zip)

## ⑤-3 Place lightningTypes in `force-app/main/default/`

Since the **lightningTypes** folder does not exist yet, first create a folder named **lightningTypes** under `default`.

Next, drag and drop the **hotelResponse** folder from the downloaded **lightningTypes** directory into the newly created **lightningTypes** folder.

Once placed, the added Lightning Type is automatically recognized in the project.

> *The sample can be downloaded from here:* [***hotelLWCandCLT.zip***](https://resources.docs.salesforce.com/rel1/doc/en-us/static/misc/hotelLWCAndCLTExample.zip) *Note: This ZIP also contains the LWC files.*

## ⑥ Deploy to Salesforce

After placing all code, run the following command.  
Replace `[username]` with the username of the Salesforce Org you are currently logged in to.  
Do not include the brackets.

```
sf project deploy start --verbose -o [username]
```

This starts the deployment.  
 If deployment succeeds, the following will be registered in the org:

- Apex
- LWC
- LightningTypeBundle

## ⑦ Configure the Agentforce Action

### Create a Topic

1. Launch **Agentforce Employee Agent** and create a new topic.

2. For the topic description, enter:  
**I’d like to use this topic to find hotels.**

3. Without further customization, click **Next** and create the topic.

4. Finish.

### Add an Action

1. Open the created topic and add a new action.

2. Select **Apex** as the reference action type.

> *The Apex class used here has already been deployed from VS Code.*

3. Select **Invocable Method** as the reference action category.

4. Select **Find hotels** as the reference action and click **Next**.

## Agent Action Configuration

### Agent Action Instructions

Use this action to find available hotels when the user provides a city, a check-in date, and a check-out date.

### Loading Text

Searching for available hotels…

### checkInDate — Instructions (Input)

Enter the check-in date for your stay in **YYYY-MM-DD** format.

- ☑ Require input
- ☑ Collect data from user

### checkOutDate — Instructions (Input)

Enter the check-out date for your stay in **YYYY-MM-DD** format.

- ☑ Require input
- ☑ Collect data from user

### city — Instructions (Input)

Enter the name of the city where you want to search for hotels.

- ☑ Require input
- ☑ Collect data from user

### hotels — Instructions (Output)

Returns a list of available hotels that match the specified criteria.

- ☑ Show in conversation

## Verify with Standard Lightning Type

1. First, leave **Output Rendering** set to the default:  
`@apexClassType/c__Hotel`

2. This is to confirm the display using the standard Lightning Type.  
A display like the one on the left is expected.

3. Save the settings, refresh the screen with **F5**, and open the preview.  
Enter **Find Hotels** in the input field.

4. The input form appears. Enter the following values:

- city: Hyderabad (*any value is acceptable*)
- checkInDate: any
- checkOutDate: any

> *In this sample,* ***two hard-coded results*** *are returned regardless of the search conditions.*

> ***Note:*** *This form is displayed only when* ***Collect data from user*** *is checked.  
> If it is not checked, the interaction will be text-based.*

5. Two hotel results are displayed, but this is **not yet using the Custom Lightning Type**.

### Switch to Custom Lightning Type

1. To override the output with a Custom Lightning Type, delete the action once and recreate it.

2. The action creation steps are the same as before, but select **HotelResponse** for **Output Rendering**.  
This enables output override using the collection renderer.

3. A display like the one on the right is expected.

### Final Verification

1. Save the settings, refresh again with **F5**, and open the preview.  
Enter **Find Hotels** as before.

Enter:

- City
- Check-in date
- Check-out date

and submit.

![]()

2. The output is displayed with the intended custom design.  
 This confirms the configuration was successful.

## Conclusion

This time, we implemented and verified **Agentforce Custom Lightning Types (Collection Renderer Override)** using official samples.

Because this approach customizes **only the output UI** and does not touch the input UI, it allows you to enrich the UI with a relatively low difficulty level.

In practice, the implementation consists of building the layout with HTML included in the sample and styling it with CSS.  
 For developers with LWC experience, this approach is intuitive and easy to understand.

Start by getting a feel for UI customization with this method, and then decide whether to move on to the Editor + Renderer approach as needed.

For this verification, we used the **Agentforce Employee Agent** for a simple functional check.  
If you want to validate this with the **Agentforce Service Agent (Enhanced Chat v2)**, there are a few important points to note.

First, to test with Enhanced Chat v2, you need to create a dedicated permission set and grant the service agent access to the required Apex classes.

In this sample, access to the following **six Apex classes** is required:

- Hotel
- HotelCategory
- HotelRequest
- HotelReservation
- HotelResponse
- Room

In addition, the Service Agent preview provided in **Agentforce Builder** behaves the same as **v1**, so the results of this verification cannot be confirmed within Agentforce Builder itself.  
When testing, be sure to switch Enhanced Chat to **v2** and verify the behavior in the actual runtime screen.

Below is an example of how it appears in **Agentforce Service Agent (Enhanced Chat v2)**.

![]()

That’s all for this article.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
