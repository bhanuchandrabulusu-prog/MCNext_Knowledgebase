# SFMC Tips #124 : SFMC Automation Viewer: New Journey Activity Search Feature Added

**Source:** https://medium.com/@marketingcloudtips/sfmc-automation-viewer-new-journey-activity-search-feature-added-a686a9f10fea

---

# SFMC Tips #124 : SFMC Automation Viewer: New Journey Activity Search Feature Added

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a686a9f10fea---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a686a9f10fea---------------------------------------)

5 min read

·

May 30, 2025

--

Photo by [Apothecary 87](https://unsplash.com/@apothecary87?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

A new feature has been introduced to the **SFMC Automation Viewer**, a **Google Chrome extension** created by [**Matheswaran Kanagarajan**](https://www.linkedin.com/in/mathesk/), allowing users to identify which Journey Builder is utilizing a specific data extension. Let’s review this exciting update!

### Installing SFMC Automation Viewer

You can install SFMC Automation Viewer from the link below:

[## SFMC Automation Viewer - Chrome Web Store

### View SFMC automation details without pausing active automations.

chromewebstore.google.com](https://chromewebstore.google.com/detail/sfmc-automation-viewer/bfdjgmcdnopdhpkfiolfmkcgeadgapmb?source=post_page-----a686a9f10fea---------------------------------------)

📝 *At the time of writing, version 0.1.1 is the latest release.*

## Connection Setup Steps

### **1. Open Automation Studio**

To connect SFMC Automation Viewer to Marketing Cloud Engagement, first, open **Automation Studio**.

*Note:* If you attempt to start without opening Automation Studio, the connection status in the upper-right corner will show **“Not Connected”**, and the setup won’t complete.

### **2. Verify Connection**

While Automation Studio is open, confirm the connection in the SFMC Automation Viewer. A successful connection will display a green icon in the connection status, based on your environment stack.

### **3. Navigate to Journey Builder**

Once the connection is established, switch from Automation Studio to **Journey Builder**.

### **4. Use Journey Activity Details**

Return to the SFMC Automation Viewer and click **“Journey Activity Details”**. The new feature is now ready to use!

## Search Methods

Next, let’s explore the search functionality within the SFMC Automation Viewer.

The following five criteria are primarily used for searching:

1. **Data Extension Name**
2. **Published Interaction Count**
3. **Type**
4. **Category**
5. **Scheduled on or after today**

*Note:* Event Definition Name and Event Definition Key are typically harder to retrieve.

### 1. Data Extension Name

Specify the name of the data extension used as the journey’s entry source. This search functionality includes all data extensions tied to event definitions, including those used in “Wait Until Event” activities.

💡 *Input Tip*: Ensure accurate case-sensitive input, as the search is case-sensitive.

### 2. Published Interaction Count

Filter by the journey’s current status (active or inactive). For example, even draft journeys with saved entry sources can be included in results using the “Not Active” condition.

### 3. Type

Specify the type of journey entry event. For example, select **Email Audience** for entry events using a data extension.

**Key Types:**

- **Email Audience**: Standard data extension sends
- **Automation Audience**: Sends linked to Automation Studio
- **API Event**: Triggered sends via API events
- **CloudPages**: Sends triggered by CloudPages
- **Salesforce Data**: Sends leveraging Salesforce Data

### 4. Category

Define the category of your search target:

- **Audience**: Covers Email Audience and Automation Audience types
- **Event**: Includes all other event types

### 5. Scheduled on or after today

Search for journeys scheduled to end in the future.

💡 **Pro Tip**:  
 This API not only retrieves entry source details but also journey start and end times. For example:

- Leave **Data Extension Name** blank
- Set **Published Interaction Count** to **Active**
- Enable this checkbox to display all currently active journeys in detail.

## Search Results

For instance, based on the criteria above, the search results might include:

- **Journey Name**: Weekdays
- **Data Extension Name**: master\_subscribers
- **Journey Start Date and Time**: Dec 14, 2023, 5:00 PM
- **Journey End Date and Time**: Dec 14, 2073, 5:00 PM
- **Send Frequency**: Weekdays

Additionally, you can use **Ctrl + F** for keyword search directly on the page to quickly locate the desired information. Make use of this feature to streamline your searches!

## Troubleshooting

If the search functionality does not work after setup, it’s possible that the configured **stack** is incorrect. Follow the steps below to verify and fix the issue:

### 1. Go to the Settings Screen

Navigate to the **Settings** page in the SFMC Automation Viewer.

### 2. Click the Gear Icon

Click the **gear icon** displayed on the right side of the screen.

### 3. Select the Correct Stack and Save

Choose the correct stack that matches your environment and click the **“Save”** button to update the settings.

## Additional Updates: Enhanced View Activity Details

With the latest version of SFMC Automation Viewer, the existing **View Activity Details** feature has been significantly improved for ease of use.

### 1. Click the Query Tab

To review queries created in Automation Studio, go to **View Activity Details** and click the **Query** tab.

### 2. View All Queries

All queries created in Automation Studio are displayed in the list.

### 3. Use Ctrl + F for Quick Searches

- **Data Extension Usage**  
   You can search for specific data extensions and see which queries are using them by using **Ctrl + F** on the screen.
- **Query Text Search**  
   Search within query texts to quickly locate target data extensions or review the query content itself.

This enhanced functionality greatly improves the management of data extensions and queries, making it incredibly efficient and user-friendly.

Give it a try — you’ll find it super useful!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
