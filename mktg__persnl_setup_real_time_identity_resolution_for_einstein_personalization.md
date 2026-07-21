# Real-Time Identity Resolution for Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_real_time_identity_resolution_for_einstein_personalization.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Real-Time Identity Resolution for Personalization

Real-time identity resolution matches information about active users to a unified profile object, consolidating profile data from different sources. Each unified profile contains all unique contact point values from all sources, providing a comprehensive view of each individual. Combining real-time identity resolution and Salesforce Personalization, you can deliver personalized content to individuals using your app or website within milliseconds.

When configuring real-time identity resolution, keep these considerations in mind.

Before you can use identity resolution, you must map Personalization data lake objects to data model objects.
For real-time personalization, create a custom match rule to match on party identifiers using these criteria.
PARAMETER	VALUE
Object	Party Identification
Field	Identification Number
Match Method	Exact
Match on Blank checkbox	Unchecked
Party Identification Type	Review data in the fields mapped to Party Identification Type and Party Identification Name to determine which values in your data you want to use for matching.
Party Identification Name
Match Rule Name	Provide a unique name, up to 80 characters, for the custom match rule.
Identity resolution uses the same reconciliation rules in all modes, regardless of whether match rules are scheduled or real time. See Identity Resolution Reconciliation Rules.
When using real-time matching, identity resolution compares the value provided by the Personalization app to unified profile records in the ruleset’s related real-time data graph.
When an existing customer is identified, these actions are triggered.
Real-time insights based on the unified profile are calculated. Results are saved to the real-time data graph record.
Real-time segments based on the unified profile are built. Segmentation is saved to the real-time data graph record.
The updated real-time data graph record becomes available to the Personalization app.
SEE ALSO
Salesforce Help: Unify Source Profiles
Salesforce Help: Identity Resolution Match Rules
