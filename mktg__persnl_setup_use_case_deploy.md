# Deploy a Preconfigured Personalization Use Case

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_use_case_deploy.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Deploy a Preconfigured Personalization Use Case

Deploy a recommender-based use case that generates personalized, targeted recommendations for individuals to advance a specific business-related goal. The use case setup process currently supports two predefined use cases–Maximize Revenue and Maximize Clicks. These predefined objectives map and include certain Data 360 entities in your profile and item data graphs.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To deploy a preconfigured use case:	Personalization Intelligence Admin permission set

To create and deploy a preconfigured use case:

In the org containing your Personalization install, click Setup and select Personalization Setup.
Under Personalization Setup Options, click the Use Case Setup tab.
In the Deploy Preconfigured Use Cases section, select a data space that you want to deploy the use case to and click Select.
In the Use Case Selection dialog, select the use case that you want to use and click Next.
	
Maximize Product Revenue	Returns recommendations intended to increase checkout frequency, increase cart value at checkout, or both.
Maximize Article Clicks	Returns articles that are organized to maximize clicks based on current abd historical article interaction from machine learning.
In the Use Case Verification and Setup dialog:
Select a unified individual data model object (DMO) to base your real-time profile data graph on.
The unified individual object enables identity resolution using match rules (for example, matching IDs, names, phone numbers, and so on) to consolidate individual data sources into a single record.
Review the data model objects and DMO field mappings required for the use case deployment.
The use case setup process automatically flags any required objects that are missing from the data stream and any unmapped object fields using a red X icon.
To repair any missing or unmapped values, access the Behavioral Events data stream.
When use case verification determines that all values are included and properly mapped, as indicated by green checkmark icons, the Deploy button becomes active.
Click Deploy.

After successfully deploying your use case, you must set up the personalization point with any decisions that you want to provide. See Add a Decision to a Personalization Point for details

SEE ALSO
What to Know About Personalization Use Case Setup
What the Use Case Setup Deploys
