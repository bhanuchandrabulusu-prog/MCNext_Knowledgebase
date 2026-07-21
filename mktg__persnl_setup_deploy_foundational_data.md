# Deploy Personalization Foundational Data

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_deploy_foundational_data.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Deploy Personalization Foundational Data

Deploying Salesforce Personalization foundational data installs objects and preconfigured insights required for Personalization to function with Data 360.

To help with required Data 360 setup, a data kit is installed after you purchase Salesforce Personalization. The data kit contains foundational data necessary for Personalization to work with Data 360.

IMPORTANT

We recommend that you install and configure Data 360 before setting up Personalization and deploying foundational data.

Deploying Personalization foundational data installs and configures required components and configurations in the data space that you select.

REQUIREMENT	DEPLOYMENT
Data Model Objects (DMOs)	

These data model objects (DMOs) are installed:

Personalization Point DMO
Personalization Decision DMO
Personalization Content Schema DMO
Personalizer DMO
PersonalizationLog DMO

Connectors and Data Streams	

A Salesforce CRM data stream is created for these DMOs:

Personalization Point DMO
Personalization Decision DMO
Personalization Content Schema DMO
Personalizer DMO
PersonalizationLog DMO

The ingestion API connector and data stream is created for the Personalization Log DMO (including the Ingestion API Schema File)


Object Mapping	Installed DMOs are fully mapped during data stream creation.
Calculated Insights	

These calculated insights are installed, but must be manually scheduled:

Daily Personalization Uniques
Daily Personalization Requests

To deploy foundational data:

In the org containing your Personalization install, click Setup and select Personalization Setup.
Under Personalization Setup Options, click the Foundational Setup tab.
In the Deploy Foundational Data section, click Select Data Space.
Select a data space that you want to deploy foundational data to and click Deploy.
