# Using Segmentation with Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_segments_using.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Using Segmentation with Salesforce Personalization

Segmentation breaks down your data into segments to help you understand, target, and analyze your website and app users. You can create different types of segments to work with Salesforce Personalization. 

When creating segments for use with Personalization, keep these considerations in mind.

You can configure standard segments or real-time segments. The type of segment that you create and apply to a data graph depends on the data that you’re using the segment for. For example, here are two kinds of segments.
Real-time segment on product engagement—Create a real-time segment based on product engagement, where website visitors who view certain products are added to the segment and evaluated in real time to provide personalized content.
Batch segment on product affinity—Create a standard segment based on product style or color affinity.
When creating a segment, use the same data space and data graph that you created for use with Personalization.
To make a real-time segment available in your data graph, add the segment ID and timestamp fields from the segment membership DMO to your real-time profile data graph.
Real-time segmentation doesn’t run if an Account object and an Individual object are included in the same source data graph.
SEE ALSO
Salesforce Help: Create and Activate Segments
Using Data Graphs With Personalization
