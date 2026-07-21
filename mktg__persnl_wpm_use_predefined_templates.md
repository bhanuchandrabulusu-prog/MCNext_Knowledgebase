# Use Experience Templates

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_wpm_use_predefined_templates.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Use Experience Templates

You can use custom experience templates to add your personalized content to the website, or replace existing content with personalized options. Experience templates offer the benefits of reuse and extensive styling flexibility, enabling you to customize a wide range of attributes efficiently. Experience templates also provide faster creation, support for personalization features like product recommendations, and greater stability, especially on complex pages.

To configure customized experience templates for use with Web Personalization Manager, see Experience Templates.

From the Personalization Experiences menu in Web Personalization Manager, select New.
Select Embedded Content, and click Next.
NOTE To learn more about the Web Curation Agent experience or for assistance with setup, contact your account executive.
Select the button next to the personalization point that you want to base the personalization experience on.
Web Personalization Manager displays only personalization points in the data space you've configured in the website's sitemap.
(Optional) To create a new personalization point, click Create Personalization Point.
A window opens enabling you to create and configure a personalization point. After you finish creating the personalization point, you can then return to the selection window to choose it.
Click Next.
Select an experience template and click Next.
From the Location tab in the Editor panel, specify the page option where you want to display the personalized content.
To display the personalization experience on all website pages of the type you’re currently on, select Current Page Type.

For example, selecting this option on a Product Detail Page type duplicates the experience on all product detail pages on the website.

To select pages based on a URL, select Page URL and specify a URL.

Using wildcards, you can apply the personalization to multiple pages. For example, you can use a wildcard for the page name to apply the personalization to all pages in a specific path, such as https://mysite.com/product/*.html.

Under Display Method, select how you want to display the content.
DISPLAY METHOD	ACTION
Replace a Content Zone	To replace the content zone, select a predefined zone from the Content Zone dropdown, and replace it with the content defined in the experience template.
Use Content Zone Handler	To use a content zone handler registered on your website, select the required handler from the Content Zone Handler dropdown.

This option is available only if your website uses a frontend framework and a content handler has been registered for a component. For more information, see Integrate Personalization with Modern Frontend Frameworks.


Replace an Element	To replace an element with personalized content from the experience template, hover over the element that you want to select until it’s highlighted, and click it.
Add Before an Element	To add personalized content from the experience template before a specific element on the web page, hover over the element until it’s highlighted, and click it.
Add ‌After an Element	To add personalized content from the experience template after a specific element on the web page, hover over the element until it’s highlighted, and click it.
Add an Overlay	An overlay is a layer of content that you place on top of existing content to provide contextual recommendations. ‌From the When to Display dropdown, select an option to add an overlying layer of content where you want to add the recommendation defined in the experience template depending on user interaction.
Immediately—Displays an overlay as soon as personalized content is received.
Exit Intent—Displays an overlay when you move the cursor to the top of the screen, indicating an intention to change tabs or close the browser. You can set a delay value to schedule the overlay.
Element Click—Displays an overlay when you click a specific element on the page. Click Select Element, and select a targeted element on the page to specify the element.
Scroll Percentage—Shows an overlay when you scroll the page. You can specify a certain amount of scroll before the overlay appears.
After you select the display method, click Content.
From the Engagement Destination menu, select the type of engagement that you want to track. For more information, see Track Personalization Engagement.
(Optional) Select a different experience template from the Selected Template list.
Click the Preview Settings tab.
PREVIEW OPTION	ACTION
Show Overlays	Enable this option if you want to display highlighted overlays around personalized content when previewing your personalization experience.
Show All Personalization Experiences	Enable this option if you want to preview the current experience along with all the other personalization experiences created on the page.
(Optional) Enter a different Individual ID if you want to preview the personalization experience from the perspective of a different user.
Click Save.
SEE ALSO
Manually Personalize Page Elements
Preview the Experience
