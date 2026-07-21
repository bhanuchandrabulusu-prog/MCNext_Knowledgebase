# Configure a Data 360 Web Connector

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_web_connector.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Data 360 Web Connector

To enable real-time behavioral tracking and provide the IndividualId context for personalized agent conversations, create a Data 360 web connector. The web connector captures customer engagement events and sends them to Data 360, where they enrich customer profiles for improved personalization.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To set up a web or mobile app connection:	Data Cloud Architect
Connect your website to Data 360 using a connector.

See Connect a Website or Mobile App to Data 360.

Create and upload a sitemap for the website.

A sitemap is a JavaScript file that defines the logic to capture data across different pages of your website. It's used by the SDK to collect interaction data and share it with Data 360.

See Create and Upload a Sitemap.

Add this JavaScript configuration to the sitemap section.

Use the configuration values from your Enhanced Chat deployment. See Step 7 in Create an Enhanced Chat Deployment.

// Set local session variable with constants needed to power the Adaptive Web
// Agent Component (AWAC)
if (window.sessionStorage.getItem("SEARCH_COMPONENT_WEB_STORAGE_00D1Q000001fdJS") == null) {
    window.sessionStorage.setItem(
        "SEARCH_COMPONENT_WEB_STORAGE_00D1Q000001fdJS", 
        JSON.stringify({
            ORGANIZATION_ID: "00D1Q000001fdJS",
            MESSAGING_URL: "https://pspdemo.my.salesforce-scrt.com",
            DEPLOYMENT_DEVELOPER_NAME: "Web_Curation_Custom_Channel"
        })
    )
}
// This function must be generated from the Adaptive Web Agent Component (AWAC)
// Library and added to the sitemap
window.addSearchComponentToPage()
// YOU MUST ADD THIS SECTION FROM AWAC REPO
function addSearchComponentToPage() {
    // LIBRARY COMPILED CODE GOES HERE
}

This JavaScript connects Data 360 behavioral tracking, your website's session storage, and the Adaptive Web Agent Component (AWAC) so that the agent can conduct meaningful conversations using real-time customer context and product data.

NOTE The sessionStorage key includes the OrgId (for example, SEARCH_COMPONENT_WEB_STORAGE_00D1Q000001fdJS). If you ever change the JSON configuration values, you must update the key.
SEE ALSO
Salesforce Help: Web and Mobile App Connector
