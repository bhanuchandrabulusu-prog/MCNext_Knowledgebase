# Differences Between Developing Apps on Data 360 and the Salesforce Platform | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/app-dev-comparison.html

---

Check out the tools and APIs that are available for custom app development in Data 360, and compare them to those available in the Salesforce Platform.

Task	Data 360	Salesforce Platform
Customer developers: Migrate metadata from one org to another	Use one of these packaging features or APIs.
Unmanaged packages
Second generation managed packages
Data kits
DevOps Center
Data 360 Metadata API
Salesforce Metadata API
	Use one of these features or APIs.
Unlocked packages
Unmanaged packages
DevOps Center
Scratch Orgs
Salesforce Metadata API

Salesforce partners: Distribute apps to customers	
Data kits
Managed packages
	
Managed packages

Environments for custom app development and testing	Sandbox org with Data 360 (beta). Altenatively, customer developers use a second org for development and testing. Salesforce partners use a Partner Business org.	Sandbox org for customer developers. Scratch orgs or sandboxes for Salesforce partners.
Managed Package Generation	First-generation and second-generation managed packages with data kits.	First-generation managed packages and second-generation managed packages.
API Authentication	When using Data 360 API, requests are authorized via OAuth with a Salesforce access token, which is exchanged for a Data 360 access token. The requests reach the Data 360 tenant-specific endpoint. When using Connect API, the same OAuth authorization path as the Salesforce Platform APIs is used.	When using Salesforce Platform APIs, requests are authorized for the org’s MyDomain endpoint via a Salesforce access token.
SOQL Queries	To query records in Data 360, you can use a subset of SOQL. For more information about what’s supported and the limitations, see Data 360 Query Profile Parameters in the REST API Developer Guide.	To query records in Salesforce, you can use SOQL. For more information, see SOQL and SOSL Reference.

See Also

Data Cloud Development Environments
App Development Lifecycle
