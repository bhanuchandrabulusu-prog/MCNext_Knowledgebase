# Fix “Authenticated Domains” Setup Not Enabled in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/authenticated-domains-not-enabled

---

When setting up Authenticated Domains for email sending in Salesforce Marketing Cloud Next (Growth and Advanced), you might run into an issue where the setup option isn’t visible. This usually happens after an upgrade from Salesforce Foundation to Growth Edition.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/image3-1024x379.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/image3.png) 

The good news? The fix is simple once you know where to look.

## Step 1: Complete the Migration Process

Salesforce requires you to complete a one-time migration step before enabling domain authentication.

1/ Go to *Salesforce Setup* and navigate to: *Unified Messaging → Email → Migration*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20227%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/image2.png) 

The Unified Messaging → Email → Migration page

2/ On the Migration page, check the status indicator. You’ll need to *Pause* or *Complete All Campaigns* before proceeding.

3/ Click *Transfer* to Marketing Cloud. This action updates your Salesforce org to allow authenticated domain configuration.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20284%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/image1.png) 

Transferring the Domain to Marketing Cloud Next

## Step 2: Wait for the Update

After clicking Transfer, the system may take up to 24 hours before the Authenticated Domains page becomes available in Setup. Don’t worry if you don’t see it immediately.

## Step 3: Add Your Authenticated Domain

Once visible, you can now configure your domain:

1. Go to *Setup → Email → Authenticated Domains*.
2. Follow the prompts to add your domain (e.g., email.yourcompany.com).
3. Update DNS records as directed for authentication (SPF, DKIM, etc.).

Helpful References:

- [Transfer to Marketing Cloud – Salesforce Help](https://help.salesforce.com/s/articleView?id=004141354&type=1)
- [Add an Authenticated Domain – Salesforce Help](https://help.salesforce.com/s/articleView?id=mktg_um_channel_email_domain.htm&type=5)

**Problem solved!** Once migration is complete and domains are authenticated, your team can send branded, trusted emails without issues.

Thanks to Nicole Anaya for helping to solve this one!
