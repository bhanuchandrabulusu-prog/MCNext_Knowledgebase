# App Development Lifecycle | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-app-lifecycle.html

---

The app development lifecycle includes planning and gathering requirements, creating the app, testing the app, making iterative changes to fix issues, and performing user-acceptance testing as a final test. The final step for an app developed in-house is the app’s release to production. The final step for an app developed by a Salesforce partner is app distribution to other Data 360 customers who purchase the app.

If you’re a Salesforce partner, the development lifecycle also includes distributing, marketing, selling, and supporting your app.

For more information about the Salesforce partner program, check out the Build Apps as an AppExchange Partner trail. This trail is intended for development on the Salesforce platform and isn’t customized for Data 360, but it contains some useful information about the program.

We encourage customers to purchase apps from Salesforce partners rather than building them themselves. Installing and using apps from AppExchange ensures that the app is maintained regularly and meets quality and security standards. In addition, AppExchange apps save customers time and resources.

Third-party apps that are available on AppExchange are for data activation and data enrichment. To find AppExchange apps AppExchange for Data 360, see Data 360 product collection on AppExchange.

If you’re a Salesforce partner, you’re familiar with the package development workflow, and you know that the workflows and tools for developing a first-generation managed package and second-generation managed package are distinct.

To learn about building apps on AppExchange, check out these resources.

First-Generation Managed Packaging Developer Guide
Second-Generation Managed Packaging Developer Guide
ISVforce Guide
Salesforce Help: Build and Share Data 360 Functionality
Trailmix: Building Data Cloud Activation Platform Apps for ISVs

Customer developers who develop an app in-house for their own org can use a separate test org for creating and testing their apps. You can use a sandbox org with Data 360 (beta) for testing, or you can use a test org. The Data 360 test org is also a production org, and service usage results in billing charges the same way as on the production org. See Cost and Usage. To request a Data 360 test org, contact your Account team.

The app development lifecycle model described in this section uses an org dedicated for development and testing and the Data 360 production org. In this model, you develop and test the app on one Data 360 org and release it to production. You migrate the app and configuration settings to the production org using unmanaged packaged, data kits, or Metadata API.

See Also

Packages and Data Kits
Metadata API
Salesforce Help: Data Cloud in a Sandbox (Beta)
