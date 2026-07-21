# Create a Personalization Campaign

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_campaign_create.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create a Personalization Campaign

Configure a personalization campaign using a guided configuration process that steps you through creating, mapping, and deploying a personalized experience.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure a Personalization campaign	Personalization User

To create a personalization campaign:

From the App Launcher, search for and select Personalization Campaigns.
Click New Campaign
Specify a name for the campaign and an optional description.
The API name is auto-generated.
Click Continue.
Select a data space to use for the campaign. The data space that you select determines what data is available for use in the campaign.
If your business has multiple data spaces that separate various brands or departments, make sure to select the appropriate data space for your campaign business goals.
Select a profile data graph. The menu shows only profile data graphs contained in the selected data space.
A profile data graph combines and organizes object data into a structured view that Personalization uses to determine what individuals (for example, customers or site visitors) are eligible to receive personalized content. The data graph enables near real-time retrieval of unified customer profiles, based on gathered behavior and engagement data.
Select a strategy for the personalization campaign.
Personalization campaign creation currently supports the Dynamic Content strategy. This strategy enables you to define content attributes and apply them using predefined templates.
Select a marketing channel that you want the campaign to use.
Options provided are specific to the selected channel. Personalization campaign creation currently supports only a web marketing channel option.
Select a predefined Data 360 web connector that you want to use for deploying the campaign and click Next.
Select a content schema. The content schema is channel independent and defines available attributes for the campaign. Selecting a content schema displays available templates for use with the selected channel.
Select an experience template to use with the campaign. Experience templates are channel dependent and define how personalized content appears on a website.
Define a decision and its associated content for the campaign.
Personalization decisions use targeting rules to determine who’s eligible to receive personalization response and what content to return.
Name the decision.
(Optional) Specify a priority for the decision. By default a single decision has a priority of 1. When you create multiple decisions, it’s possible for individuals to qualify for more than one. By prioritizing decisions, you can define what decision Personalization returns to individuals.
Choose a status for the decision. All decisions are enabled by default. However, you can choose to disable a decision and re-enable it when you want to use it.
In the Template Preview section, define the content that you want the decision to provide. Depending on the template you select, this content can contain various options including call-to-action (CTA) text, header or subheader text, background images, and so on.
(Optional) Add any merge fields for the content you define in the template. Using merge fields enables you to include profile data directly into your text. For example, you can include your user's first name within a text-based element to greet them personally. See Add a Merge Field for more information.
(Optional) Add any targeting rules to define who is eligible for the decision.
If no targeting rules are defined, the decision content is made available to all individuals. For more information about targeting rules, see Create a Targeting Rule
(Optional) Add a new decision.
Personalization campaigns can contain multiple personalization decisions targeted at different sets of individuals. The order you create decisions in initially determines their priority. However, you can modify the priority of any decision you create.
Click Next.
The Personalization Campaign Details page opens to show the full campaign configuration.
(Optional) To make any changes to the campaign, use the Back button to navigate to the page that you want to modify.
Click Save and Finish.
Personalization creates the campaign. Before you can use the campaign, you must map it to a channel.
(Optional) To exit the campaign configuration without mapping it, close the prompt window. You can finish mapping the campaign at any time from the Related tab in the campaign record.
To map the campaign, click Continue to mapping.
Personalization opens the campaign record Related tab. Go to Map a Campaign Using Web Personalization Manager to continue.

Personalization campaigns appear in the Personalization Campaigns tab after they're created. In this tab you can edit, delete, or view individual campaigns.

WARNING Editing decisions in a campaign impacts what personalized content appears to customers in all mapped channels for that campaign.

The personalization point created during the guided campaign configuration process appears in the Personalization Points tab. Personalization points created through the campaign process show a Personalization Campaign designation in the Source column of the Personalization Points table.

SEE ALSO
Prerequisites for the Personalization Campaign Guided Configuration
Using the Personalization Campaign Guided Configuration
Map a Campaign Using Web Personalization Manager
Assign a Default Data Graph to a Data Space
Configure a Personalization Content Schema
Add a Decision to a Personalization Point
Create a Targeting Rule
