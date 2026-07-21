# Meet Repeaters, your new superpower for Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/repeaters

---

**With the coming release (Summer ’25) Marketing Cloud will give you a new tool: the ability, without writing any code, to display dynamic lists (specific to each recipient) of things in your emails.**

Here is some inspiration. For each recipient, you can now very easily include in your email copy :

- The last 3 solved cases
- The latest products (including thumbnails) bought from you
- Replay links to all the registered but not attended webinars

Possibilities are endless, you just need to add the data (Object and Fields) you want to display in you current Data Graph, and it is available as a Data Source for your Repeater. You can then style it, design the layout of each record, etc.

The best way to demonstrate this new feature is to build a complete Repeater inside an Email as an example. We’ll be writing a loyalty Email for the Ursa Boat Rental Brand. In that Email, we’ll thank our Customers for their Loyalty and display a list of Boats that they’ve been renting this summer.

## Data Model

In Salesforce, we have a Custom Object to store all reservations, including a link to the boat thumbnail and a lookup to the Lead who actually rent the Boat.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Salesforce-Custom-Object-containing-our-reservations-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Salesforce-Custom-Object-containing-our-reservations.png) 

Salesforce Custom Object containing our reservations.

That object is mirrored as a DSO in Data Cloud, and mapped to a DMO. That DMO is related to the Individual Object. Also, we’ve added the Boat Reservation DMO in our default Data Graph (the one defined in Customer Engagement that is used be Emails).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Ursa-Boat-Rental-default-DMO.png) 

Ursa Boat Rental default DMO

We also have a Campaign associated with an Email to Send our loyalty Email and a Segment, of all Unified Individual who rented at least 3 boats during the summer.

## Email Building

### Repeater Source

We’ve prepared an Email, using our predefined brand identity. Unlock your CMS Workspaces in Marketing Cloud Next</marketing-cloud-next-deep-dives/unlock-cms-workspaces/>

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Our-starting-Point.png) 

Our starting Point

You may have noticed on the left sidebar, in the Layout Section a “Repeater” item. Let’s drag it in the canvas, below our first paragraph and above our footer with social links.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-An-empty-Repeater-has-been-added-to-the-copy.png) 

An empty Repeater has been added to the copy

On the right sidebar, we will select where the data we want to repeat as a list comes from. In Repeater Source > +Select > Select Data Graph Attribute > Unified Link Individual > Individual > Boat Reservation.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-The-Repeater-source-is-now-set.png) 

The Repeater source is now set

We could also filter or sort the reservations we want to display (only display premium boats for example is the informations is in the Data Graph).

### Repeater Display

To design what will actually be displayed in the email, we actually design and setup only the first item. All other records will be repeated using the same layout.

*Number of Items to Show* is the way to set the max number of records we will be displaying and *Number of items per Row* is the number of records per line. We set this to 4 boat reservation max and 2 per lines.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-The-layout-reflects-our-display-choices.png) 

The layout reflects our display choices

By default, all items are displayed using the Card layout, which gives you a top image, a heading, a paragraph and a button. We set the value of the elements in the first item.

Repeaters are easy to use, but sometimes navigating in the nested elements is no so easy. This is where the Component Tree in the left sidebar comes handy. Here we select the image inside the Card from it, to configure it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Selecting-the-card-components-in-the-Component-Tree.png) 

Selecting the card components in the Component Tree

We want that image tp be populated for each item by the thumbnail we have in the Data Graph for a Boat Reservation record. So, we select Merge Field > +Add Merge Field instead of Salesforce CMS (otherwise every Card in the Repeater would display the same static image).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Adding-a-dynamic-image-definition.png) 

Adding a dynamic image definition

We select the DMO in the Data Graph (the top entry) and then our field containing the boat preview url.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Setting-in-the-image-to-be-displayed.png) 

Setting in the image to be displayed

Our first card (and other ones) reflect our definition. For this demo, we will also add a heading, and suppress the paragraph and the button (of course we could have kept them and define them with informations for the Data Graph). By clicking on the “Enter Heading” element , we select the Merge Field (using the toolbar and clicking {}) to simply display the reservation name (which is the same as the Boat). We use our Boat Reservation Repeater Data Source and select the give Field.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Adding-the-Boat-Reservation-detail.png) 

Adding the Boat Reservation detail

Then, from the left sidebar, within the Tree Component, we remove the Paragraph and the Button (recycle bin icon).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Removing-unused-elements-from-the-card.png) 

Removing unused elements from the card

We save the email (this is mandatory for the preview). Here is what we have built, a Repeater, displaying for each recipients the thumbnail of the rented boat along with its name. Let’s see how it looks like. Once saved, we click Preview, select a Segment and a Recipient from that Segment and see our work in action!

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-The-email-Captain-Marie-will-get-with-the-Boats-she-rented.png) 

The email Captain Marie will get, with the Boats she rented

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-The-one-David-will-get-with-his-own-rentals.png) 

The one David will get, with his own rentals

Nice and Clean 😎

We’ve started with a Card layout (image, heading, paragraph and button), and you’ll notice that there are 2 other options: “List” or “Custom”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/022-Predefined-layouts-for-Repeaters.png) 

Predefined layouts for Repeaters

“Custom” is an empty Layout, so you create you own from scratch and “List” is a good starting point to display one item per line.

## Final Thoughts

**This feature, plus the HTML mode are really cool features**.

This is very flexible, as long as you can embed it in your Data Graph, you can display it in your Email. You can include multiple Repeaters inside an email.

Data Graph can embed a given number of records for a DMO and these records must be recent.

You could also add recommendations (for instance products a given recipient may like regarding its specific lifecycle). The integration in your emails is the same as what follows, you’ll just need a Trained Recommender (Personalization) and add it a global Data Source.

If you need to handle replies and out-of-office at scale, see [Mastering Reply Mail Management in Marketing Cloud Next](/marketing-cloud-next-deep-dives/replay-mail-management-rmm/).

PS : the sreenshots in this article were taken from a SDO preview org and may differ from what we’ll get when the Summer ’25 is actually rolled out.
