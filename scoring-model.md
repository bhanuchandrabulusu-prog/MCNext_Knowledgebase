# Scoring model in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/scoring-model

---

On most Marketing Automation Platforms, *Scoring* is a metric calculated for every Prospects, based on their interactions with your Brand. Generally, each interaction is given a number (ex. Link Click in an Email: +3) and the platform then sums every interactions, multiplied by the number of time they occured in the Prospect lifetime or in a given time window.

This is no different in Marketing Cloud Growth & Advanced, except Engagement Data is not directly stored in the Marketing Automation platform, but in Salesforce DataCloud, **and that is a game-changer**.

If you need the lifecycle context before tuning scores, see [Lifecycle Walkthrough](/marketing-cloud-next-deep-dives/lifecycle-walkthrough/).

## Engagement Model

First, we need to understand how Engagement data is injected from Marketing Cloud Growth & Advanced to Data Cloud.

### Email Engagement

Whenever you are sending an Email, contained links are rewritten so that when a Prospect clicks on it, an intermediary call is made to the platform which gets and stores the information, and then redirects to the original target. Email Opens rely on the same principle, a white pixel image is inserted, whose url is called once opening the Email, the platform getting and storing the Open information.

In Marketing Cloud Growth & Advanced, those interactions are sent to Data Cloud, in a DLO object *(MessagingEventsEmail-EmailEngagement)* which is mapped to the *Email Engagement DMO* related to the *Individuals* the Email was sent to. *Individual Email Clicks, Opens and Unsubscribe* are Stored.

### Website Engagement

In Marketing Cloud Growth & Advanced, Landing Pages and Forms are stored in an under-the-hood Experience Cloud Site, which is Connected to Data Cloud, and handles the Consent Banner.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-9-1024x128.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-9.png) 

Marketing Cloud Growth & Advanced default Consent Banner. One can create Custom Banners.

Once a visitor accepts to be tracked by the use of Cookies, a unique Id is created and stored in a browser’s cookie. This Id will be used by Marketing Cloud Growth & Advanced to identify the interactions with your Landing Pages.

More specifically, the Experience Cloud Connector, writes in a *Behavioral Events DLO* mapped to *Website Engagement DMO*.

Two other DLO are used by the Experience Cloud Connector one mapped with the *Contact Point Email DMO* and the other one mapped to the *Individual DMO*. This ties Email Adresses, Individual and Website interactions together. *Form Submission, Page View and Link Clicks* are stored.

## Marketing Cloud Growth & Advanced Scoring Model

So, we have Individual Email interactions stored in *Email Engagement DMO*and Website Interactions stored in *Website Engagement DMO.*

The *Identity Resolution* process creates a Unified Profile, based on your *Match and Reconciliation Rules*.

Every *Unified Individual* is tied to its composing *Individuals* (via a Bridge unmapped DMO, “Link”), and so it is possible either for an *Individual* or for a *Unified Individual* to get Engagement Data.

### Out of the Box Scoring

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-10.png) 

Marketing Cloud Growth & Advanced default Scoring

Marketing Cloud Growth & Advanced handles the Scoring on a Unified -Individual basis. A default Scoring is implemented, based on the definitions above, which can be seen from *Setup > Marketing Cloud > Scoring Setup* (TIP : from the general blue gear, not from the Marketing Cloud orange gear).

Those informations are used in a *Calculated Insight*, whose 😱 scary definition is given below, as the SQL definition of a Calculated Insight.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-11.png) 

SQL definition of a Unified Individual Engagement

Basically, this is the sum of Interactions stored in the *Engagement DLOs* listed above, from which Engagement data is fetched for every Individual and weight.

Data Cloud and Marketing Cloud Growth & Advanced offer a Lightning Component *Data Cloud Profile Insight*, which can be deployed on Leads and Contacts, displaying the default Score.

### Use the score as Segmentation criteria

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-12.png) 

Marketing Cloud Growth & Advanced: Score as a Calculated Insight.

Activities, including Engagement Data, but also *Flow* the Individual ran into can also be easily displayed using the Component *Data Cloud Profile Engagement*:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-13.png) 

Unified Individual Engagement and Flow Data. Filters are very handy.

### Display on Leads & Contacts Layout

As basic Calculated Insights, the score in made available directly as a direct Relation, under the Unified Individual it is tied to. [2 Methods to list your Segment members](/marketing-cloud-next-deep-dives/list-your-segment-members/)

### 😎 How cool is that?

Well, **you can create your own Calculated Insights** (you can even clone the out-of-the-box one) and display it on Leads and Contact.

For example, you can only take recent Engagements, say 3 months ago max, and display it along with the overall Score:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/scoring-model-14.png) 

Extending the Standard Scoring Model with a Custom Model

We could also imagine to have an Email-only Engagement Score or Web-only Engagement Score. One could also filter on certain pages, mimicking what is called *Category Score* in Pardot.

**And, as this is done in the Data Cloud era, every data is available at you finger tips**, so you can also add Opportunities in the mix for instance.

Possibilities are endless.
