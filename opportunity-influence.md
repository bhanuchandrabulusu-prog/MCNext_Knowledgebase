# Opportunity Influence in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/opportunity-influence

---

**As a marketer, you create campaigns with the goal of getting your targets to interact with them. The impact of your campaigns is measured through the concepts of influence and attribution. Marketing Cloud Next (Growth & Advanced) offers two attribution models: First Touch and Last Touch.**

## First, disable previous attribution models

Opportunity Influence replaces previous campaign attribution features: Campaign Influence or Customizable Campaign Influence. So, it is required to disable them and a best practice to remove the associated metrics fields from your campaign page layout.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Campaign-Influence-is-disabled-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Campaign-Influence-is-disabled.png) 

Campaign Influence is disabled

## Then, activate Opportunity Influence

Go to *Setup > Marketing Cloud > Assisted Setup > Reporting & Optimisations > Analytics* then at the bottom of the page, choose *Set Up Opportunity Influence.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Marketing-Cloud-Next-Opportunity-Influence-Setup.png) 

Marketing Cloud Next Opportunity Influence Setup

The guided process first checks the required Data Kits are installed and install two new Data Lake Objects, one for each model.

Once those elements installed and the previous attribution models disabled, as stated above, you will be able to activate the new feature.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Opportunity-Influence-is-ready-to-be-activated.png) 

Opportunity Influence is ready to be activated

Once this is done, you need to to turn on the attribution models you are interested in. You recommend you activate both First Touch and Last Touch models.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-There-you-have-it.png) 

There you have it!

## Where do I access the associated data?

It takes around one hour for the data to be available, and then it is updated every hour. Note, Opportunities created less than 30 days ago are taken into account.

The Opportunities influenced by a given Campaign are available on the Campaign Record (under Performance).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Influenced-Opportunities-in-First-Touch-model.png) 

Influenced Opportunities in First Touch model

The *Total Revenue* is displayed: it is the amount of business your Campaign was credited for, in the chosen Attribution Model (Note, if you know the Campaign Cost, then its ROI is defined as: *(Total Revenue — Campaign Cost)/Campaign Cost*.

It is very easy to switch for one model to the other, using the Attribution Model selector.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Influenced-Opportunities-in-Last-Touch-model-for-the-same-campaing.png) 

Influenced Opportunities in Last Touch model for the same campaign

## How does that work?

In Opportunity Influence, Contacts do not need to be Campaign Members of a given Campaign to be related to it. Instead, they need to Engage with that Campaign, by clicking on an Email or SMS link sent from this Campaign (site clicks are not considered).

Contact Roles are still used in Opportunity Influence: this the glue (Junction Object) between an Opportunity and a Contact.

So, for every Close/Won opportunity, Marketing Cloud Next, will:

1. Generate a list of every Contact Role’s clicks (Email or SMS)
2. Keep only Clicks that happened no more than 30 days before the opportunity creation and until it was closed
3. The oldest click is related to a Campaign which is declared the First Touch Campaign and gets credited of the Opportunity Amount in First Touch Mode
4. The most recent click is related to a Campaign which is declared the Last Touch Campaign and gets credited of the Opportunity Amount in Last Touch Mode

In the following diagram, Contact 1 is not a Contact Role of the evaluated Opportunity, so none of this click are considered. Clicks before the Opportunity creation minus 30 days of after the closing are not considered neither, even though related to Contact 2 and Contact 3, actual Contact Roles. The first and last considered click are related respectively to Campaign 2 and Campaign 5.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20450%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-This-Opportunity-will-be-listed-in-Campaign-2-influenced-Opportunities-list-Fir.png) 

This Opportunity will be listed in Campaign 2 influenced Opportunities list (First Touch) and in Campaign 5 list (Last Touch)

Marketing Cloud Next (Growth & Advanced) does the hard work of storing for all Closed/Won Opportunities their First Touch Campaign (in a Data Lake object that was installed in the first steps: OpportunityInfluenceFirstTouch1) and their last touch one (OpportunityInfluenceLastTouch2).

Thos two latter DLOs are mapped to a standardised DMO, called Opportunity Influence and with relationships with Campaigns, Individuals (Unified Individuals are not used as it pertains to Opportunity Influence) and Opportunities.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-First-Touch-Opportunity-Influence-DLO-mappings-to-Opportunity-Influence-DMO.png) 

First Touch Opportunity Influence DLO mappings to Opportunity Influence DMO

## What is the meaning of Attribution Models?

The overall ROI for your Marketing Team is calculated by comparing your Campaign Cost and their Results (sum of close/won opportunities amounts, see above).

What’s important with attribution models is they are just that, models, and one model is not better than another, they just reflect different aspects of your Campaign performance.

When analysing the Campaign Performance in First Touch Attribution Model, we credit all first interaction’s Campaign as if they were responsible on their own for the whole opportunity lifecycle. By doing so, we highlight their performance in an acquisition-focused approach.

Similarly, Last Touch Attribution Model highlights the Campaign performance from a closing point of view.

Comparing the Performance of a Campaign in different attribution models, is what gives insights on what they do best.

As of now, only Last Touch and First Touch are available, but there are a lot of others (M shape, W shape, Even Distribution, etc.), all allowing you to analyse the performance of your campaigns across different functions.

## Final Thoughts

The First touch and Last Touch data are available as a Related List of Influenced Opportunities and total amount, in the Performance item of the Campaign Layout.

But, as this data is stored in a standardised DMO, it can be displayed as a Salesforce Report, as a CRMa Lens that can be embedded in a Dashboard, etc.

You could also create your own Attribution model, for example as a new DLO mapped to the Opportunity Influence DMO, and feed it using a Data Transform.
