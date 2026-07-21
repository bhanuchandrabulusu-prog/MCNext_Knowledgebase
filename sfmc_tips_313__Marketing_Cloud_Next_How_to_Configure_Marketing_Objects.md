# SFMC Tips #313 : Marketing Cloud Next: How to Configure Marketing Objects

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-configure-marketing-objects-ec7213fda266

---

# SFMC Tips #313 : Marketing Cloud Next: How to Configure Marketing Objects

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ec7213fda266---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ec7213fda266---------------------------------------)

7 min read

·

Jun 19, 2026

--

Photo by [Karsten Winegeart](https://unsplash.com/@_karsten?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Objects, introduced in the **Marketing Cloud Next Growth & Advanced Editions** [**Summer ’26 release**](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6), are containers (data stores) designed to hold data used for marketing initiatives.

They serve a role similar to **Data Extensions** in Marketing Cloud Engagement and allow data to be imported through CSV files. At this time, only manual CSV file imports are supported.

The imported data can then be used for email personalization through [AMPscript Lookup functions](/@marketingcloudtips/marketing-cloud-next-summer-26-ampscript-support-has-arrived-18272b5f6a1e).

## Supported Data Types

- **Text**  
   String values up to 255 characters.
- **Number**  
   Positive or negative integers up to 18 digits.
- **Decimal**  
   Positive or negative decimal numbers up to 18 digits.

The length and precision of these data types cannot currently be expanded or reduced.

## Resource Allocation

### Total Marketing Object Storage Capacity

- **Growth Edition**  
   10 GB
- **Advanced Edition**  
   40 GB

### Maximum Number of Marketing Objects

- **Growth Edition**  
   25
- **Advanced Edition**  
   100

### Maximum Fields per Marketing Object

- **Growth Edition**  
   100 fields
- **Advanced Edition**  
   100 fields

## What Are Marketing Objects Used For?

In environments where Data Cloud is sufficiently structured, customer personalization can be achieved directly using Data Cloud data.

This naturally raises the question:

> *What is the purpose of Marketing Objects?*

My current understanding is:

- **Data Cloud**  
   = Customer Data Platform (CDP)
- **Marketing Object**  
   = Reference Data Platform

## Example Use Cases as a Reference Data Platform

Many marketing use cases require data that:

- **Is not directly related to customer records**
- **Needs to be easily maintained by business users**
- **Already exists in CSV format**

For example:

- **Campaign-specific messaging**
- **Segment-specific CTAs**
- **Locale-specific headlines**
- **Seasonal promotional copy**

Even when the email layout remains the same, marketers often need to change only the displayed content based on:

- CampaignCode
- Locale
- SegmentCode

## Demo Scenario

In this article, I will store the following reference data in a Marketing Object:

- Campaign
- Locale
- Segment

and dynamically switch content based on those values.

```
CampaignCode  
Locale  
SegmentCode  
Headline  
SubHeadline  
HeroMessage  
OfferLabel  
PrimaryCTA
```

You can download the sample file below:

![]()

<https://image.s12.sfmc-content.com/lib/fe3311727364047e721170/m/1/campaign_message_reference_20_records.xlsx>

## Creating a Marketing Object

1. Beginning with Summer ’26, open the newly added **Data Management** tab in the Marketing Cloud application.

2. Click **New**.

3. Upload the CSV file prepared earlier.

4. Enter the following information and click **Next**. No confirmation screen is displayed, and the import starts immediately.

- **Name**  
   Campaign Message Reference
- **API Name**  
   Campaign\_Message\_Reference
- **Description**  
   Reference data store for campaign messaging content by CampaignCode, SegmentCode, and Locale.

In this example, the following three fields are configured as the primary key. (*Marketing Objects do not support composite keys*.)

- CampaignCode
- Locale
- SegmentCode

***Important:*** *When using the AMPscript Lookup function, all fields configured as primary keys must be included as Lookup parameters.*

5. Once the import is complete, the Marketing Object is created.

6. Open the Marketing Object and navigate to the **Details** tab.

*The API Name displayed here will be used later when referencing the Marketing Object from AMPscript.*

*The important point is that you must use the* ***API Name****, not the label name.*

7. In the **Data Explorer** tab, you can review the imported records.

## Current Limitations of Marketing Objects

Currently, Marketing Objects do not support:

- Adding records
- Updating records

Therefore, if data must be corrected:

1. Delete the Marketing Object
2. Modify the CSV file
3. Re-import the data

## Preparing CRM Data

For this demo, the following three picklist fields were created in CRM:

- Campaign Code
- Locale
- Segment Code

### Campaign Code Values

```
SUMMER26  
AUTUMN26  
WINTER26  
SPRING27
```

### Locale Values

```
en_US  
ja  
fr
```

### Segment Code Values

```
GENERAL  
VIP  
DORMANT  
NEW_CUSTOMER  
HIGH_VALUE
```

For this example:

- CampaignCode = SUMMER26
- Locale = en\_US

remain fixed, while records are created with different SegmentCode values.

## Creating Content

Next, open the email content editor and create the following four **content variables**.

**Data Type:** Text

```
firstName  
campaignCode  
locale  
segmentCode
```

![]()

If you are unfamiliar with Content Variables, [please refer to the related article](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911).

## Subject Line

Enter the following in the email subject:

```
%%=v(@headline)=%%
```

## Email Body

Add an HTML block and use the following AMPscript.

The values assigned through Flow will be mapped using the variables referenced by `$content.xxx`.

```
%%[  
SET @firstName = $content.firstName  
SET @campaignCode = $content.campaignCode  
SET @segmentCode = $content.segmentCode  
SET @locale = $content.locale  
  
SET @headline = Lookup("Campaign_Message_Reference__mo","Headline__c","CampaignCode__c",@campaignCode,"SegmentCode__c",@segmentCode,"Locale__c",@locale)  
SET @subHeadline = Lookup("Campaign_Message_Reference__mo","SubHeadline__c","CampaignCode__c",@campaignCode,"SegmentCode__c",@segmentCode,"Locale__c",@locale)  
SET @heroMessage = Lookup("Campaign_Message_Reference__mo","HeroMessage__c","CampaignCode__c",@campaignCode,"SegmentCode__c",@segmentCode,"Locale__c",@locale)  
SET @offerLabel = Lookup("Campaign_Message_Reference__mo","OfferLabel__c","CampaignCode__c",@campaignCode,"SegmentCode__c",@segmentCode,"Locale__c",@locale)  
SET @primaryCTA = Lookup("Campaign_Message_Reference__mo","PrimaryCTA__c","CampaignCode__c",@campaignCode,"SegmentCode__c",@segmentCode,"Locale__c",@locale)  
]%%  
  
<div style="max-width:600px;margin:0 auto;padding:32px 24px;font-family:Arial,Helvetica,sans-serif;color:#1f1f1f;line-height:1.6;">  
  
  <p style="font-size:16px;margin:0 0 24px;">  
    Hi <strong>%%=v(@firstName)=%%</strong>,  
  </p>  
  
  <p style="font-size:16px;margin:0 0 24px;">  
    As one of our valued customers, you are invited to preview our summer collection before it becomes available to everyone else.  
  </p>  
  
  <h1 style="font-size:32px;line-height:1.2;margin:0 0 16px;color:#032d60;">  
    %%=v(@headline)=%%  
  </h1>  
  
  <h2 style="font-size:20px;line-height:1.4;margin:0 0 24px;color:#0176d3;font-weight:600;">  
    %%=v(@subHeadline)=%%  
  </h2>  
  
  <p style="font-size:17px;margin:0 0 28px;color:#333333;">  
    %%=v(@heroMessage)=%%  
  </p>  
  
  <div style="background:#f3f8ff;border-left:5px solid #0176d3;padding:18px 20px;margin:0 0 28px;">  
    <p style="margin:0 0 6px;font-size:13px;color:#0176d3;font-weight:bold;text-transform:uppercase;letter-spacing:0.5px;">  
      Special Offer  
    </p>  
    <p style="margin:0;font-size:20px;color:#032d60;font-weight:bold;">  
      %%=v(@offerLabel)=%%  
    </p>  
  </div>  
  
  <p style="font-size:16px;margin:0 0 18px;">  
    Click below to start exploring:  
  </p>  
  
  <p style="margin:0 0 32px;">  
    <a href="#"  
       style="display:inline-block;background:#0176d3;color:#ffffff;text-decoration:none;font-size:16px;font-weight:bold;padding:14px 28px;border-radius:4px;">  
      %%=v(@primaryCTA)=%%  
    </a>  
  </p>  
  
  <p style="font-size:16px;margin:0 0 8px;">  
    Thank you for being one of our most valued customers.  
  </p>  
  
  <p style="font-size:16px;margin:0 0 28px;">  
    The Example Company Team  
  </p>  
  
  <p style="font-size:12px;color:#666666;margin:0;border-top:1px solid #dddddd;padding-top:16px;">  
    Availability, eligibility, and offer details may vary by customer and region.  
  </p>  
  
</div>
```

After completing the content, save and publish it.

## **Tips: Referencing Data Graph Fields**

The examples above use content variables. However, when referencing fields from the data graph, use the following format:

`$dataGraph.<FieldName>`

For example, to reference the **Email** field in your data graph, use:

`$dataGraph.Email__c`

By using `$dataGraph`, you can access attributes stored in the data graph directly within your email content and create personalized messages for each recipient.

## Configuring the Flow

For this example, use a **Record Query Flow**.

When mapping values in the email send element’s **Content Variables** section, picklist fields can still be mapped to text variables.

Using the **Triggered Lead** resource, configure the mappings as shown below.

![]()

## Tips

If a referenced record does not exist in the Marketing Object used for content personalization, the email will not be sent with blank values.

Instead, the send enters a **Retry** status and continues retrying until the referenced data becomes available.

Once the corresponding record is added, the email will be sent during the next retry cycle.

Example:

- Marketing Object contains `en-US`
- CRM record contains `en_US`

Because the values do not match, the Lookup fails and the email enters Retry status.

The remaining configuration is standard. Complete the flow and activate it.

## Reviewing the Sent Emails

As a result of the send, five emails were delivered.

Below are three representative examples.

You can see that different content was delivered based on the SegmentCode value, confirming that the personalization worked successfully.

### Email Example ①

![]()

### Email Example ②

![]()

### Email Example ③

![]()

## Conclusion

By using Marketing Objects, organizations can now store and manage **reference data separately from customer data** directly within Marketing Cloud Next.

This approach is particularly well suited for:

- **Campaign-specific message management**
- **Locale-based content variations**
- **Segment-specific CTA management**
- **Seasonal campaign content management**

If Data Cloud serves as the foundation for managing customer data, Marketing Objects have the potential to serve as a **reference data management platform for marketing operations**.

Although current limitations include the lack of editing capabilities and API-based integrations (automated synchronization), requiring manual CSV imports, this feature demonstrates that combining Marketing Objects with AMPscript enables a simple and effective way to personalize email content based on segments, locales, and campaign attributes.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
