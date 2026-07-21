# Configure a Custom Ruleset

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_qs_configure_a_custom_ruleset.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Custom Ruleset

You can manually configure a custom ruleset for the Individual or Unified Individual object. A custom ruleset creates unified records that meet your specific business needs and specifications.

For Salesforce Personalization, real-time identity resolution allows you to collect data as and when there is a profile match and store details in the data graphs. This data provides deep understanding about an individual for decision targeting and to generate recommendations.

For the latest data available, you can configure real-time identity resolution for Salesforce Personalization. See Real-Time Identity Resolution for Personalization.

These instructions refer to the standard identity resolution rulesets, which are batched as scheduled.

Create a ruleset. If you have a ruleset to use, skip this step.
On the Identity Resolutions tab, click New.
Select Create New Ruleset, and then click Next.
Select the data space that you use for marketing, and then select Account or Individual for the Primary Data Model Object.
Enter an ID for the ruleset, and then click Next.
This 4-character ID is appended to the API name to distinguish between rulesets.
Name the ruleset and save your work.
From the identity resolution record, create custom rules.
In the Match Rules section, click Configure.
Follow the prompts to define the rules that unify related records.
If your ruleset is for the Individual object, add the Add Recommended Rules to Your Identity Resolution Ruleset.
Define which object to use for personalization.
From Setup, in the Quick Find box, enter Basic, and select Basic Settings.
In the Create an Identity Resolution Ruleset section, select the Unified Individual or Unified Account object related to your ruleset.
