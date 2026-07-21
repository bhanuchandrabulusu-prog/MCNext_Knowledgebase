# Configure Flicker Defense | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/configure-flicker-defense.html

---

Page flicker is a visible glitch that occurs when a web page loads or updates content, causing it to flash or change content rapidly. This issue is common in personalization or A/B testing scenarios, where a web page’s original content is displayed momentarily before being replaced with personalized or variant versions of content.

The FlickerDefenseConfig interface helps prevent page flicker caused by rendering personalized content returned by Personalization on web pages.

The FlickerDefenseConfig interface defines the configuration settings for Flicker Defender.

The FlickerDefenseConfig interface includes the properties in this table.

Property	Description	Type	Default Value
redisplayTimeoutMilliseconds	The time (in milliseconds) to wait before redisplaying hidden elements on the page	Number	2000
renderPersonalizationAfterTimeoutElapsed	Determines whether to proceed with or block the rendering of personalized content after the timeout has lapsed	Boolean	false

You can customize Flicker Defense by specifying your own values for redisplayTimeoutMilliseconds and renderPersonalizationAfterTimeoutElapsed, as shown in this example.

The default values provided in the Flicker Defense configuration is sufficient for most use cases. Modify these values only if necessary.
