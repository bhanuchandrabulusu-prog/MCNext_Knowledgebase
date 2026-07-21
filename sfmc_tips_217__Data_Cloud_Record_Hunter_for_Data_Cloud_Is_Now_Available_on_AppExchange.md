# SFMC Tips #217 : Data Cloud : Record Hunter for Data Cloud Is Now Available on AppExchange

**Source:** https://medium.com/@marketingcloudtips/data-cloud-record-hunter-for-data-cloud-is-now-available-on-appexchange-8da6fb7769c4

---

# SFMC Tips #217 : Data Cloud : Record Hunter for Data Cloud Is Now Available on AppExchange

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8da6fb7769c4---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8da6fb7769c4---------------------------------------)

4 min read

·

Dec 17, 2025

--

Photo by [Joshua Profitt](https://unsplash.com/@joshua112?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The Data Cloud edition of the well-known **“Record Hunter”** tool for Salesforce CRM users — **Record Hunter for Data Cloud** — was newly released on **AppExchange on December 17, 2025**.

[## Data Cloud Search Tool - Record Hunter for Salesforce Data Cloud Query and Filter | Salesforce…

### Record Hunter for Data Cloud enables users to quickly create search interfaces for exploring Salesforce Data Cloud…

appexchange.salesforce.com](https://appexchange.salesforce.com/appxListingDetail?listingId=a703d241-7c13-4fd6-bc53-0ded1d11f1af&source=post_page-----8da6fb7769c4---------------------------------------)

This tool is provided by **Salesforce Labs** and is **free** to use, allowing you to get started right away.

As the name “Hunter” suggests, this is an extremely useful tool that lets you easily search (hunt) **Data Cloud DLO / DMO records directly from CRM record pages**.

## How to Get Started

1. Access the [URL](https://appexchange.salesforce.com/appxListingDetail?listingId=a703d241-7c13-4fd6-bc53-0ded1d11f1af) and click **[Get It Now].**

2. Log in with **Trailblazer.me.**

3. Select and log in to your **Salesforce environment (Data Cloud environment).**

![]()

4. Choose the environment where you want to install the package and click the button.

5. On the confirmation screen, click **[Confirm].**

6. After logging in to the environment, the installation screen appears.  
→ Install for **“All Users”**

7. You can close the screen after the installation starts.  
Once completed, the screen will change as shown below

## Adding Components to a Lightning Record Page

Next, open **Lightning App Builder** for the record page where you want to display the components.  
In this example, I selected the **Contact** record page.

You will see the following **three components** added under **Custom Managed Packages**.  
※ Components starting with **“RHDC”** belong to Record Hunter for Data Cloud.

- **RHDC — Action Buttons**  
   → Search button
- **RHDC — Filter**  
   → Search condition input fields
- **RHDC — List**  
   → Search results list

Drag and drop these three components onto the page.  
The placement order is flexible — adjust the layout to suit your needs.

## Customizing the Search Target

By default, the settings are as follows:

- **Object**: Individual DMO
- **Search Conditions**: Individual Id / Last Name / Birth Date
- **Displayed Fields**: Individual Id / Last Name / Birth Date

In this example, I will create a component that searches **Consent (Opt-In / Opt-Out)** records using an **email address**.

※ All inputs must be specified using **API reference names**.

## RHDC — Filter Settings

**Object Name**  
 `ssot__CommunicationSubscriptionConsent__dlm`

**Field Name**  
 `ssot__ContactPointValueText__c`

## RHDC — List Settings

**Object Name**  
 `ssot__CommunicationSubscriptionConsent__dlm`

**Field Names**

- `ssot__ConsentStatus__c`
- `ssot__CommunicationSubscriptionChannelTypeId__c`

> ***Tip:*** *In rare cases, an error message may appear, but it is often resolved simply by clicking* ***[Save]****. Try saving once before troubleshooting further.*

## Verification

When you open the actual record page, you can confirm that **Data Cloud consent records can be searched directly from the CRM record page**, as shown below.

## Final Thoughts

**Record Hunter for Data Cloud** is a highly practical tool that you can start using **for free right away**.  
If you have ever wanted to **view or search Data Cloud records directly from CRM screens**, this tool is definitely worth trying.

> *※ Please note that* ***AppExchange-provided tools are not covered by Salesforce Support****.  
> You cannot receive bug support via support cases for these tools, so keep this in mind.*

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
