# SFMC Tips #14 : Dynamically Setting Reply-to Email Addresses for Each Contact

**Source:** https://medium.com/@marketingcloudtips/dynamically-setting-reply-to-email-addresses-for-each-contact-in-salesforce-marketing-cloud-11f541c0d57f

---

# SFMC Tips #14 : Dynamically Setting Reply-to Email Addresses for Each Contact

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--11f541c0d57f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--11f541c0d57f---------------------------------------)

2 min read

·

Dec 27, 2023

--

Photo by [Jezael Melgoza](https://unsplash.com/@jezar?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In some companies, there are cases where a central team at the headquarters sends out emails to customers managed by various branches. In situations where you want customers to reply to the received emails and have the ability to reply to the email addresses of each branch, it can be convenient to dynamically set the reply-to email addresses for each branch.

At first glance, it may seem that Salesforce Marketing Cloud’s standard features allow you to select only one reply-to email address. However, it is possible to achieve dynamic reply-to addresses. Note that this feature is not enabled by default, and you need to raise a case with technical support to activate it. Although the help document below provides information on this feature, it is not visible by default, so take note of it on this occasion.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_es_dynamically_populate_reply_name_and_address.htm&type=5&source=post_page-----11f541c0d57f---------------------------------------)

To request activation from technical support, simply ask them to enable the **“Populate Reply-to Address Dynamically”** feature.

When activated, the option “Insert Reply Address Dynamically” will appear below the “Routing” section in the “Reply Mail Management (RMM)” as described above.

Enabling the feature does not make it instantly functional. **By default, the feature is “Off”**, and the Reply Mail Management (RMM) settings take precedence. When you turn it “On”, the Reply Mail Management (RMM) settings become disabled, and the “Populate Reply-to Address Dynamically” feature becomes active.

Regarding the “Reply Name” and “Reply Email” when set to “On”, you can dynamically display them by creating “branch\_name” (branch name) and “branch\_email” (branch email address) fields in the data extension of each contact in the entry source. Populate these fields with the respective values. Note that “branch\_email” can be a **text type**, not necessarily an email address type.

Refer to the attached diagram for configuration guidance. That concludes the information for this session.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
