# Configure Localization for Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_localization_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Localization for Salesforce Personalization

Configure localization in Salesforce Personalization Setup to deliver recommendations in your customers' preferred languages.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure localization:	Change and Edit
From Setup, in the Quick Find box, enter Personalization, and then select Personalization Setup.
If you already have the recommender open, go to the next step.
Under Personalization Setup Options, click the Advanced Setup tab.
In the Localization section, turn on Localization.
Click Select Data Space.
Select a data space that contains the data graphs you want to localize.
NOTE The selected data space must have Salesforce foundational data already deployed.
Define the item localization Data Model Object (DMO):
Select an item data graph containing a DMO with a locale-related field.
Select the localization DMO and field used to determine the locale.
(Optional) Define a profile locale fallback value to determine a locale when a decision request doesn't include one:
Select a profile data graph containing a DMO with a locale-related field.
Select the locale-related attribute used to determine the fallback locale.
NOTE To pass a locale value directly in the decision request, configure it in your sitemap. For more information, see Sitemap Implementation. If a locale value is present in the decision request, the profile locale fallback isn't used.
Click Save.
