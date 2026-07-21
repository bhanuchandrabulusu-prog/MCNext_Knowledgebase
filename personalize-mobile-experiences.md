# Personalize Mobile Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/personalize-mobile-experiences.html

---

The Personalization module of the Engagement Mobile SDK enables you to query the Personalization service and receive targeted content within your iOS and Android applications.

While the Personalization module processes these requests to return personalized content, the Data 360 module handles the capture of customer interactions. By integrating both modules, you can send engagement data to Data 360 to build behavior profiles and use that data to drive real-time personalization decisions in your app.

The Personalization module depends on the underlying Data 360 module for identity resolution, consent management, and behavioral data collection. Therefore, integrate your mobile app with the Data 360 module. For procedure, see Data 360 Engagement Mobile SDK.

The Engagement Mobile SDK provides methods to capture interactions and personalize content. Call these methods in your application’s code at the appropriate moments in the user journey to track events and retrieve personalized experiences.
