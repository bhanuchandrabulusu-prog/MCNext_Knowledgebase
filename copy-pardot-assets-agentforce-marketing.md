# Copy Account Engagement’s Assets to Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/copy-pardot-assets-agentforce-marketing

---

**In Agentforce Marketing (Marketing Cloud Next), all assets are stored in a default Enhanced CMS workspace from Digital Experiences, that is created during the setup**. Account Engagement’s assets (Email, Files, Forms and Landing Page) are stored in different locations. Let’s see what can be made available from Pardot to MC Next and how.

## Activate Copy to CMS

This feature creates a new Enhanced CMS Workspace for each Account Engagement’s Business Unit it it activated in. Go to Marketing Setup > Copy to CMS.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-10.41.37-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-10.41.37-scaled.png) 

Copy to CMS creates a new Enhanced CMS Workspace for any Business Unit

Next to each Business Unit you want to copy assets from, click Enable. You’ll have to review an accept that Pardot’s Folder based permissions do not apply once copied. **Once Enabled, a new Enhanced CMS Workspace is created, using the naming convention *Content Workspace for Marketing Cloud Account Engagement – Copied Content – Your Business Unit Name.***

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-10.53.20-scaled.png) 

A new Enhanced CMS is created. Its name ends with the Business Unit Name

## Copy to CMS

### Emails

To copy Emails from Account Engagement to the new Enhanced CMS that Marketing Cloud Next will be able to access, we can use the Copy to CMS new option. **This option is only available for sent emails (see below for other techniques)**. Go to Account Engagement Emails > Sent. Change the View filter to All Sent Emails, so you have acces to all the previously sent emails (independently of how they were created). If you want to export on email, then click Copy to CMS in the Action column at the end of the line.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-12.46.00-scaled.png) 

Copying a single sent email to the new CMS

For multiple copy at once, select the emails by checking the column next tot their name and at the bottom of the section, select Copy to CMS in the dropdown next to With X Selected, and then Go. Once the copy is done, **you get a completion email with the status of the copy.**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20488%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-12.49.16.png) 

The Email was copied from Account Engagement, and made available to Agentforce Marketing

**From Marketing Cloud Next, you can open the Content default menu entry, and from there, open the Email in the MC Next Builder**. If you open this email in the Builder, you’ll see that it is basically a single HTML component, with the whole original email body copied into it. If your initial Email had non-inlined CSS (classes defintions for example), you email may not render correctly (see below for a workaround).

In [Salesforce documentation related to this feature](https://help.salesforce.com/s/articleView?id=mktg.mcae_when_to_use_copy_to_cms.htm&type=5), we find the following diagram. Before rebuilding an Account Engagement Email directly, you may try to copy it and see how it renders. **Merge Fields, Dynamic Content and HML are not supported**. You’ll need to recreate your Completion Actions as Flows, but, using Completion Action does not prevent the use of Copy to CMS per-se. **Same is true for images**, depending on how you declared them, they may work or not in the MC Next version.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20518%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/mcae_when_to_copy_marketing_assets.png) 

Salesforce recommendations on when to use the Copy to CMS feature

### Files

The Copy to CMS feature is also avaiable for Account Engagement Files, which can be copied as in bulk or single mode. Go to Content > Files and before you copy them, set the View Filter to **CMS Compatible** to display only [Files that can be copied](https://help.salesforce.com/s/articleView?id=mktg.mcae_supported_cms_file_types.htm&type=5).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-10-at-16.49.09-2-scaled.png) 

Bulk File copy from Account Engagement to MC Next

### Forms

Forms can be copied in the exact same way, from Content Form, on a Form by Form basis or in bulk. **The CSS style of the Form is not copied**, only the Fields are, and in the resulting Marketing Cloud Next From in the new CMS workspace, **no Data Source is selected**. Also, **Form Handlers cannot be copied as of today.**

### Landing Pages

Account Engagement Landing Pages built **with the Classic Builder** (Content > Landing Page) can be copied using the Copy to CMS feature. **Landing Pages built using the Lightning Builder do not support this feature**. Just like Emails, the whole html body from the original Landing Page in copied in a single HTML component, with only the inlined CSS remaining, so your Landing Page may or may not appear correctly in MC Next. **Finally, if a Form was included in the original Landing Pages, you will need to copy it an add it from MC Next**.

## Alternative methods

Even though the Copy to CMS is handy for simple assets, the style stripping may sometimes lead to unusable copies.

### Raw HTML export for Classic Emails

From Account Engagement Emails (Classic Buider) on Published and Draft Email Templates you can **export the raw HTML** (click anywhere inside the HTML box in the HTML tab of the email, Select All > Copy), and then create a new Email directly in Agentforce Marketing and [switch it to HTML Mode](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/html-emails-vs-code-mode/) in which you can paste the Account Engagement Email code, an Publish it. Obviously, **there is no bulk mode for this method, but the styling should be correct**. The handlebar Merge Fields won’t be recognised in MC Next, so you’ll need to replace them prior to publishin the new email.

### Lighgning Builder

In Account Engagement, there are two ways create and edit an Email:

- the **Classic Builder**, from the Account Engagement Emails menu
- the **Lighning Builder**, from the  Email Content menu

When Marketing Cloud Growth / Advanced was released, its Builder was shared with Account Engagement, and so the **Lighning Builder can be used in Current Experience mode (the original one), or New Emal Experience (MCG/A).**

When using that latter mode, the Email Content are saved in a dedicated Enhanced CMS workspace (created when using that Builder mode for the first time), and hence available from MC Next. **So that your Email Contents created using the New Email Experience are natively available to MC Next.**

When used from Account Engagement, the New Email Experience can be personnalised using the Merge Fields in the **Other category (Unsubscribe, etc.) and Recipient category**. However, when accessed from MC Next, **those Merge Fields are not compatible**, Link category must be used for Unsubscribe and Preference Center and the Data Graph must be used as the recipient Merge Fields.

**If you are currently using the Current Email Experience, you can edit your Email Contents using the New Email Experience, so that they can be used by MC Next.** Email Templates in the Current Email Experience cannot be copied, and must be created as an Email Content and then saved using the New Email Experience.

Finally, the images used by the Current Email Experience are stored in a standard CMS Workspace (where the Email Contents are also sent). **They can be selected and exported from there, and then imported in any Enhanced CMS workspace.**

## Final Thoughts

We to describe the options to recreate your asset from Account Engagement into Agentforce Marketing. However, it may also be a good time to recreate some or all of them or even imagine new experiences, by benefiting from advanced presonalisation techniques (like the [Repeaters](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/repeaters/)).

There is no out of the box tool to copy the Account Engagement Automations (Completion Actions, Automation Rules, Engagement Studio, etc.), which must be recreated as Flows. As a replacement to an Email Completion Action [see how to handle Link Clicks](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/trigger-flow-click-open-event/) in Agentforce Marketing Segment and Automation Event Triggered Flows.
