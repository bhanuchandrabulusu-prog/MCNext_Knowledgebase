# SFMC Tips #16 : How to Exclude Subscribers with a Specific Email Domain in Salesforce Marketing…

**Source:** https://medium.com/@marketingcloudtips/how-to-exclude-subscribers-with-a-specific-email-domain-in-salesforce-marketing-cloud-c45cd4096cbe

---

# SFMC Tips #16 : How to Exclude Subscribers with a Specific Email Domain in Salesforce Marketing Cloud

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c45cd4096cbe---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c45cd4096cbe---------------------------------------)

3 min read

·

Jan 9, 2024

--

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In certain situations, there may be instances where you prefer not to share information with a competing company, such as Company A. In such cases, utilizing the domain exclusion feature in Salesforce Marketing Cloud allows you to collectively exclude subscribers with the email domain of your competitors from your email communications.

To employ this feature, you need to create a dedicated data extension called “DomainExclusion” for domain exclusion.

1. Click on [Email Studio > Subscribers Tab > Data Extensions].  
2. Click the [Create] button in the upper right corner.  
3. Choose “Standard Data Extension” and click [OK].  
4. In the creation method, select **[Create from Template]** from the dropdown.  
5. Choose **“DomainExclusion”** and click [OK].

This action will create “DomainExclusion” in the top-level folder of your data extensions. Please note the following considerations:

- You can create multiple domain exclusion data extensions.
- It doesn’t need to be a sendable data extension.
- This data extension only stores the Domain field.
- Enter the domain **after the “@” symbol (e.g., gmail.com)**.

The setup for the domain exclusion feature can be found in the “Delivery Options” section within the Email Activity. Only the data extension created through the mentioned steps will be available for selection in this feature.

As a cautionary note, this feature cannot be used in the Mail Send Activity within Automation Studio. If domain exclusion is needed in Automation Studio, handle it in advance using activities like SQL Query.

Additionally, information on how excluded subscribers appear in the “Extract Not Sent” list and reasons for their exclusion has been covered in a previous article. Please refer to the provided link.

[## SFMC Tips #13 : How to Identify Reasons for Failed Email Sends in Journey Builder

### In cases where email sends fail in the Journey Builder of Salesforce Marketing Cloud, you may want to investigate the…

medium.com](/@marketingcloudtips/how-to-identify-reasons-for-failed-email-sends-in-journey-builder-3731fde54ec5?source=post_page-----c45cd4096cbe---------------------------------------)

For insights into whether excluded contacts exit a journey immediately or remain in the path after domain exclusion in Journey Builder, please check the following article.

[## SFMC Tips #3 : Which types of ‘contacts unable to receive emails’ can pass through Journey…

### Why is it important to understand which types of ‘contacts unable to receive emails’ can pass through the email…

medium.com](/@marketingcloudtips/what-types-of-contacts-can-pass-through-journey-builders-email-activity-d240bff65fff?source=post_page-----c45cd4096cbe---------------------------------------)

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
