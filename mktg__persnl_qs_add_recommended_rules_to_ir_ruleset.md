# Add Recommended Rules to Your Identity Resolution Ruleset

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_qs_add_recommended_rules_to_ir_ruleset.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Add Recommended Rules to Your Identity Resolution Ruleset

To get the most out of Identity Resolution, we recommend adding two custom rules to the Individual object ruleset. First, add a rule to match exact values when a lead converts to a contact. If you use web tracking on Marketing Cloud Next landing pages or a connected external site, add a rule that attributes activity to the correct unified individual.

Because Salesforce Personalization supports real-time identity resolution, you can also configure rules that best support your business needs and use cases. Consider these notes as you develop your strategy.

Real-time identity resolution is supported on exact match and exact normalized matching for emails and phone numbers.
Fuzzy matching conditions are batch processed at the data lake level.
To make sure that real-time data is applied to identity resolutions, use the unified individual object for your profile data graph.

For more recommendations, see Real-Time Identity Resolution for Personalization.

Go to the Identity Resolutions tab, and then open the ruleset that you created for the Individual object.
Under Match Rules, click Edit, and then click Next.
Click Add Match Rule.
Click Custom Rule, and then click Next.
Name your rule. For example, "Lead to Contact" or "Device Visitor Identification."
Select the match criteria.
For Data Model Object, select Identity Match.
For Field, select Identity Match Type.
For Match Method, select Exact.
Under Advanced Settings, click Configure, and then enter the Identity Match Type for the first custom rule.
For lead to contact conversion, enter lead-to-contact.
For web tracking attribution, enter device-to-known.
Click Back To Basic Settings, and then click Next.
To add the second rule, repeat steps 3 through 8 and use the remaining Identity Match Type.
Save your work.
