# Create a Custom Attribution Configuration

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_attrib_config_custom_create.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create a Custom Attribution Configuration

Instead of using the predefined attribution configurations, you can create your own custom attribution configurations using first-or last-touch models to better meet your needs. These custom configurations can help you evaluate how well your personalization decisions or strategies are working. By defining your own engagement signals and metrics, you can configure a two- to four-stage funnel stage configuration to track customer journeys from initial impression to conversion.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure a custom attribution configuration:	Personalization Intelligence User
From the App Launcher, search for and select Attributions.
Click New.
Select the data space where you want to create and use the attribution model.
Select the identity resolution ruleset that you want to use for the attribution model.

For data model objects that don’t require the use of an identity resolution ruleset, like the Individual object, you can choose the No IR Ruleset option.

Specify a name for the attribution model.
Click Next.
Define the parameters that you want to use for this attribution configuration.
Select either a First Touch or Last Touch attribution model type.
OPTION	DESCRIPTION
First Touch	Multiple qualifying engagements for a desired business conversion are resolved by assigning the first engagement 100% of the value. ‌For example, if an individual purchases a product that was recommended three different times within the attribution window, the first engagement (view or impression) receives 100% of the value for that purchase.
Last Touch	Multiple qualifying engagements for a desired business conversion are resolved by assigning the last engagement 100% of the value. For example, if an individual purchases a product that was recommended three different times within the attribution window, the last engagement (view or impression) receives 100% of the value for that purchase.
Select an attribution window to use for this model.
Click Next.
Define at least 2 funnel stages that map an individual’s personalization journey. You can define up to 4 stages.
Select an engagement signal to use for the funnel stage. An engagement signal defines an engagement action that an individual can take during the personalization journey. For more information about engagement signals, see Engagement Signals and Engagement Signal Metrics.
For an engagement signal to be eligible for use in a funnel stage, it must have an active relationship with the Personalization Log DMO.
For Stages 2 through 4, select whether you want to enable Content Match. Content matching links item attribution from one funnel stage to the previous stage. For example, if you enable content matching for an add-to-cart stage, attribution occurs only if the item added to the cart is the same item engaged with in the previous stage. If content matching is disabled for the add-to-cart stage, attribution occurs if any item is added to the cart, even if the item wasn’t engaged with before.
Move any metrics that you want to report on from the Available Metrics pane to the Selected Metrics pane.
To save a draft of the new attribution configuration without enabling it, click Save Draft. You can enable a draft attribution model at any time.
To save and enable the new attribution model, click Save & Enable.
Create the Personalization Point output data model objects (DMOs) that you want to use when gathering attribution data. The attribution model uses two separate data model objects when gathering data‌. When creating these DMOs, make sure to name them differently.
DATA MODEL OBJECT	DESCRIPTION
Personalization Point Output DMO	This DMO gathers personalisation point-specific attribution data.
Personalization Point Content Output DMO	This DMO gathers content-specific attribution data.
SEE ALSO
Types of Salesforce Personalization Analytics
Deploy Preconfigured Personalization Attribution Intelligence Data
View Attribution Intelligence for Active Attribution Configurations
Using the Personalization Attribution Intelligence Dashboard
Salesforce Personalization Data Model Objects
