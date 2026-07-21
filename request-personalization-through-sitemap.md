# Request Personalization Through the Sitemap | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/request-personalization-through-sitemap.html

---

The Personalization property of the SalesforceInteractions object enables you to interact with the Decisioning API and request for one or more personalizations for personalization points on your Sitemap.

To fetch personalized data, call the fetch method on the Personalization property. The fetch method accepts an array of personalization point names as parameters.

If you have more than one data space, you must define a data space you’d like to use in the fetch method within the SalesforceInteractions.init function, as shown in the following example. If you don’t define a data space, the fetch method uses the default dataspace.

In the following example, we request personalizations for the home_hero and home_recommendations personalization points.

The fetch method returns a Promise. After the Promise is resolved, the arrow function (personalizationResponse) => { ... } is executed. Within the arrow function, you can implement your own custom logic to render the fetched personalized data on your website. In the preceding example, the code simply logs the personalizationResponse object to the console using console.log().

The personalizationResponse object in the preceding example represents the response received from the Decisioning API. For successful personalizations, the response object contains personalized data for the personalization points specified in the request.

The following is an example of personalized data received from the Decisioning API.
