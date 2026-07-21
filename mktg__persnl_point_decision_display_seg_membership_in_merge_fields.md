# Display Segment Membership in Merge Fields (Example)

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_point_decision_display_seg_membership_in_merge_fields.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Display Segment Membership in Merge Fields (Example)

To deliver Data 360 segment membership IDs on your website, use merge fields. In this example, we show you how to personalize customer experience by displaying Data 360 segment membership information on your website.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To add merge fields to personalization decisions:	

Create and Edit Personalization Points

Create and Edit Personalization Decisions

Create a Manual Content personalization response template and add Segments as a personalization attribute. See Configure a Personalization Response Template.
Create a Handlebars web experience template for your website connector.

This enables business users to select the template in the Web Personalization Manager (WPM) and deliver segment membership data directly to the page. See Create an Experience Template.

Create a personalization point using the response template you created in step 1.

The personalization point acts as the bridge between your data and the web experience.

Add a decision to the personalization point.
Configure a Segment Memberships merge field on the available personalization attribute. See Add a Merge Field.

To ensure that the necessary data is available to the page at runtime, make sure that the profile data graph used in your personalization point includes the Segments object related to the root DMO. Additionally, within the Data Graph definition, verify that the Segment ID field is selected

Update the sitemap.

To ensure that the segment memberships returned in a personalization decision response are properly written to both the console and window object, add this snippet to the sitemap or directly to the site.

/* START: External Segments */
SalesforceInteractions.Personalization.Config.ContentZoneHandler.set("Export_Segments", {
  onReady: (content) => {
    let segments = []
    try { 
      segments = JSON.parse(content) 
    } catch(err) {
      // Handle parsing error
    }
    console.log("segments returned are: ", segments);
    window.sfdcSegments = segments;
  }
});
/* END: External Segments */

Deploy a new experience to your site using Web Personalization Manager (WPM).
Open Web Personalization Manager on your website and navigate to the target page. See Access Web Personalization Manager.
Create an experience and select Configure Embedded Content.
Select your segment's personalization point and click Next.
In the Location panel, set your target.
To target the current page, use Page URL or Page Type.
To target every page, use URL Address with a wildcard (for example, https://example.com/*).
In the Display Method section, select Content Zone Handler and select the content zone that you added while configuring the sitemap.
Publish the experience on the site. See Publish a Personalization Experience.
