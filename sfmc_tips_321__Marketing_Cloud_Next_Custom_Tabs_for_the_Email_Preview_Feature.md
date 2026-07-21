# SFMC Tips #321 : Marketing Cloud Next: Custom Tabs for the Email Preview Feature

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-custom-tabs-for-the-email-preview-feature-edc57cc47506

---

# SFMC Tips #321 : Marketing Cloud Next: Custom Tabs for the Email Preview Feature

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--edc57cc47506---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--edc57cc47506---------------------------------------)

9 min read

·

Jul 13, 2026

--

Photo by [Rombo](https://unsplash.com/@rombo_guitar_picks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Editions, you can add custom tabs to the **Preview and Test** screen for email content by using Lightning Web Components (a Salesforce framework for creating screens, buttons, tables, graphs, and other UI components).

In this article, we will use Agentforce Vibes IDE (the browser-based version of Visual Studio Code) to create a **Content Check** tab that verifies the following three items:

- Email subject length
- Whether the preheader is empty and its character count
- Whether a Preference Center link exists

Once completed, the following tab will be added to the Marketing Cloud Next preview screen:

```
Preview | Test | Content Check
```

When you open the **Content Check** tab, the following validation results are displayed based on the email currently being previewed.

*Note:* Agentforce Vibes IDE is available only in SDO, Developer Edition, or Sandbox environments for supported editions. It cannot be used in a typical production org.

## Setup Steps

## 1. Enable Agentforce Vibes IDE

First, launch Agentforce Vibes IDE from Salesforce Setup.

### 1. Open Agentforce Vibes

Log in to Salesforce, click the gear icon in the upper-right corner, open **Setup**, and then select **Agentforce Vibes**.

### 2. Accept the Terms of Use

When launching Agentforce Vibes IDE for the first time, the Terms of Use are displayed.

Click **Accept** to start using Agentforce Vibes IDE. These terms apply not only to Agentforce Vibes IDE but also to Salesforce DX tools such as DevOps Center and DX Inspector.

Wait a few minutes until the environment finishes loading.

![]()

In this example, we will build everything without Agentforce assistance because many environments cannot enable the Agentforce feature shown in the red box below. If your environment supports it, feel free to use it.

*Clicking* ***Enable Agentforce*** *enables the AI development assistant in Agentforce Vibes, allowing you to use AI-powered code generation and code review features.*

### 3. Launch Agentforce Vibes IDE

A development environment similar to Visual Studio Code opens in your browser.

**Tip:** During the first launch, you may see an error such as **“Apex Language Server Extension couldn’t create connection to server”** in the lower-right corner. If this happens, press **Ctrl + Shift + P** and run **Developer: Reload Window**, which may resolve the issue.

## 2. Create a Salesforce Project

Next, create a Salesforce project to store your Lightning Web Component.

### 1. Open the Command Palette

In Agentforce Vibes IDE, press:

- **Windows:** Ctrl + Shift + P
- **Mac:** Command + Shift + P

The Command Palette appears at the top of the screen.

### 2. Create a Salesforce Project

Enter the following command in the Command Palette:

```
SFDX: Create Project
```

![]()

Select the standard project type.

![]()

For the project name, enter something like:

```
MarketingCloudNextPreviewExtension
```

![]()

Choose a location to save the project, and the Salesforce project will be created.

![]()

**Tip:** *If you launch Agentforce Vibes IDE from Salesforce Setup, it automatically recognizes the target Salesforce org.*

If you leave the screen and later want to return to the **MarketingCloudNextPreviewExtension** project, you can reopen it from **Open File** or **Recent**.

## (Reference) Let Agentforce Generate the LWC

If you would like AI assistance, enter the following prompt into Agentforce Vibes:

```
Create a Lightning Web Component to add to the Preview and Test modal in Marketing Cloud Next.  
  
Name the component contentCheckTab.  
  
The requirements are as follows.  
  
Receive data from Marketing Cloud Next through @api previewData  
Display previewData.emailSubject as the email subject  
Display an error if the email subject is blank  
Display the number of characters in the email subject  
Display a warning if the email subject exceeds 50 characters  
Display previewData.emailPreheader as the preheader  
Display an error if the preheader is blank  
Display the number of characters in the preheader  
Display a warning if the preheader exceeds 100 characters  
Check whether previewData.content contains a link to the preference center  
Display an error if the link is not found  
Finally, display an overall result of either PASS or Needs Revision  
Use Salesforce Lightning Design System classes  
Do not use Apex  
Do not use external APIs  
Configure the lightning__dynamicComponent capability  
Ensure that no JavaScript errors occur if null or undefined is passed  
Create the following three files  
  
contentCheckTab.html  
contentCheckTab.js  
contentCheckTab.js-meta.xml  
  
Before creating the files, explain the implementation approach, and then create the files.
```

Agentforce reviews the requirements and generates the required files.

## 3. Create the Files Manually

In this example, we will manually create the folders and files under the **lwc** directory as follows:

```
force-app/  
└── main/  
    └── default/  
        └── lwc/  
            └── contentCheckTab/（<--- Folder）  
                ├── contentCheckTab.html（<--- HTML File）  
                ├── contentCheckTab.js（<--- JS File）  
                └── contentCheckTab.js-meta.xml（<--- XML File）
```

![]()

The templates for each file are shown below.

## contentCheckTab.html

```
<template>  
    <div class="slds-p-around_medium">  
        <div class="slds-text-heading_medium slds-m-bottom_medium">  
            Content Check  
        </div>  
  
        <template if:true={hasPreviewData}>  
            <section class="slds-box slds-m-bottom_medium">  
                <h2 class="slds-text-heading_small">Subject</h2>  
                <p class="slds-m-top_x-small">{subjectDisplay}</p>  
                <p>{subjectLength} characters</p>  
                <p class={subjectStatusClass}>{subjectStatus}</p>  
            </section>  
  
            <section class="slds-box slds-m-bottom_medium">  
                <h2 class="slds-text-heading_small">Preheader</h2>  
                <p class="slds-m-top_x-small">{preheaderDisplay}</p>  
                <p>{preheaderLength} characters</p>  
                <p class={preheaderStatusClass}>{preheaderStatus}</p>  
            </section>  
  
            <section class="slds-box slds-m-bottom_medium">  
                <h2 class="slds-text-heading_small">  
                    Preference Center  
                </h2>  
                <p class={preferenceCenterStatusClass}>  
                    {preferenceCenterStatus}  
                </p>  
            </section>  
  
            <section class="slds-box">  
                <h2 class="slds-text-heading_small">Overall Result</h2>  
                <p class={overallStatusClass}>{overallStatus}</p>  
            </section>  
        </template>  
  
        <template if:false={hasPreviewData}>  
            <div class="slds-text-color_error">  
                Unable to retrieve preview data.  
            </div>  
        </template>  
    </div>  
</template>
```

## contentCheckTab.js

```
import { LightningElement, api } from "lwc";  
  
const SUBJECT_MAX_LENGTH = 50;  
const PREHEADER_MAX_LENGTH = 100;  
  
export default class ContentCheckTab extends LightningElement {  
    @api previewData;  
  
    get hasPreviewData() {  
        return this.previewData != null;  
    }  
  
    get subject() {  
        return this.previewData?.emailSubject?.trim() || "";  
    }  
  
    get preheader() {  
        return this.previewData?.emailPreheader?.trim() || "";  
    }  
  
    get content() {  
        return this.previewData?.content || "";  
    }  
  
    get subjectDisplay() {  
        return this.subject || "Not provided";  
    }  
  
    get preheaderDisplay() {  
        return this.preheader || "Not provided";  
    }  
  
    get subjectLength() {  
        return Array.from(this.subject).length;  
    }  
  
    get preheaderLength() {  
        return Array.from(this.preheader).length;  
    }  
  
    get isSubjectValid() {  
        return (  
            this.subjectLength > 0 &&  
            this.subjectLength <= SUBJECT_MAX_LENGTH  
        );  
    }  
  
    get isPreheaderValid() {  
        return (  
            this.preheaderLength > 0 &&  
            this.preheaderLength <= PREHEADER_MAX_LENGTH  
        );  
    }  
  
    get hasPreferenceCenter() {  
        const content = this.content.toLowerCase();  
  
        const preferenceCenterPatterns = [  
            "preference",  
            "subscription",  
            "unsubscribe",  
            "manage preferences"  
        ];  
  
        return preferenceCenterPatterns.some((pattern) =>  
            content.includes(pattern)  
        );  
    }  
  
    get subjectStatus() {  
        if (this.subjectLength === 0) {  
            return "The subject is required.";  
        }  
  
        if (this.subjectLength > SUBJECT_MAX_LENGTH) {  
            return `The subject exceeds ${SUBJECT_MAX_LENGTH} characters.`;  
        }  
  
        return "Looks good.";  
    }  
  
    get preheaderStatus() {  
        if (this.preheaderLength === 0) {  
            return "The preheader is required.";  
        }  
  
        if (this.preheaderLength > PREHEADER_MAX_LENGTH) {  
            return `The preheader exceeds ${PREHEADER_MAX_LENGTH} characters.`;  
        }  
  
        return "Looks good.";  
    }  
  
    get preferenceCenterStatus() {  
        return this.hasPreferenceCenter  
            ? "A Preference Center link was found."  
            : "No Preference Center link was found.";  
    }  
  
    get isAllValid() {  
        return (  
            this.isSubjectValid &&  
            this.isPreheaderValid &&  
            this.hasPreferenceCenter  
        );  
    }  
  
    get overallStatus() {  
        return this.isAllValid ? "PASS" : "Needs Revision";  
    }  
  
    get subjectStatusClass() {  
        return this.isSubjectValid  
            ? "slds-text-color_success"  
            : "slds-text-color_error";  
    }  
  
    get preheaderStatusClass() {  
        return this.isPreheaderValid  
            ? "slds-text-color_success"  
            : "slds-text-color_error";  
    }  
  
    get preferenceCenterStatusClass() {  
        return this.hasPreferenceCenter  
            ? "slds-text-color_success"  
            : "slds-text-color_error";  
    }  
  
    get overallStatusClass() {  
        return this.isAllValid  
            ? "slds-text-heading_medium slds-text-color_success"  
            : "slds-text-heading_medium slds-text-color_error";  
    }  
}
```

## contentCheckTab.js-meta.xml

```
<?xml version="1.0" encoding="UTF-8"?>  
<LightningComponentBundle  
    xmlns="http://soap.sforce.com/2006/04/metadata">  
    <apiVersion>66.0</apiVersion>  
    <isExposed>true</isExposed>  
    <capabilities>  
        <capability>lightning__dynamicComponent</capability>  
    </capabilities>  
</LightningComponentBundle>
```

## 4. Configure the Preference Center

The Preference Center URL and identifier strings vary depending on your org and email template configuration.

In this sample, the email is considered to contain a Preference Center if the email content (either as plain text or within a URL) contains any one of the following:

- preference
- subscription
- unsubscribe
- manage preferences

```
get hasPreferenceCenter() {  
    const content = this.content.toLowerCase();  
  
    const preferenceCenterPatterns = [  
        "preference",  
        "subscription",  
        "unsubscribe",  
        "manage preferences"  
    ];  
  
    return preferenceCenterPatterns.some((pattern) =>  
        content.includes(pattern)  
    );  
}
```

If you know the actual Preference Center URL used in your organization, it is more reliable to include part of that domain or URL in the matching conditions.

For example, if every Preference Center URL contains:

```
preferences.example.com
```

then update the matching conditions as follows:

```
const preferenceCenterPatterns = [  
    "preferences.example.com",  
    "manage preferences"  
];
```

## 5. Deploy the LWC to Your Org

After confirming the contents, deploy the LWC to your Salesforce org.

### Deploy from the File Explorer

Right-click the **contentCheckTab** folder and select:

```
SFDX: Deploy This Source to Org
```

## 6. Obtain the ID of the Deployed LWC

Deploying the LWC alone does not make it appear in the Marketing Cloud Next preview screen.

Open the **Developer Console** from Salesforce Setup.

In the Developer Console, open **Query Editor** and enable **Use Tooling API**.

*The* ***LightningComponentBundle*** *object is not a standard data object like Contact or Case. It stores metadata for deployed Lightning Web Components, so* ***Use Tooling API*** *must be enabled.*

Run the following query:

```
SELECT Id, DeveloperName, IsExposed, NamespacePrefix  
FROM LightningComponentBundle  
WHERE DeveloperName = 'contentCheckTab'
```

Record the 18-character **Id** returned by the query.

![]()

*This ID will be used when registering* ***UiPreviewMessageTabDef****.*

## 7. Register UiPreviewMessageTabDef

**UiPreviewMessageTabDef** is metadata used to register which Lightning Web Component should appear as a custom tab in the Marketing Cloud Next **Preview and Test** modal.

Run the following query in the Developer Console Query Editor:

```
SELECT Id, MasterLabel, DeveloperName, TabName, IsActive, SupportedChannel, LightningComponentDefId  
FROM UiPreviewMessageTabDef
```

The query returns zero records if no custom tabs have been registered, which is expected.

Click **Insert Row** once to add a new row.

Enter values similar to the following:

- **Id:** Automatically generated
- **MasterLabel:** Content Check
- **DeveloperName:** ContentCheck
- **TabName:** Content Check
- **IsActive:** true
- **SupportedChannel:** Email
- **LightningComponentDefId:** The contentCheckTab ID copied earlier

After entering the values, click **Save Rows**.

*Once* ***IsActive*** *is set to* ***true****, the tab appears in the Marketing Cloud Next preview screen.*

## 8. Verify the Behavior in Marketing Cloud Next

Open your email content in Marketing Cloud Next and select **Preview and Test**.

Alongside the standard Preview and Test tabs, the following tab appears:

```
Content Check
```

Open the tab and review the validation results.

## Conclusion

In this article, we used Agentforce Vibes IDE as the development environment to add a custom **Content Check** tab to the Marketing Cloud Next **Preview and Test** screen.

Although this is a small sample, it demonstrates how you can freely extend pre-send validation according to your organization’s operational requirements.

For example:

- Brand guideline validation
- Merge field validation
- Broken link detection
- Required content validation
- Custom quality validation based on internal rules

and many other pre-send validation tools can be added directly to the preview screen.

The ability to customize the Marketing Cloud Next preview screen is still a feature that many people are unaware of.

I encourage you to try creating your own custom validation tabs in your environment.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
