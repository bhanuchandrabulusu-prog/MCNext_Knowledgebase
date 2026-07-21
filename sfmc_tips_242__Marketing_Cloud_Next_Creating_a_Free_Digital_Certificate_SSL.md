# SFMC Tips #242 : Marketing Cloud Next: Creating a Free Digital Certificate (SSL)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-creating-a-free-digital-certificate-ssl-8e8b43becd9b

---

# SFMC Tips #242 : Marketing Cloud Next: Creating a Free Digital Certificate (SSL)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8e8b43becd9b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8e8b43becd9b---------------------------------------)

6 min read

·

Jan 27, 2026

--

Photo by [Tanya Yarosh](https://unsplash.com/@monday88?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

If you need a digital certificate (SSL) for some kind of verification purpose or as a temporary measure, the **90-day free plan from ZeroSSL** is very convenient.

I have personally used it in the past, and because:

- It can be used without registering a credit card
- You receive reminder emails when the expiration date approaches
- Even if you ignore them, there are no persistent sales or solicitation emails afterward

there is no particular problem even if you leave it without renewing.

## Relationship with Marketing Cloud Next

In **Marketing Cloud Next**, when configuring a **custom domain for click tracking**, you need to **prepare a digital certificate (SSL) in advance**.

Therefore, in this article, I prepare an SSL certificate with this use case in mind.

> *For this process, I will begin the work while partially referring to the steps in the following article.*

[## SFMC Tips #172 : Marketing Cloud Next: Setting Domains for Email Tracking Links

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), when a recipient clicks a link in an email, the…

medium.com](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d?source=post_page-----8e8b43becd9b---------------------------------------)

## Preparing a CA-Signed Certificate

1. In Setup, enter “Certificate”, open **Certificate and Key Management**, and click **Create CA-Signed Certificate**.

2. Enter the required information and save.

**Configuration example:**

- Display Label: `CASignedCert_10Sep2025` (Display name for Salesforce management)
- Unique Name: `CASignedCert_10Sep2025` (API name for Salesforce management)
- Common Name: `click.XXXXX.com` (Enter the “subdomain” used for clicks)
- Company Name: `XXX Company` (Official company name)
- City/County: `Minato-ku` (Company location)
- Country Code: `JP` (2-letter country code)
- Key Size: `2048` recommended
- Email Address: `abc@xxx.com` (\*Optional)
- Department: `IT`, etc. (\*Optional)
- State/Province: `Tokyo` (Company location)

> *※ After saving, only* ***Display Label*** *and* ***Unique Name*** *can be edited.  
> ※* ***Exportable Private Key*** *specifies whether the private key is exported to the keystore together with the certificate. If this option is disabled, the private key is not included when exporting the certificate. As a general rule,* ***keep this “off”****.*

3. Open the saved record and click **Download Certificate Signing Request**. You can obtain a certificate signing request with the `.csr` extension.

**Example of a Certificate Signing Request with the** `.csr` **Extension**

> *Think of this* `.csr` *file as an* ***application form*** *to ZeroSSL that says,  
>  “I would like to create an SSL certificate for this domain.”*

## Registering a CAA Record

Next, register a **CAA record** in your DNS registrar’s management console.

A CAA (Certification Authority Authorization) record is a mechanism to explicitly declare in DNS:

> *“The only certificate authority (CA) allowed to issue SSL certificates for this domain is this one.”*

### Why is this necessary?

In this case, since we are using ZeroSSL,  
the certificate authority that receives the certificate issuance request will check the CAA record in DNS in order to confirm:

> *“Is it acceptable for me to issue a certificate for this domain?”*

If a CAA record does not exist, or if a certificate authority that is not permitted is specified, the certificate issuance will be rejected.

In other words, this is like putting up a signpost in DNS.  
Because it is an important prerequisite for certificate issuance, be sure to configure it.

### Values for ZeroSSL

When using ZeroSSL (which is actually Sectigo), set the following value:

- **Value:** `sectigo.com` 【**※ DNS work is performed here**】

※ The record type and how to specify flags vary depending on the DNS provider, so [follow the instructions shown in the management console](https://help.zerossl.com/hc/en-us/articles/360060119753-Invalid-CAA-Records).

## ZeroSSL Configuration

1. On the ZeroSSL website, click **Get Free SSL**.

2. Register a user account.

3. After logging in, select **New Certificate**.

4. Enter the custom domain and click **Next Step**.

5. Select a **90-day** validity period and click **Next Step**.

6. Add-Ons are not required, so skip them and click **Next Step**.

7. Turn off **Auto-Generate CSR**, then turn on **Paste Existing CSR**. The screen will look like the following.

8. Paste the **certificate signing request (CSR)** prepared in advance and click **Next Step**.

9. A confirmation screen is displayed. Click **Next Step** as is.

10. A plan confirmation screen is displayed.  
Previously, the “Free Plan” was explicitly shown, but it is no longer displayed. Turn **both toggles off**, then click **Next Step**.

11. At this point, a draft is created. Go to the **Certificates** menu.

12. You can confirm that a draft has been created and that the expiration date is **90 days from now**. Next, click **Verify**.

13. You will return to the verification method selection screen. Select **DNS (CNAME)**.

14. The authentication information to register in DNS (CNAME record) is displayed. Copy this and register it in your own DNS. 【**※ DNS work is performed here**】

After registration is complete, click **Next Step**.

15. Finally, run the domain verification. Click the button, and if there are no issues, the verification will complete.

> *※ After registering DNS records, it is recommended to wait about* ***5–10 minutes*** *for propagation.*

16. When verification succeeds, a screen for downloading the certificate is displayed. Click the button to obtain the files.

17. From the downloaded files, register `certificate.crt` **(server certificate)** in Salesforce.

![]()

18. From here, return to **“Step 5”** of the previously mentioned article and continue the work.

[## SFMC Tips #172 : Marketing Cloud Next: Setting Domains for Email Tracking Links

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), when a recipient clicks a link in an email, the…

medium.com](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d?source=post_page-----8e8b43becd9b---------------------------------------)

## Conclusion

In cases where an SSL certificate is required for a short period or for verification purposes — such as validating a custom domain for click tracking in Marketing Cloud Next — the **90-day free certificate from ZeroSSL** is a sufficiently practical option.

First, try going through this procedure once to understand the overall flow.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
