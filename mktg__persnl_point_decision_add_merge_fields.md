# Add a Merge Field

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_point_decision_add_merge_fields.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Add a Merge Field

To include profile data in personalization decision text, use merge fields.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To add merge fields to personalization decisions:	

Create and Edit Personalization Points

Create and Edit Personalization Decisions

From the App Launcher, search for and select Personalization Points.
Open a personalization point.
Create or select a personalization decision.
On the Decision Configuration tab, click Add Merge Field next to a personalization attribute text field.
Select an attribute that you want to add as a merge field. You can select either direct attributes or segment memberships.
Direct attributes provide attributes that are defined on the root data model object (DMO) of your profile data graph.
Segment memberships list all segment IDs that the individual is a member of.

For an example of how to render segment membership data on your website, see Display Segment Membership in Merge Fields (Example).

NOTE If you want the segments to be selectable, add the segment memberships object to your profile data graph and select the segment ID field on the data graph definition.
Enter an API name for the merge field. The API name is auto-generated for a direct attribute, however you can edit the name if you prefer. Segment memberships have a per-defined API name.
Enter the default text that you want to appear in place of the merge field when no attribute value is found.
For example, If you provide “Valued Customer” as a default text for first name, Salesforce Personalization replaces “Dear {first_name}” with “Dear Valued Customer” if no value is found for the first name. If you don't want any text to appear or if you want to use the available reference template to render segment memberships, leave this field blank.
Click Save.
Display Segment Membership in Merge Fields (Example)
To deliver Data 360 segment membership IDs on your website, use merge fields. In this example, we show you how to personalize customer experience by displaying Data 360 segment membership information on your website.
