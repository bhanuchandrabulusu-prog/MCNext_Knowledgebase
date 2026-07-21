# SFMC Tips #104 : Marketing Cloud Next: Creating a Signup Form

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea

---

# SFMC Tips #104 : Marketing Cloud Next: Creating a Signup Form

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--dcb43bbe9fea---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--dcb43bbe9fea---------------------------------------)

7 min read

·

Apr 23, 2025

--

Photo by [Austin Neill](https://unsplash.com/@arstyy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Marketing Cloud Next** (Marketing Cloud Growth & Advanced Editions) provides an efficient way to capture new leads by creating a “Signup Form”. You can share the form’s URL on social media or include a QR code in printed event advertisements to maximize reach.

This signup form functionality is a powerful tool that comes standard with Marketing Cloud Growth & Advanced Editions. In this article, I’ll walk you through the steps to create and utilize this feature effectively.

## Step-by-Step Instructions

## Create and Save the Form

### 1. Select the Signup Form

On the Campaign Flow page, click **“New Flow”** from the left-hand menu. From the list of templates displayed, select **“Signup Form”**.

### 2. Edit the Registration Form

Click the **“Edit”** button in the **“Start Trigger”** section.

### 3. Add a Data Source

Click **“Add Data Source”** to define the target object for processing through the form.

### 4. Select a Target Object

Choose a target object from the following four options (specify a record type if necessary):

- Account
- Contact
- Lead
- Prospect

### 5. Add Fields

Drag and drop the **“Title”** field from the lead object into the form area.

### 6. Configure Styles

To adjust the padding around the added **“Title”** field, go to the **Style Settings** and select **“Small”** under **Layout > Padding**.

*Note*: The preview screen may show slight size misalignments, but the live landing page will display correctly.

### 7. Save the Form

After reviewing the form’s content, click **“Save”**.

*Note*: At this stage, the form cannot be published. Attempting to publish it will result in the following error.

### 8. Expand the Flow Accordion Menu

Once the form is saved, expand the **“Flow”** accordion menu on the right-hand side.

### 9. Launch Flow Builder

From the dropdown menu, select **“Open in Flow Builder”** to transition to the Flow Builder screen, where you can configure flows linked to the form.

## Create and Activate the Flow

### 1. Configure Flow Builder

Using the **“Signup Form”** flow template automatically places elements like **“Create Record”** and **“Consent Request”** in the flow.

### 2. Edit the “Create Records” Element

Open the **“Create Records”** element.

- If you’ve added new fields to the form, map them accordingly.
- The left-hand side represents the field name on the **Lead object**, and the right-hand side corresponds to the field name on the **form**.

**Tips:** The standard flow template “Signup Form” is designed for lead capture. Even if you create the form for *Contacts* or *Prospects*, the “Create Record” element is still set up for *Leads* by default. You’ll need to manually switch it. **LeadCreation** does not automatically convert into **ContactCreation** or **ProspectCreation**.

**Example Mapping:**

- Left: **“Title”** (field name on the Lead object)
- Right: **“Associated Form > Title”** (field name on the form)

> ***Important:*** *If necessary, configure* ***“Check for Matching Records”*** *to handle potential duplicate lead records. Use conditions such as* ***First Name + Last Name + Email Address*** *to search for matching records, and choose whether to “Update” them or “Skip” them. If this is not configured, an error will occur in the flow, and it will not proceed.*

### 3. Edit the “Consent Request” Element

Open the **“Consent Request”** element.

- Configure the input for channels (e.g., Email, SMS) and communication preferences.
- For the **“Contact Point”** field, select **“Email Address”** retrieved from the form.

### 4. Save the Flow and Check for Errors

Save the flow and ensure no errors are present. If everything looks good, click **“Activate”**.

### 5. Publish the Form

Once the flow is activated, the previously created form will be **published** automatically.

> ***Tips:*** *Flows are activated immediately, but publishing a form may take some time.* ***If you try to publish a landing page while the form is still unpublished, an error will occur****. Make sure the form has been fully published before publishing the landing page. You’ll receive a confirmation email once the form is published.*

## Create and Publish the Landing Page

### 1. Review and Edit the Landing Page

After confirming the flow activation, return to the Campaign Flow page and review the **“Landing Page”** section. Click **“Edit”** to make changes.

### 2. Edit, Save, and Publish the Page

Once the editing page opens, you’ll see the form you previously created integrated into the page. Update the page with compelling visuals and text, such as changing images or adding enticing content. After completing your edits, click **“Save”** and then **“Publish”**.

This concludes the basic setup process.

### 3. Access the Published URL

To obtain the URL of the published landing page, click on the name of the landing page.

### 4. Open the URL Tab

In the landing page settings screen, navigate to the **“URL”** tab.

### 5. Retrieve the Published URL

Within the **“URL”** tab, locate and copy the **“Published URL”** for future reference or sharing.

The URL alias displayed in the public URL is the ending part of the content URL. By default, it is automatically generated based on the “Content Title” and “Content API Name,” but you can change it to a more readable name, such as “holiday-sale”. [**Once the content is published, the alias can no longer be edited**](https://help.salesforce.com/s/articleView?id=mktg.mktg_content_lp_create.htm&type=5), so make sure to update it while it is still in draft status.

### 6. Verify the Landing Page Display

Click the **“Published URL”** to open the landing page. Confirm that the page displays as expected.

## **Adding Users as “Contributors”**

To publish standard Marketing Cloud **forms** or **landing pages**, users must be added as **Contributors**. If you encounter an error when publishing a landing page, it may be because the user has not been added as a Contributor and therefore lacks permission to publish forms. Follow the steps below to add the target user as a Contributor:

1. Go to **Setup** > search for **All Sites**, then open it. Select the **Workspace** to the left of **Marketing Landing Pages**.

2. Click **Administration**.

3. Select **Members**, choose the **Profile** that includes the user you want to add, add them as a member, and save.

4. Next, select **Contributors** and click the **Add Contributor** button.

5. Select the user you want to add and grant them “**Builder” permissions**. After this, they will be able to publish forms and landing pages.

![]()

### Reference: Points to Note When Using SDO (Simple Demo Org)

If a Salesforce partner is using SDO, clicking the published URL of a landing page may result in an error message saying **“URL No Longer Exists”.** This error is caused by **login IP address restrictions**.

![]()

You can resolve this issue by following the steps below. This is explained in detail in the article below.

[## SFMC Tips #105 : Marketing Cloud on Core: How to Resolve Errors on Landing Pages in SDO

### This article is intended for Salesforce partners using Marketing Cloud on Core (Marketing Cloud Growth/Advanced…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-how-to-resolve-errors-on-landing-pages-in-sdo-644dee92aa8e?source=post_page-----dcb43bbe9fea---------------------------------------)

## Summary and Final Thoughts

To recap, the steps for setting up the signup form are as follows:

1. **Create and Save the Form**
2. **Create and Activate the Flow** (which also publishes the form)
3. **Create and Publish the Landing Page**

In this setup, I used the built-in campaign flow templates without any customizations. However, the flow offers great flexibility. For example, as described in below article, you can configure the signup form to send a thank-you email to customers after submission.

[## SFMC Tips #122 : Marketing Cloud on Core: Personalization Part.2

### In a previous article, I explained how to deliver personalized messages to individual contacts in Marketing Cloud on…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-part-2-8d0efb6402af?source=post_page-----dcb43bbe9fea---------------------------------------)

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
