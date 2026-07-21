# Experimentation Assignment API

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/experimentation-api-reference.html

---

Use the Experimentation Assignment API to request experiment cohort assignments for your users based on data from Salesforce Data 360.

https://{tenantSpecificEndpoint}

Replace tenantSpecificEndpoint in the base URI with the Tenant Specific Endpoint of your Data 360 tenant before adding this code to your Sitemap. To find your Tenant Specific Endpoint, see Data 360 Integration Guide: Share Ingestion API Developer Information.

Supported Operation	HTTP Method	URI
Request experiment assignment	POST	/experimentation/v1/authenticated/assignment
