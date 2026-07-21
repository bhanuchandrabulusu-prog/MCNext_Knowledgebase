# SFMC Tips #184 : Marketing Cloud Next: How to Configure Form Handlers

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-configure-form-handlers-ed3e045adfad

---

# SFMC Tips #184 : Marketing Cloud Next: How to Configure Form Handlers

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ed3e045adfad---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ed3e045adfad---------------------------------------)

8 min read

·

Oct 6, 2025

--

Photo by [Cam](https://unsplash.com/@cxmeel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of **Marketing Cloud Next Growth & Advanced Edition**, a new **Form Handler** feature has been introduced. This allows you to easily integrate data collected from external forms into Salesforce **without modifying the structure of the external form**.

When setting up form handlers, it is important to correctly map the fields from the external form to the fields in the Salesforce object. In particular, the HTML form’s `name` attributes must exactly match the Salesforce field names. Note that uppercase and lowercase differences are treated as distinct, so pay close attention.

This article explains the steps to configure the Form Handler feature.

## 1. Configure CORS Allowlist

To allow form submissions from external sites, you need to register the external site domain in Salesforce’s **CORS (Cross-Origin Resource Sharing) settings**. The steps are as follows:

1. In **Setup**, search for **CORS**, select it, and click **New**.

2. Add an **Origin URL Pattern**.

**Tips for entering the Origin URL Pattern:**

- **Include protocol and domain name:** The URL pattern must include `http` or `https` and the domain name. Do not include the trailing hyphen.
- **Using wildcards:** You can use `*` to allow all subdomains, but it must be placed before the second-level domain.

Example: `https://*.example.com` → allows all subdomains of `example.com`.

In my case, I’m using **Marketing Cloud Engagement’s CloudPages**, so I entered the following:

https://mcxkknz3m0zj3jqsxn4hm3dp3q-4.pub.sfmc-content.com

## 2. Create a Form Handler

1. Next, go to the **Content** tab, click **Add Content**, and select **Form Handler**.

![]()

2. Give the form handler a name of your choice and save it.

## 3. Map External Fields

1. In the **Data Source** section, click **Add Data Source**.

2. Here, the submitted form data will be used as the data source. Select the Salesforce object to map the data to. You can choose from **Account**, **Contact**, **Lead**, or **Prospect**.

3. From the left-hand field panel, select the fields you want to map and enter the corresponding **External Field Name** for each field.

**Considerations:**

- Select all required fields.
- For **External Field Name**, enter the value of the `name` attribute from the HTML form. Uppercase and lowercase letters must match exactly.

Example:

```
<div class="form-group">  
  <label for="lastName">Last Name</label>  
  <input type="text" id="lastName" name="lastName" required="">  
</div>
```

> *In this case,* `name="lastName"` *means the* ***External Field Name*** *is* `lastName`*.*

- Do not use spaces in **External Field Name**. If a space is included, an error will occur when saving in the flow.
- Salesforce checkbox fields are stored as boolean values (`true` or `false`), so the HTML form checkbox should use `true` when checked and `false` when unchecked.
- Date and time values must be entered in the specified format, including the timezone.

**Date and Time Formats:**

- Date: `YYYY-MM-DD`
- Time: `hh:mm:ss`
- DateTime: `YYYY-MM-DDTHH:mm:ss.sssZ`  
   Example: `2025-07-31T15:00:00.000+0530`

**Tip:** On external web pages, consider using a **hidden field** to combine date, time, and timezone into a single value before mapping.

## 4. Spam Protection (Optional)

To prevent automated spam submissions, you can add an **invisible honeypot field** to the form handler.

🐝 **What is a Honeypot Field?**

A honeypot field is an **invisible input field** embedded in the form.

It is hidden from human users using CSS, so normally it cannot be filled out.

However, many spam bots are programmed to **fill in every input field in the form**, so they will also fill in this hidden field.

In other words, if the hidden field contains a value, it can be used to **identify a bot submission**.

1. From the left-hand **Spam Protection Fields** panel, add a **Honeypot** field.

2. Set the external field name to something like `comments`, which is a name a bot is likely to fill in.

3. Add a hidden input field with the same `name` attribute in the form’s HTML.

```
<!-- Honeypot field (for bot protection) -->  
<div class="honeypot">  
  <label for="comments">Comments</label>  
  <input type="text" id="comments" name="comments">  
</div>
```

## 5. Redirect Settings After Submission

Next, configure the URLs where users will be redirected **after a successful or failed submission**.

1. For this example, I’ll keep it simple: if the submission succeeds, redirect to `https://www.salesforce.com/`, and if it fails, redirect to `https://www.google.com/`.

2. Since the next step is to transition to the flow, **save your work at this point**.

**Tip:** In form handlers, you do **not** publish the handler directly. You must activate the **subsequent flow**, and activating the flow will automatically enable the form handler as well.

## 6. Automated Processing via Flow

To automate processes such as **creating leads**, **creating consent records**, or **sending emails** after a form is submitted on an external page, you need to create a flow.

1. In the **Flow** section of the form handler, click the **New Flow** button.

2. A draft flow will be automatically created. Open it in the **Flow Builder**.

3. By default, an element is placed to create a record for the same object as the data source.

4. You can activate it as-is, but you may want to configure additional elements, such as creating consent records or sending emails, and then save the flow.

5. Activate the flow. Activating the flow will automatically **publish the form handler** as well.

**Note:** If you edit the form handler after the flow has been created, the changes are **not automatically reflected**. You need to create a **new version of the flow** to apply the updates.

## 7. Publishing the Form Handler

1. Once the flow is activated and the form handler is published, **copy the Tracking Script**.

2. In this example, I am treating **Marketing Cloud Engagement’s CloudPages** as an external website. Open the **Code View** tab and paste the script **just before the** `</body>` **tag**.

3. Next, copy the **Form Attributes** and add them **inside the** `<form>` **tag**.

If you’re unsure how to add them, you can refer to the example HTML block I used below:

```
<meta charset="UTF-8">  
<title>Contact Form</title>  
<style>  
  body { font-family: Arial, sans-serif; background-color: #f4f7f9; margin:0; padding:20px; }  
  .form-container { max-width:500px; margin:40px auto; background:#fff; padding:30px; border-radius:12px; box-shadow:0 4px 12px rgba(0,0,0,0.1); }  
  .form-container h2 { text-align:center; margin-bottom:25px; color:#333; }  
  .form-group { margin-bottom:20px; }  
  .form-group label { display:block; margin-bottom:8px; font-weight:bold; color:#444; }  
  .form-group input { width:100%; padding:12px; border:1px solid #ccc; border-radius:8px; font-size:14px; transition:border-color 0.3s; box-sizing: border-box; }  
  .form-group input:focus { border-color:#0070d2; outline:none; }  
  .submit-btn { width:100%; padding:14px; background-color:#0070d2; border:none; border-radius:8px; color:#fff; font-size:16px; font-weight:bold; cursor:pointer; transition: background-color 0.3s; box-sizing: border-box; }  
  .submit-btn:hover { background-color:#005bb5; }  
  /* Honeypot (hidden) */  
  .honeypot { display:none; }  
</style>  
  
<div class="form-container">  
  <h2>Contact Us</h2>  
  <form id="MCO27UGLAB4BGFZMV5P7TGQ2PUK4" data-uma-forms="true" method="post">  
  
    <div class="form-group">  
      <label for="lastName">Last Name</label>  
      <input type="text" id="lastName" name="lastName" required="">  
    </div>  
  
    <div class="form-group">  
      <label for="firstName">First Name</label>  
      <input type="text" id="firstName" name="firstName" required="">  
    </div>  
  
    <div class="form-group">  
      <label for="emailAddress">Email Address</label>  
      <input type="emailAddress" id="emailAddress" name="emailAddress" required="">  
    </div>  
  
    <!-- Honeypot Field -->  
    <div class="honeypot">  
      <label for="comments">Comments</label>  
      <input type="text" id="comments" name="comments">  
    </div>  
  
    <!-- Hidden Fields -->  
    <input type="hidden" name="CreatedDate" value="">  
    <input type="hidden" name="LastModifiedDate" value="">  
    <input type="hidden" name="Status" value="New">  
  
    <button type="submit" class="submit-btn">Submit</button>  
  </form>  
</div>  
  
<script>  
document.addEventer("DOMContentLoaded", function() {  
  const now = new Date().toISOString();  
  document.querySelector("input[name='CreatedDate']").value = now;  
  document.querySelector("input[name='LastModifiedDate']").value = now;  
});  
</script>
```

4. Optionally, enable **external website tracking** to monitor user behavior. For implementation details, refer to the relevant guide.

[## SFMC Tips #130 : Marketing Cloud Next: Tracking External Websites with a Consent Banner

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can track visitor activity and engagement…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c?source=post_page-----ed3e045adfad---------------------------------------)

**Note:** If you are using **reCAPTCHA**, generate the token on the external page and ensure it is **always submitted with the form**.

## 8. Submitting the Form and Verifying Record Creation

1. Access the CloudPage and **submit the form**.

![]()

2. The submission was successful, and the page redirected to `https://www.salesforce.com/`.

3. A new **lead record** was created. Success!

## **Conclusion**

Form Handlers provide a convenient way to **capture data from external forms into Salesforce**, manage automated processing, prevent spam, and handle post-submission redirects. Paying close attention to **exact field name matching** and **date/time formatting** ensures smooth implementation and accurate data handling.

That concludes this guide.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
