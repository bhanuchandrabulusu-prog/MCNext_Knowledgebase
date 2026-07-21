# Clean URLs in Marketing Cloud Next Landing Pages: Dealing with the Random Suffix

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/landing-page-url-suffix

---

## An extra string at the end of the URL?

Marketing Cloud Next (Growth & Advanced) Landing Pages can be created directly from CMS ([want to optimise how you use your CMS?](/marketing-cloud-next-deep-dives/unlock-cms-workspaces/)) or from a Campaign by creating a Sign up type Flow. However, by default, a hash string will added at the end end of the URL. This string is actually the Content Key of the Landing Page in the CMS.

By itself, it won’t hurt your SEO, but it is always nice to be in complete control of your slugs and URL, so here is way to get rid it.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-12.12.18-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-12.12.18-scaled.png) 

A hash is appended by default at the end of the Landing Page URL

## So, how to remove it?

The Trick here is that you can remove the string, but only **before the Landing Page is published for the firs time**. Once published, it is not possible to remove it.

Outside the Landing Page editor, from the main page, go to the *URL Tab*, and click the pencil next to *URL Alias*. A popup window opens, where the URL alias can be edited.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-12.53.11-scaled.png) 

Editing the URL Alias to get rid of the string.

There you have it, you can remove the string, adjust the URL Alias to whatever slug you wish. We recommend doing this right after the creation of the page, to ensure you made the changes prio to publishing it.

You may have noticed the *URL Redirect* field. This is a handy way, in case you deactivate your page, that your audience does not face a 404 error, but rather sees the page you declare there.

Finally, in the Builder, there is an *URL* section, in the right sidebar, under the *Details* section. You can input a slug there, however, this setting does not seem to be taken into account by Marketing Cloud Next (Growth and Advanced) when generating the actual Landing Page URL.
