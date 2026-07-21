# Marketing Cloud Next: Dynamic images in Email, 2 ways that work

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/email-dynamic-images

---

In a previous article about [Repeaters for Emails](/marketing-cloud-next-deep-dives/repeaters/) in Marketing Cloud Growth and Advanced, we took the example of a boat rental company, sending an email listing previous reservations.

The reservations are part of the Data Graph and they contain the image URL to display for each reservation record.

In this article, we will focus on sending an email, presenting the current reservation model. This is what we are trying to achieve (we’ll focus on displaying the dynamic image, not on the body copy here):

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.35.43-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.35.43-scaled.png) 

An email presenting the specific rented boat model

## Method #1 – Using the default Image Component

So, the first step, once the Email is created, is to add an Image Component into the canvas. You can drag it from the left sidebar, under Media or click the + sign in the canvas.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.41.35-scaled.png) 

Adding the image component to the canvas

Once the email is in the canvas, we are presented, on the right sidebar, in the *Select Image Source* section, the option to add an image from the CMS (a static one), or using a *Merge Field*. It is this latter option we will choose, since the image URL is stored as field in our Data Graph.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.46.20-scaled.png) 

Selecting the Merge Field option to insert a Dynamic Image

So, we click the *Add Merge Field* option, and navigate through our Data Graph, to reach our Image URL.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.51.30-scaled.png) 

Searching for our Image URL in the Data Graph

But, no luck, it is not presented, even though actually in the Data Graph (Boat Thumbnail):

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-16.55.06-scaled.png) 

Data Graph, an image URL is there

So, why can’t we add it as Merge Field in the image Component? Well, the answer to this is that the URL format is not supported, **it needs to be a text field**. In Salesforce, our field for storing the images in a reservation is an URL type, when creating the DSO we just used the defaults.

So, to solve this, we’ll create a new Formula field in our DSO, basically a copy of the URL, but with the Text Format. In our example, we call it Boat Preview, and declare it that way:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.03.57-scaled.png) 

Our image URL copied as text Formula Field

Once done, we need to:

1. Map that text Field to a new Field in our DMO (same type)
2. Add the Field in the Data Graph, by editing it
3. Force the evaluation of new the Formula Field (the simplest is to mass update the reservations and manually trigger a refresh of the DSO)
4. Force the refresh of our Data Graph

We then have this is for a specific reservation record:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.14.33-scaled.png) 

A text field is added to our Data Graph, containing the address of our image

In case you wonder, this images are stored in the CMS, and their addresses stored in Salesforce are obtained by following the [6th recipe of our CMS optimisations](/marketing-cloud-next-deep-dives/unlock-cms-workspaces/) article.

Also, if your record is the DMO, but not in the Data Graph, this is probably due to the fact that Engagement DMOs records older than 30 days are ignored by the Data Graph.

Then we can go back to our Email Editor, and now see with the text Fields, which we will use.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.33.45-scaled.png) 

Boat preview is available in the Data Graph

So let’s insert it. Depending on wether there can have multiple records of reservations, you need to select which record to display (or use Repeaters in the exact same way);

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.42.06-scaled.png) 

Adding the text Merge Field as the source of the image

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.44.17-scaled.png) 

Accepting the default API name (\_4 as our 4th attempt here)

We are all set, now, to Preview our work. Do not forget to Save the Email before previewing it, otherwise the Merge Field disappears. Et voilà 😎

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.47.27-scaled.png) 

Our image for a given reservation

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-17.59.00-scaled.png) 

Another reservation from another Contact, yes, this is Dynamic

## Method #2 – Using an HTML component

In this method, we don’t drag an Image Component into the canvas, but an HTML component, in which we will add the Dynamic Image. This gives you the complete control on how you want the image to look.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.02.28-scaled.png) 

Adding a default HTML component to the canvas

Our goal is to replace the empty string with the Merge Field. There is a Add Merge Field button below the component, you may need to scroll the right sidebar to display it. Then, we will enter the following code (adjust to your needs) in the HTML component:  
  
**<img src=”” width=”100%” />**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.07.23-scaled.png)

The steps are exactly the same as the one described in the first method. But, doing so the HTML complains that the src attribute should contain a value starting with “https://”. Obviously, this is made for static image. Hopefully, it also supports Dynamic URLs, but we’ll need to do some extra work.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.17.49-scaled.png) 

The HTML component complaining the src attribute is not compliant

First, let’s make the component happy by adding the correct scheme at the beginning of the src attribute.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.22.22-scaled.png)

But, doing so, the image would not display, as the URL would actually be malformed (starting with two “https://” schemes).

To tackle this, we’ll simply edit the definition of our text Formula field (or create a new one) by using the following Formula:

```
				
					REPLACE(sourceField['Boat_Thumbnail__c'], 'https://', '')
				
			
```

We can ensure this works as intended with the Test Button of the Formula Fields (enter a value, click test and see the result in the Output section).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.30.37-scaled.png) 

The scheme is removed from the URL

We then to go through the exact same steps as the ones from the first method to refresh our Data Graph, so now the URL has the correct formatting to be handled by the HTML component.

Once done, we don’t forget to save our work before previewing the email for a given reservation. It works too 😎

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/Screenshot-2025-08-29-at-18.55.23-scaled.png) 

Dynamic Image inserted via the HTML component
