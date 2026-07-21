# Access Web Personalization Manager

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_wpm_access_web_personalization_manager.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Access Web Personalization Manager

Accessing Web Personalization Manager requires only appending a simple query string to your website URL.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To access Web Personalization Manager	Web Personalization Manager user permission set
NOTE To use Web Personalization Manager on Web SDK enabled websites, Data 360 users need to enable third-party cookies in the browser. For example, see Allow third-party cookies for a specific site.
Access your Web SDK-enabled website page.
Add the string ?sf_personalization_wpm​​ at the end of the URL and press return.
If parameters are already present in the URL, add &sf_personalization_wpm at the end.
NOTE To access Web Personalization Manager in a sandbox environment, add sf_personalization_wpm&sf_personalization_wpm_env=prod_sandbox at the end of the URL.

Example: https://example.com/?sf_personalization_wpm&sf_personalization_wpm_env=prod_sandbox

In the window that opens, enter your Salesforce credentials.
If the log in window doesn't open, disable your browser's popup blocker and click Log In from the resulting prompt.
Create a Bookmarklet
To activate Web Personalization Manager on your website without manually adding the string to the URL each time, you can create a browser bookmarklet in Google Chrome.
SEE ALSO
Create a Bookmarklet
Salesforce Personalization and Data 360 Setup
Developers: Personalize Web Experiences with the Salesforce Interactions SDK
