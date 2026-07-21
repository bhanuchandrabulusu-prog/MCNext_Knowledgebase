# Agentforce Marketing: Mastering Reusability in MC Next to Build Once and Deploy Everywhere

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-mastering-reusability-in-mc-next-to-build-once-and-deploy-everywhere

---

Agentforce Marketing in MC Next allows users to create reusable components, like Expressions and Content Blocks, so that complex logic and brand assets can be built once and deployed across all channels instantly.

In this article we’ll mainly focus on the Email channel, but most of the features we’ll describe can also be used in SMS, WhatsApp and Landing Pages.

Reusability is the secret sauce of MC Next, which Agentic Marketers leverage to:

- **Save Time**: Eliminate manual builds by deploying Saved Expressions and Content Blocks across every campaign in seconds.
- **Ensure Consistency**: Maintain a single “source of truth” for brand assets and logic, ensuring a unified customer experience across all MC Next touchpoints.
- **Streamline Maintenance**: Update a single Saved Variation or component to instantly propagate changes across your entire marketing ecosystem.
- **Lower Error Risks**: Replace risky copy-pasting with pre-vetted, reusable modules that guarantee technical accuracy and data integrity every time.

In this article, we’ll describe the main features and tools that Marketing Cloud Next makes available to achieve reusability.

[![Agentforce Marketing - Create Once, Deploy Everywhere](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-15.05.24-1024x694.png)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-15.05.24.png) 

Agentforce Marketing - Create Once, Deploy Everywhere

## Create Merge Fields templates as «Expressions»

An Expression, or Saved Expression, in Marketing Cloud Next is just **a template for a Merge Field**. You create an expression so that you don’t have to recreate the same Merge Field from scratch in every email, and others from the team can also benefit from it.

### How to create an Expression

Expressions are created from the CMS.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-10.53.43-scaled.png) 

Creating a new Expression from MC Next CMS

Once the Expression is created, you need to define the following elements:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-11.08.44-scaled.png) 

Defining the Expression

1. **Title**: This will be the Expression name in the CMS
2. **Description**: Not mandatory, but a good practice is to describe its purpose and when to use this Expression
3. **Data Source**: This is the Data Graph, the default one is used. The following criterias are coming from it
4. **Attribute**: This is what will be displayed in the Asset. It can simply be an Attribute of the Unified Individual DMO, or any Attribute in a related DMO.
5. **Sort By**: Even though the selected Attribute can be tied to mutilple records (like Boat reservations in this example), you can only have one record’s attribute displayed, so you need to sort them (use [Repeaters](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/repeaters/) to display them all).
6. **Where**: We don’t want every Boat reservations for this Unified Individual, only a specific Brand, so we add Filters
7. **Ressources**: You can add more DMOs from the Data Graph for cross personalization.

Then you Save and Publish the Expression.

### (Re)use an Expression

Now that our Expression is created and published, we can use it in one or more emails, by adding a Merge Field (using the {} in the toolbar) and selecting Saved Expression (you may need to scroll to see the option).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-11.42.02-scaled.png) 

Adding a Saved Expression to an Email

Then you select your Expression from the List (search for its name if you have many).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-11.45.05-scaled.png) 

The definition of the Merge Field is cloned from the Expression

This is what makes Expressions handy, they are Merge Fields templates, which means that when using them to create your Merge Field you have a starting point, created for you by cloning the Expression criteria, and you can then use them as-is or adapt them to your needs (in that latter case, the Expression itself won’t be changed, it is just a starting point). Next.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-11.49.34-scaled.png) 

The Merge Field is ready to be inserted

Define a Default Value in case the criteria return no value for a given recipient, and an API name (which will be visible in the Email canvas). It is a good practice to use the Preview feature of an Email to see how it renders for different recipients.

## Define a section once, reuse it in multiple emails with «Content Blocks»

In Marketing Cloud Next, the Email Builder you can use predefined Components, like Paragraph, Button or Section. With Content Blocks, you can create a section made of standard components and use it in multiple emails. By changing the Content Block in one place, then every Email that include it can benefit from that centralised modification. Think Header or Footer for example.

### How to create a Content Block

You can create a Content Block from the CMS (not from an Email, as there is no “Save as Content Block” yet).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-12.26.48-scaled.png) 

Creating a Content Block Email in MC Next CMS

Once created, you give the Content Block a name (use the pencil icon) and create your reusable section.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-12.41.16-scaled.png) 

Building the Content Block (Footer example)

You can use every standard component on the left in your Content Block (including Expressions). You cannot nest an existing Content Block into another Content Block, and Repeaters are not available. The Variations (Dynamic Content we will explore in the next section) are not available in a Content Block (but you can create several Content Blocks and use them as Variations in an Email). If you use a Brand (you’ll discuss Brands later in this article) to style a Content Block, and the Email that uses this Content Block also has a Brand defined, the Email Brand has precedence.

Once done, Save and Publish your Content Block, which is now ready to be embedded.

### (Re)use a Content Block

From an Email, you drag the Content Block component from the left sidebar, in the Layout section, into the canvas of the Email Builder.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-12.54.56-scaled.png) 

Inserting a Content Block in an Email in MC Next

As a Content Block is essentially a Section, you cannot drop it in an existing Section (as Sections cannot be nested), so you need to drag it above, below or between the existing Sections. Then you select the Content Block you want to use, from the list of published ones.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-13.08.03-scaled.png) 

A Content Block embedded in an Email

You can define Variations, as we already stated above, but when inserted, if you want to edit the Content Block, you need to do it by opening it from the CMS and make changes.

If you want a Flow (Segment Triggered Flow or Form Triggered Flows for example) to use the latest version of the Email, you need to publish the Email (the Flow does not need be paused and there is no need for a new Flow version). So whenever you make changes in a Content Block embedded in an email, you need to:

- Publish the Content Block
- Publish the Email (even though the only changes are from the Content Block)

Since Spring ’26, you can also use the Convert to Section featute, which unlinks the Content Block, so that its elements are copied into the Email as new Components that you can then edit, without further reference to the original Content Block.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-19-at-13.21.35-scaled.png) 

Creating a local version of a Content Block

Once converted to a section, the changes you make locally leave the original Content Block unedited.

## «Dynamic Content»: Reusing Decision Logic for Consistent Personalization

In Marketing Cloud Next’s Email Builder, every standard Components (with the only exception of repeaters), plus the Subject Line and Pre-header, can **render differently depending on the recipient’s informations. This is called Dynamic Content**. For example, depending on the value of a Calculated Insight, you may render different buttons.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20450%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Dynamic-Content-in-MC-Next-Personalization-Concepts-2.png) 

Personalization Concepts of Dynamic Content in MC Next Emails.

Before we create a Dynamic Content and see how to use/re-use some part of it, let’s explain the terms on the diagram above. At Send time, for a given recipient, the **Targeting Rules** (Data Graph based rules) are evaluated. The Rule that the recipient qualifies for is selected, and the associated **Variation**, a unique Content Version, is used in the sent email. A Variation and its related Targeting Rule is called a **Personalization Decision**. A **Personalisation Point** is tied to a specific Email (and one or more Component) and is related to its Personalization Decisions.

The Personalizations Points and Personalization Decisions are stored in Data Cloud (installed when deploying Personalization Foundational data) and are part of Salesforce Personalization, but can only be created, edited or deleted from the Email Builder.

### How to create a Dynamic Content

Let’s create a Dynamic Content, we’ll use a Button as an example, with a different link and label depending on the CLTV ([Customer Life Time Value](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/calculated-insight-guide-customer-life-time-value/), a Calculated Insight store in the Data Graph). First we create a Button.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.03.31-scaled.png) 

Adding the Component to canvas

Then, on the right sidebar, we’ll click the “+ New Variation” button

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.07.24-scaled.png) 

Creating the first Variation

Then we click the blue “New Variation” button. We’ll be able to create the first Personalization Decision and Variation, and to define the related Targeting Rule (CLTV>$4500 for Middle CLTV customers in our example, but this can be any combinaison of criteria from the Data Graph).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.13.50-scaled.png) 

Defining the first Targeting Rule

Save. We just created a Personalisation Point, associated with our Button. It contains a default Variation (used when a recipient does not match any Targeting Rule) and a middle CLTV Variation. By default, the Content of the new Variation is the copied from the default Variation.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.19.15-scaled.png) 

Default and first Variation (selected after creation)

With the Middle CLTV Variation selected, we edit the button to taylor it for the intended audience.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.23.20-scaled.png)

Then, we can create a second new Variation (we’ll thus have 3 Variations including the Default One). For this, we open the dropdown by clicking the Variation’s name.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.27.05-scaled.png)

+ New Variation

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.30.35-scaled.png) 

Defining the new Targeting Rule for the new Variation

We select customers with a CLTV higher than $10,000 in our example. Save. Again, the new Variation is selected and its content is copied from the default Variation, that we can adjust to our VIP audience.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.39.55-scaled.png) 

The second new Variation welcomes the VIPs

Our button has now a default Variation and 2 Rule-based Variations. We can preview and edit each Variation by selecting its name in the dropdown. This allows us to change the settings of the Button for a given Variation (color, text, etc.) and the Targeting Rule.

Finally, we need to ensure that our Targeting Rules are evaluated in the correct order, and we’ll change the default name of the Personalization Point. For this, we click the “Edit Property” item in the dropdown.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-01.52.18-scaled.png) 

Editing the Properties of a Personalization Point

We changed the name of this Personalisation Point to something explicit (Club Personalization in our example), and check that the Targeting Rule Priority is correct (we could reorder the rules from there if needed).

Now is a perfect time to use the Preview feature to ensure the Button displays the correct Variation by testing the rendering for some recipients.

### (Re)use a Personalisation point

A single email can have up to 25 Personalization Points and each component can have 15 variations. **Within an Email, a Personalization Point can be reused**, so that one or more component can benefit from the already defined Targeting Rules.

Let’s reuse our Personalization Point to create Variations of the Subject Line (but any Component except a Repeater can be used, even a Content Block). First, we define its default value, and start the process starts as previously, by clicking “+New Variation”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-02.16.06-scaled.png) 

Reusing a previous Personalization Point

We see our previous Personalization Point (with the name we gave it, and its associated Personalization Decisions). We Select it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-02.19.43-scaled.png) 

Reusing a Personalization Point by linking it to the current Component

We’ll keep the first option, linking the existing Personalisation Point to our current component, the Subject Line. This is a best practice, since we then still have only one, common Personalization Point, so, if we want to change it we just change it once for all linked Components. Also, as we have 25 Personalisation Points per email, using the linking option instead of the cloning one, counts for one only. Save.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-02.32.00-scaled.png) 

The Component is linked with the existing Personalization Point

Once done, our Subject Line has now a default Variation, and 2 new ones, that were created by copying the default Variation. We can now modify the Middle CLTV Variation and the High CLTV Variation of our Subject Line. Once finished the Preview will display a specific Button and Subject line to High CLTV customers, and another specific Button and Subject line for middle CLTV Customers. Other Customers will see the default Subject Line and Button. Note: in the canvas of the Email Builder, even thought the two Components are linked to the same Personalisation Point, changing the Variation on one Component does not change it on the other Component, so you could have a the Middle CLTV Variation of the Subject Line displayed and the High CLTV Variation of the Button. This is not a possible situation for a real Customer, and so previewing the Email is always a good option.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-02.56.10-scaled.png) 

Different Variations displayed in the canvas for 2 Components linked to the same Personalization Point

In a given Email, we can unlink a previously attached Personalization Point. In that case, everything is like the cloning option was initially selected. **We can also reuse a Personalization Point from another email**, but in that case, only the cloning option is possible, as a  Personalization Point is tied to a given email. This creates an identical Personalization Point, by cloning its Targeting Rules.

## Reusable Visual Identity with MC Next «Brands»

In Marketing Cloud Next’s CMS, you can create one or more **Brand: a style Container** that can be applied to several asset type, including the Emails.

### How to create a Brand

Brands are stored in the CMS, so you can create one from there.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-11.49.21-scaled.png) 

Creating a Brand from the CMS in MC Next

Once created, you give it a name, select a tone, and define the colors, typography, button types, margin and paddings and borders. On the right side of the Brand editor, you see the visual result of your changes. Once you’re satisfied, Save it.

### (Re)Use a Brand

You can define a default Brand for your CMS, so that it is applied by default to every new Email (see recipe #4 in [Unlocking your CMS](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/unlock-cms-workspaces/)), either created from the CMS, buy the Campaing Creation Agent or by the Flow templates in a Campaign. You can change, define or remove the Brand used in an Email anytime.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-11.59.29-scaled.png) 

Changing or removing the current Brand of an Email's Brand

When a Brand is applied, every Component is applied the default set of styles of the Brand, and you can switch to another set of style (a set of styles defines the typography, color, spacings, etc.).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-12.06.46-scaled.png) 

A brand defines 3 set of styles for a Button

For example, a Button as three predefined set of styles (Primary, Secondary, Tertiary), and a Heading component has 7 set of styles. Even though a Component is applied a set of styles defined in the Brand, you can style unlink a property from the Brand, to define a custome look and feel. This can be done using the custom set of styles (inheriting the defaults properties of the Brand) or directly from a predefined set of styles.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-12.16.23-scaled.png) 

Unlinking the property of a predefined set of styles

In the example below, the heading is applied a predefined set of styles, but for this specific heading, the color is redefined, the other ones are unchangesd (chain sign).

On property of an Email that can’t be defined in a Brand is the overall background of an image. That’s one of the reason an Email Template comes handy.

## «Email Templates»: The Modular Foundation of Reusability in Marketing Cloud Next

**Email Templates are starting points**, with predefined components and Brand already defined.

### How to create an Email Template

You create an Email Template from the CMS, as it where they are stored.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-12.30.46-scaled.png) 

A new Email Template in MC Next

You can create an Email Template from scratch (Use Components) of from another Email Template (Select a Template). You cannt create an email template with HTML code from another platform, but this option is available whe creating a regular Email (or converting one). The default Brand is applied by default and you can opt in to block style editing in the Emails created out of that Email Template.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-12.35.32-scaled.png) 

Locking the Email Template style or not

You can also prevent the content of a given component to be edited in an Email created out of that Email Template.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-13.11.44-scaled.png) 

Locking a zone, so that its content is defined in the Email Template and cannot be changed

Note that Variations, that we discussed previously in this article are not available in Email Templates.

### (Re)use an Email Template

Once you have created and published your Email Template (and you can create multiple ones), you can pick it in the CMS as a starting point for a new Email. This is true for Emails created from the CMS, Emails generated using the Campaing Creation Agent of by the Flow templates in a Campaign use an internal template that cannot be edited.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-13.19.08-scaled.png) 

Creating an Email from a published Email Template

Since Spring ’26, Agentforce Marketing makes a gallery of Email Templates available. To find an Email Template that we created, we switch to Custom Templates.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-13.20.33-scaled.png) 

Accessing a published Email Template

Once we have selected the Email Template, the Email is created by copying the components and styles of the Email Template. The changes we can make on the new Email depend on the Email Template options to block the style edition globally or not, and to lock or not a component for content editing. The Email Template is a starting point, which means that if we change and publish it after it was used for in an Email, the content changes won’t be reflected in the new Email. We can also change the Email Template used, using the Template Switcher (note that all edits made to the email content will be erased).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/02/Screenshot-2026-02-20-at-13.29.17-scaled.png) 

Select a different Email Template in an Email

## Final Thoughts on Reusability in Agentforce Marketing

We explored the different techniques, as it pertains to Email creation, to streamline your process, by creating a feature once and reusing it everywhere.

The real value comes when you mix this different technique, for example by embedding a Content Block in an Email Template, or using an Expression in Subject Line.
