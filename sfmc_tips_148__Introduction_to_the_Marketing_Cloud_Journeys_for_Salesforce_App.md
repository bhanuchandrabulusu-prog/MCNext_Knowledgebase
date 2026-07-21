# SFMC Tips #148 : Introduction to the Marketing Cloud Journeys for Salesforce App

**Source:** https://medium.com/@marketingcloudtips/introduction-to-the-marketing-cloud-journeys-for-salesforce-app-a5f1c6edde3c

---

# SFMC Tips #148 : Introduction to the Marketing Cloud Journeys for Salesforce App

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a5f1c6edde3c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a5f1c6edde3c---------------------------------------)

9 min read

·

Jul 9, 2025

--

Photo by [Syuhei Inoue](https://unsplash.com/@_______life_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Released in June 2020 by Salesforce Labs, the unofficial Salesforce app **Marketing Cloud Engagement Journeys for Salesforce** allows you to easily view which **Journeys** a **Contact** or **Lead** is currently in — right from their record page in Salesforce. Moreover, you can also easily **remove them from a Journey** directly from the same screen.

When removing a contact from a Journey using this app, it behaves exactly the same as removing them via the **Journey Health** “Remove from journey” button. The contact is typically excluded within about **one minute**, and when checking the Journey history, the action is recorded as an API-based removal (`ContactExitedByApi`).

One important point to note:  
 This app **does not display a history of past Journeys** a contact has entered. It only shows **currently active Journeys**, so please keep that in mind.

If you’re considering trying out the app, I recommend watching the video below for a clear overview of the user interface and how it works.

In this article, I’ll walk you through the detailed steps for setting up this app.

## Prerequisites

Please ensure that the person performing the setup meets the following requirements:

- Salesforce Administrator
- Marketing Cloud Administrator

## Install the AppExchange Package

1. Go to the following link and click **“Get It Now”**:

[## Marketing Cloud Journeys for Salesforce | Salesforce AppExchange

### View the journey a contact, lead, case, or account is in, directly from Marketing Cloud Engagement. Give visibility to…

appexchange.salesforce.com](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000FZBjRUAX&source=post_page-----a5f1c6edde3c---------------------------------------)

2. Follow the on-screen instructions to start the installation.

3. Choose to **Install for All Users**.

4. Once the installation is complete, you will see a confirmation screen.

## Create a Package in Marketing Cloud

1. In Marketing Cloud, navigate to the **business unit** where the journeys are located. Go to **Setup** > **Apps** > **Installed Packages**, and click **New**.

2. Name the package **“Marketing Cloud Journeys for Salesforce”**, then click **Save**.

![]()

3. Click **Add Component**.

4. Select **API Integration** > **Web App**, then click **Next**.

![]()

5. For the **Redirect URI**, you can enter a temporary placeholder like `https://google.com`. (This will be updated later, so any valid URL is fine for now.)

![]()

6. Select the following **scopes**, then click **Save**:  
 ✅ Offline Access (You can leave the Refresh Token Lifetime as 30 days)  
 ✅ Automation — Journeys — Read and Execute  
 ✅ Contacts — List and Subscribers — Read  
 ✅ Data — Data Extensions — Read  
 ✅ Automation — Journeys — Activate/Stop/Pause/Resume/Send/Schedule

⚠️ **Note:** The official setup guide only shows the first four scopes.  
 However, the **fifth scope is also required**. If it’s missing, you will encounter the following error when clicking the **Remove** button:  
 `"Error: An error has occurred while removing from journey. Try again later."`

A solution for this issue is provided at the end of this article.

![]()

7. Once saved, a **Client Secret** will be generated. **Be sure to copy and store it immediately,** as it won’t be shown again. After recording it, click **Finish**.

![]()

8. On the next screen, copy and store both the **Client ID** and the **Authentication Base URI**.

## Configure the Authentication Provider in Salesforce

1. Next, in **Salesforce CRM**, open **Setup**, use Quick Find to search for **“Auth”**, and click **Auth. Providers**. Then, click the **New** button.

2. For the **Provider Type**, select **Open ID Connect**.

3. Fill in the required fields as shown below, then click **Save**:

- **Name**: `SFMC Journeys`
- **URL Suffix**: `SFMC_Journeys` (This will auto-populate)
- **Consumer Key**: The **Client ID** generated in the Marketing Cloud package
- **Consumer Secret**: The **Client Secret** generated in the Marketing Cloud package
- **Authorize Endpoint URL**:  
   `https://xxxxx.auth.marketingcloudapis.com/v2/authorize`
- **Token Endpoint URL**:  
   `https://xxxxx.auth.marketingcloudapis.com/v2/token`

4. After saving, scroll down the resulting page and **copy the Callback URL**.

## Set the Callback URL in Marketing Cloud

1. Switch back to **Marketing Cloud**, go to **Installed Packages**, open the package you created earlier, and click **Edit** under **API Integration**.

2. Replace the previously entered dummy redirect URL (e.g., `https://google.com`) with the **Callback URL you copied from Salesforce**, then click **Save**.

![]()

## Configure Named Credentials in Salesforce

1. Next, go back to **Salesforce CRM** and **switch to Salesforce Classic**.

2. Navigate to **Setup**.

3. In the Quick Find box, search for **Named Credentials**, open the page, and click **New Named Credential**.

4. Fill in the fields as follows:

- **Label**: `Salesforce Marketing Cloud`
- **Name**: `Salesforce_Marketing_Cloud`

⚠️ *This exact spelling is critical, including the underscore.*

- **URL**: `https://xxxxx.rest.marketingcloudapis.com`

⚠️ *Do not include a trailing slash (*`/`*) at the end.*

- **Identity Type**: `Named Principal`
- **Authentication Protocol**: `OAuth 2.0`
- **Authentication Provider**: Select the provider you just created — `SFMC Journeys`
- **Start Authentication Flow on Save**: ✅ *Check this box*
- **Generate Authorization Header**: ✅ *Check this box*

5. Click **Save**, then make sure the **Authentication Status** shows **“Authenticated”**.

6. Once the setup is complete, switch back from **Salesforce Classic** to **Lightning Experience**.

## Add the Component to the Record Page

1. Open a **Contact** or **Lead** record, then click **Settings** in the top-right corner and select **Edit Page**.

2. Drag and drop the **Marketing Cloud Journeys** custom component onto the canvas.

3. Select the field that contains the **Contact Key**.

![]()

4. Click **Save**.

![]()

⚠️ **Note:**  
 There is an optional setting to **allow or disallow contact removal from Journeys**. If you choose not to allow this, the **“Stop”** button will not be shown.

![]()

## Supporting Multiple Business Units

1. In Marketing Cloud, go to the **Installed Packages** screen, open the “**ACCESS”** tab, and grant access to users of the additional **Business Units** you want to support.

2. Navigate to the **business unit** you want to add, and retrieve the **MID** from the screen. Once you’ve obtained the MID, **keep that business unit open**.

3. Switch to **Salesforce Classic** and create a new **Named Credential**.  
 (The steps are the same as described earlier.)

Example:

- **Label**: `Salesforce Marketing Cloud 534000779`
- **Name**: `Salesforce_Marketing_Cloud_534000779`

⚠️ **Note:**  
 The **Label** can be anything you like, but the **Name** must strictly follow the naming convention shown above. `534000779` is the MID used in my environment — replace it with your own MID.

With this configuration, the **Marketing Cloud Journeys** component will work across **multiple business units**, allowing you to view active Journeys and remove contacts accordingly for each business unit.

## Test the Integration

1. Open the **record page** of a contact who has already entered a Journey.  
 As shown below, the contact is currently active in two Journeys.

Note: This display is updated **in real time**, so it reflects the contact’s Journey status immediately. As soon as they enter a Journey, it appears here — and once they exit a Journey, it disappears instantly.

2. Click **“Stop”** next to the Journey you want to remove the contact from.

3. Then click the **“Remove”** button.

4. The contact will be successfully removed from the Journey.

5. When checking the Journey’s history, you’ll see that the removal was handled via API — confirming the process was successful!

## Wrapping Up

In this article, I walked through the full setup to integrate **Salesforce CRM** with **Marketing Cloud**, and how to add the **Marketing Cloud Journeys** component to the record page.

The entire configuration can be completed in about **one hour**, so if you’re interested, I highly recommend giving it a try!

## Troubleshooting: Missing Scope Permissions

As mentioned earlier, here’s a quick troubleshooting guide if you encounter the error shown in the image below:

✅ **Required scope not listed in the official manual:**  
 `Automation - Journeys - Activate/Stop/Pause/Resume/Send/Schedule`

If this scope was **omitted**, follow the steps below to resolve the issue:

1. In **Marketing Cloud Engagement**, go to the **Setup** page and add the missing scope.
2. After adding the scope, **wait approximately 10 minutes** to allow the change to propagate.
3. Switch to **Salesforce Classic**, open the **Named Credential** you previously configured.
4. Without changing anything on the screen, simply click **Save**.
5. When prompted with a **confirmation screen**, click **Confirm** to finalize the change and resolve the issue.

![]()

If you run into any issues, refer to this process to help get things back on track.

In the **next article**, I’ll explore how to **search and remove contacts from Journeys manually** — in scenarios where this app isn’t available, or if you’re not using Salesforce CRM at all.

That’s all for now!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
