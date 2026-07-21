# SFMC Tips #153 : Marketing Cloud Next: Leveraging Prospects

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-leveraging-prospects-8aa701aea983

---

# SFMC Tips #153 : Marketing Cloud Next: Leveraging Prospects

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8aa701aea983---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8aa701aea983---------------------------------------)

7 min read

·

Aug 5, 2025

--

Photo by [Sri Gowda](https://unsplash.com/@sri_go?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), marketers can leverage “prospects” to ensure that only highly qualified leads are passed on to sales representatives.

A “prospect” refers to a potential customer who has not yet reached the deal stage but has provided contact information (such as an email address) through channels like sign-up forms. At this point, they have not been assigned to a sales representative.

On the other hand, a “lead” is a prospect who has met certain criteria, such as scoring thresholds through marketing efforts, and has been assigned to a sales representative. Furthermore, a “contact” represents a lead that has progressed to the deal stage and is moving toward an actual transaction.

### **People Status**

- **Prospect:** Status before being assigned to a sales representative
- **Lead:** Status after being assigned to a sales representative
- **Contact:** Status when the lead has converted into a deal and the transaction has started

### **Deal Conversion Likelihood**

- **Prospect:** Low to Medium (Handled by: Marketer)
- **Lead:** Medium to High (Handled by: Sales Representative & Marketer)

## **Steps for Adding and Importing Prospects**

When you have individuals who are not yet qualified as leads but may have a potential to purchase in the future, you can add them as “prospects” in Marketing Cloud.

> ***Note:*** *Simply adding a prospect does not enable marketing communications to them. To send marketing communications, you must create a* ***Consent Record*** *for each channel.*

### Methods for Adding Prospects

1. Adding Prospects via Event Trigger Flow
2. Manually Adding a Single Prospect
3. Bulk Adding Prospects via CSV Import

### 1. Adding Prospects via Event Trigger Flow

You can create prospects through a sign-up form by using an Event Trigger Flow when the form is submitted.

> ***Note:*** *When using a standard sign-up form template, elements for lead creation are automatically generated. Therefore, if you wish to create a prospect instead of a lead, you’ll need to manually adjust and modify the form settings.*

For detailed steps on creating a sign-up form, please refer to the article below:

[## SFMC Tips #104 : Marketing Cloud Next: Creating a Signup Form

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions) provides an efficient way to capture new leads by…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea?source=post_page-----8aa701aea983---------------------------------------)

### 2. Manually Adding a Single Prospect

You can register prospects one by one directly from the Marketing Cloud interface.

1. Navigate to the **Prospects** tab.
2. Click the **New** button in the top right corner.
3. Fill in the prospect’s information in the form.

**Required Fields:** To enable sending communications, at least one of the following must be provided — *Last Name*, *Email Address*, or *Phone Number*. Additionally, *Currency* is also a mandatory field.

4. Once all required fields are filled out, click **Save** to complete the registration.

### 3. Bulk Adding Prospects via CSV Import

When you need to register multiple prospects at once, you can perform a bulk import using a CSV file.

1. Navigate to the **Prospects** tab and click **Import** in the top right corner.
2. Select **Import from File**, then click **Next**.
3. Click **Upload File**, select your CSV file, and click **Next**.
4. Map each column in the CSV file to the corresponding fields in Salesforce.
5. After completing the field mapping, click **Start Import**.
6. Click **Finish** to complete the process.

## Converting Prospects

Prospects can be converted into Leads or Contacts either manually or through automated flows.

> ***Tip:*** *With the Summer ’25 release, it is now possible to convert Prospects directly into* ***Contacts****.*

### Methods for Converting Prospects

1. Manually convert a Prospect to a Lead
2. Manually convert a Prospect to a Contact
3. Automatically convert Prospects to Leads or Contacts via Trigger Flows

### 1. Manually Converting a Prospect to a Lead

Identify prospects who meet the engagement score criteria and convert them into Leads.

1. Navigate to the **Prospects** tab, select the target Prospect, and open the record page.
2. Click **Convert** in the top right corner.
3. Choose whether to create a **new Lead** or select an **existing Lead**.

- If converting to an existing Lead, only the empty fields in the Lead record will be updated with the Prospect’s information.

4. Enter required information such as Record Owner, Company Name, etc.

5. Click **Convert**.

- The entered information will be mapped to the Lead record accordingly.

> ***Important:*** *If there are any* ***custom required fields*** *on the Lead object, you will not be able to convert the Prospect until those fields are addressed.*

### 2. Manually Converting a Prospect to a Contact

Identify qualified Prospects and convert them into Contacts. A Contact can be associated with a **new Account** or an **existing Account**.

1. Navigate to the **Prospects** tab, select the target Prospect, and open the record page.
2. Click **Convert**.
3. In the **Convert Prospect** window, select **Contact**.
4. Enter or select the related **Contact** and **Account**.

- If you select an existing Contact, you cannot create a new Account during the conversion.

5. (Optional) Associate the Contact with a **new Opportunity** or an **existing Opportunity**.

- If you do not wish to create an Opportunity, select **Don’t create an opportunity upon conversion**.

6. Assign a Record Owner for the Contact and click **Convert**.

> ***Important:*** *If there are* ***custom required fields*** *on the Contact object, you will not be able to convert the Prospect until those fields are addressed.*

### 3. Automatically Converting Prospects via Trigger Flows

You can automate the conversion of Prospects to Leads or Contacts using **Data Cloud Trigger Flows**, **Event Trigger Flows**, or **Form Trigger Flows**.

The detailed setup process for automating these conversions is explained in the following article:

[## SFMC Tips #154 : Marketing Cloud Next: Converting Prospects via Flow

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can convert prospects into leads or contacts…

medium.com](/@marketingcloudtips/marketing-cloud-next-converting-prospects-via-flow-7f95b7f6270c?source=post_page-----8aa701aea983---------------------------------------)

## Setting Up Lead Assignment Rules

Once a prospect is converted into a Lead, the **Lead Assignment Rules** determine the record owner automatically.

> *If you need to assign different owners based on specific lead criteria, you’ll need to create new assignment rules manually.*

Navigate to **Setup**, search for **Lead Assignment Rules** in the Quick Find box, and select **Lead Assignment Rules** to create a new rule.

### Examples of Lead Assignment Rules

✅ **Rule 1: NOT(ISNEW())**  
**Condition:** The record is not newly created (i.e., an existing lead is being updated).  
**Assignee:** Current Owner (Same User)  
**Purpose:** Ensure that ownership remains unchanged when editing existing leads.

✅ **Rule 2: Lead: State/Province equals CA**  
**Condition:** The State/Province field is set to “CA” (California).  
**Assignee:** Queue “Sales — Leads West”  
**Purpose:** Assign leads from the West Coast to the dedicated Sales — Leads West queue.

✅ **Rule 3: Lead: Lead Source equals Website**  
**Condition:** The Lead Source field is “Website”.  
**Assignee:** Queue “Sales — Lead”  
**Purpose:** Route leads that came through the website to a specific sales team.

✅ **Rule 4: Lead: Email not equal to null**  
**Condition:** The Email field is populated.  
**Assignee:** Queue “Sales — Lead”  
**Email Notification:** Enabled  
**Purpose:** Assign leads with an email address to the Sales — Lead queue and notify the assigned owner.

## Considerations When Working with Prospects

When managing **Prospects** in Marketing Cloud, please keep the following points in mind:

### 1. Converted Prospects Do Not Appear in List Views

- Once a Prospect is converted to a **Lead**, it will no longer appear in List Views.
- However, converted Prospects remain visible in **Data Explorer**.
- Even if you apply a filter like **Converted = True**, they will not be displayed in the List View.

### 2. Exclude Converted Prospects When Building Segments

- When creating a segment of Prospects, you must explicitly exclude converted records.
- For example, add a condition such as **Prospect Status != Converted**.
- Otherwise, converted Prospects will be included in your segment by default.

### 3. Prospects Cannot Be Added to Campaigns

- Only **Leads** and **Contacts** can be added as Campaign Members.
- Prospects are not eligible to be directly added to Campaigns.

### 4. Limitations on Prospect Management

- Prospects cannot be imported using the **Data Import Wizard**.
- Prospects cannot be copied or mass deleted.

### 5. Attribute Carryover After Conversion

- After a prospect is converted, the engagement score and engagement history (such as Email and Web) are carried over as long as the unified ID remains the same (following ID resolution and the update of precomputed insights).

### 6. Maintaining Relationships Between Prospects and Leads

- The relationship between a converted Prospect and its corresponding Lead is preserved through:
- The **Converted Lead** field on the Prospect object, which stores the Lead ID.
- A related record created in the **Identity Match DMO (Data Model Object)** to maintain the linkage.

## Conclusion

If your sales team can adequately handle potential customers before they reach the deal stage, there may not be a pressing need to utilize Prospects. However, if the volume of potential customers becomes too large to manage effectively, leveraging Prospects is highly recommended to improve sales efficiency.

By combining **Marketing Engagement Scores** with automated **Flows**, you can seamlessly pass only highly qualified Prospects to the sales team, enabling more precise and efficient collaboration between marketing and sales.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
