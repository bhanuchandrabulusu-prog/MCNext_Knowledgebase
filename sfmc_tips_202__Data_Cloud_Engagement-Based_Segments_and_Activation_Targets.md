# SFMC Tips #202 : Data Cloud: Engagement-Based Segments and Activation Targets

**Source:** https://medium.com/@marketingcloudtips/data-cloud-engagement-based-segments-and-activation-targets-dd63ebb540ed

---

# SFMC Tips #202 : Data Cloud: Engagement-Based Segments and Activation Targets

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--dd63ebb540ed---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--dd63ebb540ed---------------------------------------)

5 min read

·

Nov 14, 2025

--

Photo by [Houcine Ncib](https://unsplash.com/@houcinencibphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Until now, the **“Segment On”** option in Data Cloud segments was limited to data model objects (DMOs) in the **Profile** category. However, as of the **June 2025 update**, DMOs in the **Engagement** category can also be used as segmentation targets.

With this enhancement, you can now create segments based on engagement-category DMOs and activate them directly to **Marketing Cloud Engagement**. Previously, it was difficult to pass related attribute data to Marketing Cloud Engagement, which posed operational limitations, but this update is expected to **significantly improve efficiency**.

That said, one important point remains:  
Just like with profiles, **only records that have associated contact points — such as email addresses or phone numbers — are eligible**. In other words, you cannot activate all engagement data indiscriminately. Only engagement records that can actually be used for message delivery are included.

Let’s walk through a concrete use case to illustrate how this new capability can be utilized.

## Use Case Overview

I prepare the following **profile data** for nine individuals:

I also prepare the following **engagement (purchase) data**, where three of the nine individuals have made purchases:

I want to create an engagement-based segment in Data Cloud, and for each purchased product, send a personalized message the day after the purchase. The goal is to generate segments like the following:

This is the corresponding Journey Builder flow:

![]()

## Data Ingestion and Mapping

## Profile Data

After importing the profile data:

- **Id**, **First Name**, and **Last Name** were mapped to the **Individual** object.
- **Email** was mapped to the **Contact Point Email** object.

This is the simplest and most common configuration.

## Purchase Data

After importing the purchase data, it was mapped to a custom DMO created for this demo called **“Purchase Data Test”**.

A relationship was established between the purchase DMO and the **Individual** object. The relationship is many-to-one, using **Id → Individual Id** as the key mapping.

## Segment Configuration

In the **Segment On** setting, I select the engagement data object **Purchase Data Test**.

Since the dataset is simple, I complete the setup without adding additional filter conditions.

## Activation Setup

I proceed to activate the segment for **Marketing Cloud Engagement**.

The activation membership type remains as **engagement data**.

Next, I specify the path to the contact point (email or phone). Since multiple paths may appear, it’s essential to carefully select the path that correctly resolves the email address to be used.

> *As mentioned earlier, activation is only possible* ***when a valid email address exists****. Records with a NULL email cannot be activated.*

I then choose the attributes to send. Currently, Purchase Id and Email are already included.  
Even if you don’t manually add **Subscriber Key (Individual Id)**, it will be automatically included — so no worries there.

I add the following attributes, which are required for our use case:

- **Product**
- **PurchaseDate**
- **FirstName**
- **LastName**

Once the attributes (other than Subscriber Key) are configured, I click **Next**.

I assign an activation name, enable **overwrite (full refresh) updates**, and save.

After activation is set, I return to the segment settings and **publish** the segment.  
Activation to Marketing Cloud Engagement occurs **each time the segment is published**.

## Verification in Marketing Cloud Engagement

Within approximately 15–30 minutes, the data is delivered to Marketing Cloud Engagement.  
As you can see below, the data appears exactly as expected — matching the Excel sheet prepared earlier.

When the journey is triggered, the branches work correctly, and **six emails are sent**, as intended. Successful execution!

![]()

## Conclusion

Incidentally, with Data Cloud’s Bring Your Own Lake (BYOL) data sharing,   
it is possible to create data lake objects that use **composite keys** (primary keys composed of multiple fields).

However, there is a known issue where data extensions with multiple primary keys do not return correct results when used as the target of a segment.  
Each time you save the segment, it may return different values, and attempting to publish it as-is will result in an error.

Therefore, in such cases,  
it is recommended to combine the composite key fields into a single value using a formula such as **CONCAT**, and redefine it as a single-field primary key.

For the specific steps to create this, please follow the instructions provided in the [Salesforce Help documentation](https://help.salesforce.com/s/articleView?id=data.c360_a_composite_key.htm&type=5).

Until now, Marketing Cloud Engagement only supported **profile-based** record activation, which limited the scope of data activation. With this update, **engagement-based** activation is now possible, representing a major advantage for users who actively integrate **Data Cloud + Marketing Cloud Engagement**.

This enhancement is truly a **game changer**, expanding the possibilities for data utilization and operational design.

I encourage you to take full advantage of this powerful new feature.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
