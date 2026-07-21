# SFMC Tips #111 : Microsoft Follows Google and Yahoo with New “Sender Guidelines”

**Source:** https://medium.com/@marketingcloudtips/microsoft-follows-google-and-yahoo-with-new-sender-guidelines-b4e69f35dba5

---

# SFMC Tips #111 : Microsoft Follows Google and Yahoo with New “Sender Guidelines”

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b4e69f35dba5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b4e69f35dba5---------------------------------------)

4 min read

·

May 5, 2025

--

Photo by [BoliviaInteligente](https://unsplash.com/@boliviainteligente?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This topic might feel like a bitter pill to swallow for email senders, but let’s not forget that we are also recipients of corporate emails as individuals. This should be seen as an opportunity for positive improvement.

In October 2023, Google and Yahoo jointly announced their “Sender Guidelines” for bulk senders, effective from June 2024. Now, as of today, May 5, 2025, Microsoft is following suit. This means email domains like Outlook and Hotmail will also be impacted.

Under this change, domains sending more than 5,000 emails per day must meet specific requirements. These guidelines closely resemble those from Google and Yahoo, so if you’ve already taken measures for those providers, there’s no need for significant concern.

## Authentication Requirements

SMTP (Simple Mail Transfer Protocol) does not inherently verify if an email sender is legitimate. To ensure the sender’s authenticity, email authentication technologies like the following are necessary:

### 1. SPF (Sender Policy Framework)

SPF verifies that an email address (MAIL FROM / Envelope FROM) sent from a specific domain originates from an authorized server. By checking the TXT record (SPF record) in DNS, the legitimacy of the sending server is confirmed, preventing spoofing.

- **How it works:** The policy dictates, “Emails from this domain must be sent from these servers.”
- **Failure:** Indicates potential spoofing.

### Guideline Requirements

- The domain’s DNS record (SPF record) must list the exact sending IP addresses authorized to send emails for that domain.

### 2. DKIM (DomainKeys Identified Mail)

DKIM adds a digital signature to outgoing emails, which recipient servers verify to prevent tampering or forgery. Using public-key cryptography, the sending server creates a signature with a private key, while the recipient retrieves the public key from the DNS server for validation.

- **How it works:** A digital signature is added to the message or header. The recipient server validates this signature to confirm the integrity of the message.
- **SPF vs. DKIM:** SPF checks the MAIL FROM address and sending IP, while DKIM ensures the FROM address and email content are aligned and untampered.

### Guideline Requirements

- A valid DKIM signature must be in place to confirm the integrity and reliability of the email.

### 3. DMARC (Domain-based Message Authentication, Reporting, and Conformance)

DMARC works with SPF and DKIM to verify that the sender’s information (MAIL FROM and FROM address) matches. DMARC policies define actions for handling emails that fail authentication.

### DMARC Authentication Process

1. **SPF Check**  
   Verify if the MAIL FROM domain matches the sender’s IP address.
2. **DKIM Check**  
   Verify if the FROM address aligns with the content signed by the DKIM signature.
3. **DMARC Policy**  
   Confirm whether either SPF or DKIM (or both) are valid and aligned, and whether the domains in MAIL FROM and FROM addresses match.  
   Additionally, define the handling policy for emails that fail authentication:

- **Reject (Bounce)**: Do not accept the email.
- **Quarantine (Spam Folder)**: Move the email to the spam folder.
- **None (No Action)**: Deliver the email without any restrictions.

### Guideline Requirements

- SPF and/or DKIM must align, with at least a `p=none` policy (allow delivery without action).

When implemented correctly, SPF, DKIM, and DMARC complement each other to protect against spoofing and phishing attacks, significantly enhancing email security.

## Email Hygiene Best Practices

Bulk senders must adopt the following practices to maintain the quality and trustworthiness of their email communications:

### 1. Compliant P2 (Primary) Sender Address

Ensure that the “From” address and “Reply-To” address are valid, reflect the actual sending domain, and are capable of receiving replies.

- **Key Point**: It’s essential not only that the recipient’s inbox can receive emails, but also that the sender’s domain is valid and operational within the DNS infrastructure.

### 2. Functional Unsubscribe Link

For marketing emails or bulk messages, provide a simple and clearly visible method for recipients to opt out of future communications.

- **Best Practice**: The unsubscribe link should be easy to locate and ensure immediate removal upon a recipient’s request.

### 3. Transparent Email Sending Practices

Use accurate subject lines, avoid misleading headers, and ensure that recipients have explicitly agreed to receive messages.

- **Example**: Avoid unnecessary “RE:” or “FW:” prefixes that could mislead recipients about the content’s origin.

### 4. List Hygiene and Bounce Management

Regularly remove invalid addresses to reduce spam complaints, bounces, and wasted messages.

- **Pro Tip**: Salesforce Marketing Cloud’s Automation Studio can help identify subscribers who haven’t opened emails in the past 180 days and exclude them from your mailing lists.

[## SFMC Tips #20 : Extracting Subscribers Who Haven’t Opened Emails in the Last 180 Days Using…

### In your organization, is there a possibility that subscribers who have not opened any emails in the past 180 days might…

medium.com](/@marketingcloudtips/extracting-subscribers-who-havent-opened-emails-in-the-last-180-days-using-automation-studio-27c0d1c9bb80?source=post_page-----b4e69f35dba5---------------------------------------)

### Consequences of Non-Compliance

Significant violations related to authentication or hygiene can result in actions from Microsoft, including spam filtering or blocking messages entirely.

- **Rejected Messages**: You may encounter errors like:  
  `"550; 5.7.515 Access denied, sending domain [SendingDomain] does not meet the required authentication level."`

For more details on these sending guidelines, refer to the following blog:  
[**Blog: Strengthening Email Ecosystem: Outlook’s New Requirements for High‐Volume Senders**](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730)

### Final Thoughts

As mentioned earlier, if you’ve already implemented measures to comply with Google or Yahoo sender guidelines, there’s no need for excessive concern. Most senders likely have some safeguards in place. Simply being aware of Outlook and Hotmail’s new “sending guidelines”, effective May 5, 2025, should suffice.

That’s all for now!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
