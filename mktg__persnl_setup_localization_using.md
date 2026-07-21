# Using Localization for Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_localization_using.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Using Localization for Personalization

Deliver language-consistent recommendations to global audiences by using automatic attribute fallbacks and translation schemas.

Maintain a single source of truth across your global data spaces by localizing only the fields that require translation. This approach ensures that non-localizable data in your Root Data Model Object (DMO), like pricing or SKUs, remains consistent while the system dynamically serves translated content where it matters most.

Key Considerations

When setting up localization, keep these considerations in mind:

Global Control: You can enable or disable localization at any time across all data spaces to manage feature rollout.
Locale Matching: Personalization uses the locale field you select during item definition to match requests to your customer’s preferred language.
Reliable Fallbacks: To prevent gaps in the user experience, Personalization checks the decision request, then the customer's profile data, then item defaults when determining a locale.
Localization Benefits

Review the benefits of using localization to maintain a single source of truth across your global data.

BENEFIT	DESCRIPTION
Ensure Language Consistency	Prevent mixed-language experiences, such as a Spanish title with English body text, by using precise translation schemas.
Simplify Data Management	Save time by automatically pulling non-localizable data, such as prices or SKUs, directly from the Root DMO.
Respect Localization Intent	Maintain more granular control by ensuring that intentionally blank fields do not trigger an accidental fallback.
Localization Fallback Logic

To ensure a consistent user experience, Personalization evaluates locale data in two stages: first by determining the locale using a priority order, and then by evaluating specific attribute data within the DMO.

Hierarchy for Determining the Locale

Personalization checks for a locale value in this order:

Decision Request: Personalization first looks for a locale value in the decision request. To include a locale value in the decision request, configure it in your sitemap. For more information, see Sitemap Implementation.
Profile Locale Fallback: If no locale value is in the decision request, Personalization looks for a locale attribute on the profile data graph. You can configure this in Personalization Setup.
Default Value: If no locale value is found in either the decision request or the profile data graph, Personalization uses the default language and currency values.

Field-Level Fallback Actions

Review these system actions and results to understand field-level fallback behavior:

ATTRIBUTE STATUS	SYSTEM ACTION	RESULT
Absent from the schema	Returns the value from the default locale in the Root DMO.	The field populates with default data, such as a global inventory count or a default image.
Defined but left blank	Treats the blank as an intentional choice.	The field remains blank. No fallback occurs to ensure your intentional formatting is preserved.
SEE ALSO
Configure Localization for Salesforce Personalization
