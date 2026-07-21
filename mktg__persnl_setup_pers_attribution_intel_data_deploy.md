# Deploy Preconfigured Personalization Attribution Intelligence Data

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_pers_attribution_intel_data_deploy.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Deploy Preconfigured Personalization Attribution Intelligence Data

If you plan to track attribution for add-to-cart, order, or revenue metrics, you can deploy preconfigured Salesforce Personalization attribution intelligence data to Data 360. Attribution analysis requires the product browse engagement, shopping cart engagement, and product order engagement objects. If you don’t plan to use these objects, then deploying personalization attribution objects to Data 360 isn't necessary.

IMPORTANT You can deploy attribution intelligence data in any data space running the Personalization app. The deployment process automatically checks whether you have already deployed attribution data to the selected data space.

Deploying Personalization attribution intelligence data installs and configures preconfigured attribution components and configurations in the data space that you select using the identity resolution ruleset you choose. This data includes necessary data lake and data model objects, and two preconfigured first touch and last touch attribution models.

To ensure unique object naming, Personalization uses these naming conventions when deploying preconfigured components:

Installed objects use a naming convention of {dataspacePrefix}_{irSuffix}_{objectBaseName} for data lake objects (DLOs), and {dataspacePrefix}_{irSuffix}_{objectBaseName}__dlm for data model objects (DMOs).
The default dataspace doesn’t have a prefix, so selecting this dataspace doesn’t add a prefix or underscore to the beginning of the object name. Selecting any other dataspace adds a prefix and underscore to the object name.
When deploying attribution intelligence, you must choose a data space. However, selecting an identity resolution ruleset is optional. If no identity resolution ruleset is selected, no {irSuffix} value is added.
If you select an identity resolution ruleset with an empty suffix, Personalization prepends the value e_s_ as the {irSuffix} value to indicate the empty suffix.
API names can’t start with a number. If the identity resolution ruleset starts with a number and the default dataspace is used (meaning that no data space prefix is included), Personalization adds n_s_{irSuffix} as the prefix.
COMPONENTS	ATTRIBUTION DEPLOYMENT
DLOs	

These attribution DLOs are created:

{dataspacePrefix}_{irSuffix}_PersnlPointFirstTouchViewAttr
{dataspacePrefix}_{irSuffix}_PersnlPointLastTouchViewAttr
{dataspacePrefix}_{irSuffix}_PersnlContentFirstTouchViewAttr
{dataspacePrefix}_{irSuffix}_PersnlContentLastTouchViewAttr

DMOs	

These attribution DMOs are created:

{dataspacePrefix}_{irSuffix}_PersnlPointFirstTouchViewAttr__dlm
{dataspacePrefix}_{irSuffix}_PersnlPointLastTouchViewAttr__dlm
{dataspacePrefix}_{irSuffix}_PersnlContentFirstTouchViewAttr__dlm
{dataspacePrefix}_{irSuffix}_PersnlContentLastTouchViewAttr__dlm

Attribution Models	

These attribution models are created:

{dataspacePrefix}_{irSuffix}_DefaultAttribution_FT
{dataspacePrefix}_{irSuffix}_DefaultAttribution_LT

The attribution models combine and display both the personalization point and content first touch and last touch DMO attribution data.


Connectors and Data Streams	A Salesforce CRM data stream is created for each attribution DMO.
Object Mapping	Attribution DMOs are fully mapped during the optional attribution installation.
Calculated Insights	No added calculated insights are installed. However, we do provide some example calculated insights that you can install using SQL.

To deploy preconfigured Personalization attribution intelligence data:

From Setup, click Personalization Setup.
Under Personalization Setup Options, click the Foundational Setup tab.
In the Personalization Attribution Intelligence Setup section, click Select Data Space and IR Ruleset.
Select a data space that you want to deploy attribution intelligence to.
The data space you select must already have Salesforce Personalization foundational data deployed.
(Optional) In the Identity Resolution Ruleset column, select an identity resolution ruleset to use when deploying the attribution intelligence data.
Click Deploy.
SEE ALSO
Salesforce Personalization Analytics
Salesforce Help: Identity Resolution Rulesets
Calculated Insight Example SQL Expressions
