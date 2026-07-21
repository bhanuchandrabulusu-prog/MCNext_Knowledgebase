# Add the Web SDK to Your Website

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_add_the_web_sdk_to_your_website.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Add the Web SDK to Your Website

To power intelligent agent conversations with real-time customer context, add the connector script to your web pages. This setup connects Data 360 behavioral tracking, session storage, and the Adaptive Web Agent Component (AWAC) using your specific deployment configuration.

Add the Web SDK script.
From Setup, go to your web connector definition, and then locate your unique CDN script URL at the bottom.
Add this script URL to the <head> tag of your web pages.
Initialize the Web SDK.

Initialize the SDK by calling SalesforceInteractions.init(). During development, we recommend setting the logging level to 4 (Debug).

<head>
    <script src="https://cdn.c360a.salesforce.com/beacon/c360a/YOUR_CONNECTOR_ID/scripts/c360a.min.js"></script>

    <script>
        // Initialize the SDK
        SalesforceInteractions.init(); 
        
        // Set logging level for debugging (remove in production)
        SalesforceInteractions.setLoggingLevel(4); 
    </script>
</head>

When you load your website, the Adaptive Web Agent Component loads on the page.

SEE ALSO
Developers: Initialization
