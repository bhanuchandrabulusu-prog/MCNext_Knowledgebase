# Salesforce Personalization and Data 360

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_data_cloud_and_einstein_personalization_learn_about.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Salesforce Personalization and Data 360

To generate and present unique, personalized content experiences, Salesforce Personalization in Marketing Cloud Next uses profile and item data graphs, calculated insights, segments, and real-time behavioral data from Data 360.

User interaction data is ingested from the Data 360 Web SDK. Data is simultaneously ingested into the real-time layer for immediate processing and the standard data layer for regular processing along with other ingested data.
Data 360 identity resolution performs real-time matching to identify a user profile. If the user is unknown, a profile is created.
The known or anonymous profile in the real-time data graph is updated with ingested engagement and profile event data. 
Real-time insights and segments are calculated. The real-time profile data graph is updated with metrics and segmentation results.
When a personalization decision is required, Personalization calls the Data 360 profile API to obtain the updated individual profile from the real-time profile data graph.
SEE ALSO
How Salesforce Personalization Works
Salesforce Help: About Salesforce Data 360
Salesforce Help: Data Graphs
Salesforce Help: Create and Activate Segments
Salesforce Help: Enhance Data with Insights
