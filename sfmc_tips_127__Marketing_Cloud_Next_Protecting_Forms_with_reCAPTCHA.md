# SFMC Tips #127 : Marketing Cloud Next: Protecting Forms with reCAPTCHA

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-protecting-forms-with-recaptcha-3ffac7090282

---

# SFMC Tips #127 : Marketing Cloud Next: Protecting Forms with reCAPTCHA

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3ffac7090282---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3ffac7090282---------------------------------------)

4 min read

·

Jun 6, 2025

--

Photo by [Radek Skrzypczak](https://unsplash.com/@radosky?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), you can enhance security by integrating **Google reCAPTCHA v2** into your website (Marketing Cloud Landing Page) to protect registration forms from malicious bots.

## Why Google reCAPTCHA is Easy to Get Started with:

- **Free for Up to 10,000 Requests/Month**  
   You can try it out effortlessly with no upfront costs.
- **No Credit Card Required**  
   There’s no need to provide credit card information during registration, allowing you to start with peace of mind.

When you approach or exceed the monthly free tier limit, you will be notified to enable billing. If billing is not activated for your Google Cloud project, reCAPTCHA will return errors for new requests once the free tier limit is reached.

## **How Google reCAPTCHA Works**

## reCAPTCHA v2

### Basic Functionality

Users click a checkbox labeled “I am not a robot”.

### Additional Verification

In some cases, users may be prompted to complete image challenges (e.g., selecting traffic lights or crosswalks).

### Invisible reCAPTCHA Badge Option

- The checkbox is hidden and operates behind the scenes.
- Nothing is displayed to regular users, providing discreet bot protection.
- **This article focuses on implementing this option**.

### **Features**

- Relatively simple to implement.
- However, user experience may be slightly impacted if image verification is triggered.

## reCAPTCHA v3

### Basic Functionality

Analyzes user behavior (e.g., mouse movements, timing of form inputs) to generate a score ranging from 0.0 to 1.0. This score helps determine whether the user is a human or a bot.

### Features

- **Non-Intrusive:** No checkboxes or image challenges, preserving a seamless user experience.
- **Customizable:** Developers can set threshold scores to decide which scores qualify as “bots”.

### Use Cases

- Ideal for websites or applications where user experience is a top priority.
- Effective when bot protection is needed without making the verification process noticeable.

## **Setup Instructions**

**1. Access Google reCAPTCHA**  
Visit the Google reCAPTCHA site and click “Get Started”.

**2. Enter a Label for Your Landing Page**

- Input a label to identify your landing page site.
- Select **“Challenge (v2)”** and choose **“Invisible reCAPTCHA Badge”**.

**3. Add the Domain of Your Published Landing Page**

- In the **“Domains”** section, add the domain of the landing page published on Marketing Cloud.
- *Note:* Do not include “https://” in the domain, as this will result in an error.

**4. Set Up a Google Cloud Platform Project Name**

- Choose a Project Name.
- Agree to the terms of service and click “Submit” (only required for first-time use).

**5. Save the “Site Key” and “Secret Key”**

- Copy and securely save the **Site Key** and **Secret Key** displayed on the screen.

## **How to Add reCAPTCHA to Your Site**

**1. Access Marketing Landing Page Builder in Salesforce**

- In Salesforce Setup, search for **“All Sites”** and select the **Marketing Landing Page Builder**.

**2. Navigate to Integration Settings**

- Click the gear icon for **Settings** and go to the **“Integration”** section.
- Find **Google reCAPTCHA v2** and click **“Add to Site”.**

**3. Enable reCAPTCHA and Input Keys**

- Toggle the switch to enable reCAPTCHA.
- Enter the **Site Key** and **Secret Key** you previously saved, then click **Save.**

**4. Activate and Publish**

- reCAPTCHA will be activated immediately.
- Publish your site.

**5. Verify Implementation**

- After publishing, check your landing page.
- You should see the reCAPTCHA badge displayed in the bottom-right corner. Success!

That’s it for this guide!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
