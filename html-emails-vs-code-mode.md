# HTML emails drag & drop VS code mode in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/html-emails-vs-code-mode

---

**Marketing Cloud Next (Growth and Advanced) has a Drag & Drop Email Builder. In the coming release, Summer ’25, you will be able to convert an existing email into HTML or to import an Email built in an external platform into the Builder.**

## Converting an existing Email

Let’s say you created your Email using Marketing Cloud Next (Growth & Advanced) from a Campaign (Single Email Flow). A starting point Email was created and you apply your own brand to it (btw, in case you wonder default images can be changed be replacing the images in the CMS called “Default Email Template Header” and “Default Email Template Logo”). [Unlock your CMS Workspaces in Marketing Cloud Next](/marketing-cloud-next-deep-dives/unlock-cms-workspaces/)

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-A-default-email-with-a-brand-applied-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-A-default-email-with-a-brand-applied.png) 

A default email with a brand applied

If you want to make changes that are not easy to achieve using the predefined components and their styling possibilities (think Custom Font, or Custom Button), then you can convert your Email into HTML so you can make every changes you want. On the top of the page you can switch from Drag & Drop mode and HTML (code mode)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Editor-vs-HTML-Editor.png) 

Editor vs HTML Editor

Once you click on the code mode, you get a read access only to the HTML code, in read only mode (to check for syntax for example).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-HTML-code-in-read-only-mode.png) 

HTML code, in read only mode

Then, if you want to start using the HTML editor and no longer the builder, you silply click the “Convert to HTML” button.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Conversion-of-an-email-into-HTML-mode.png) 

Conversion of an email into HTML mode

Some things to note when converting an Email:

- the conversion cannot be reversed, you can’t use drag-and-drop components or apply styling from the Style tab.
- it also removes dynamic content, including repeaters, conditional logic, and content variants from an email.
- merge fields are still available for personalisation

## Importing HTML from an external Builder

Let’s say you use a external tool to build your Emails. You can then create an empty Email in Marketing Cloud (for example using Add Content from the CMS or creating a Blank Email Flow).

Then you convert the Email as above and just replace the HTML code by yours. You may have to add the Organisation Address and Unsubscribe link using Merge Fields as those are required for Promotional Sends.

## Final Thoughts

Editing HTML Emails is as easy as using the Builder, and I’d recommend to using that latter unless you have no other choice.

The Drag & Drop Builder used by Marketing Cloud Next (Growth & Advanced) is shared with Account Engagement (fka Pardot) and if you use it in Pardot, you get the HTML conversion / import as well in Pardot.

Screenshots in this article were made in a Sandbox in Preview Mode, and hence the feature may change since the actual release of Summer ‘25.
