# Agentforce Marketing: Einstein Decision (Einstein Engagement Frequency and Einstein Engagement Scoring)

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-einstein-decision-engagement-frequency-scoring

---

In Agentforce Marketing, you can use **Einstein Decision** in Segment Trigerred Flows, to guide each person in the flow toward a specific path, depending on their individual email engagement history. For example, you can send highly likely email openers down one path, and people whose email channel is saturated down another. **Einstein Decision relies on Einstein Engagement Frequency and Einstein Engagement Scoring**. Those features are only available in Marketing Cloud Advanced Edition, not in Growth Edition.

## Einstein Decision Setup

### Activate Einstein Engagement Frequency

From Setup, go to Einstein > Einstein for Marketing > Einstein Engagement Frequency

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-10.26.31-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-10.26.31-scaled.png) 

Einstein Engagement Frequency Setup page

Click Enable: the feature is activated when the Status changes to a green Enabled. Note that it may take 90 days before actual insights are available. Also, at l**east 10 subscribers are required, each being sent at least 5 email since 28 days**. Eintein Engagement Frequency can be disabled, in which case the generated insights are kept but no longer updated.

Einstein Engagement Frequency stores its insights in a dedicated DMO, called **Email Engagement Frequency.**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-11.41.12-scaled.png) 

Email Engagement Frequency DMO with insights

That DMO is created during the initial Setup, and Enabling the feature, as we just did, maps it to a DSO/DLO Einstein writes into, and **creates a relationship with the Contact Point Email DMO**. In this article we focus on Einstein Decision in Segment Triggered Flows, but Einstein Engagement Frequency insights can  **be used in Segmentation** for example, since they are now linked to the Data Model.

### Activate Einstein Engagement Scoring

The procedure is identical as above: Setup > Einstein > Einstein for Marketing > Einstein Engagement Scoring Enable.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-12.29.00-scaled.png) 

Einstein Engagement Scoring is enabled

Allow 90 days for insights to be generated, which will be stored inside the Email Engagement Score DMO. For an in-depth view of how the scores are calculated, see the associated [Model Card](https://help.salesforce.com/s/articleView?id=mktg.mktg_einstein_model_card_ees.htm&type=5).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-13.49.33-scaled.png) 

Email Engagement Score DMO insights

### Adding Frequency and Scoring to the Data Graph

So far, If you create a Segment Triggered Flow and add an Einstein Decision in the Flow, and select Scoring or Frequency you’ll see a message telling you that the feature needs to be activated (ex. for Scoring *“Maximize customer engagement with Einstein Engagement Scoring in Salesforce Flow. Ask your Salesforce admin to enable it today.”)*, even though we activated it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-14.26.04-scaled.png) 

The Einstein Decision Split needs a compliant Data Graph

To finish the Setup, we just need to **add the Email Engagement Score and Email Engagement Frequency to the default Data Graph**. You can have any other DMO in our Data Graph (the one declared as Marketing  Cloud Next’s default or the one you select when you create a Flow directly) but you need at least those two DMOs for Einstein Decision to Work. Those two DMOs are related to the Contact Point Email DMO, which is related to the Individual DMO, which, thanks to the Unified Link Individual DMO (a junction object), is related to the Individual DMO. **So, in the Data Graph, we add the Unified Link Individual DMO to the root Unified Individual DMO, then add the Contact Point Email DMO and finally the Email Engagement Frequency DMO**. We include the following Fields by checking the box next to them:

- Email Classification
- Email Frequency
- along with the insight created date

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-14.45.53-scaled.png) 

Adding the Email Engagement Frequency DMO to the Data Graph

Then, we also add the **Email Engagement Score DMO to the Email Contact Point DMO** in the Data Graph, and select its following Fields:

- Email Click Likelihood
- Email Click Score
- Email Engagement Persona
- Email Open Likelihood
- Email Open Score
- Email Subscribe Likelihood
- Email Subscribe Score
- along with the insight created date

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-14.53.19-scaled.png) 

Adding the Email Engagement Frequency DMO with its related Fields

We can now **Save (and Build)** the Data Graph, and **schedule its refresh** rate so we have regular data updates and up to date Einstein insights.

**The Setup of Einstein Engagement Frequency, Einstein Engagement Score and Einstein Decision is not completed.**

## Using Einstein Decison

In a Segment Triggered Flow, add the Einstein Decision Element.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-15.02.44-scaled.png) 

Adding the Einstein Decision Element to a Segment Triggered Flow

You now need to select which Einstein **Decision Model** you want, by selecting **either Scoring or Frequency**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-15.15.30-scaled.png) 

Select the Einstein Decision Model

### Einstein Decision and Einstein Engagement Frequency

By selecting the Frequency Model, as above, 5 Paths are automatically created.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-16.01.12-scaled.png) 

The 5 Paths created by a Frequency Model

**Every person in the Flow hitting this activity will automatically be directed to the correct Path**, as calculated by Einstein out of the actual engagement Data of that Person. Here is the meaning of each Path:

- **Saturated**: Received too many messages.
- **AlmostSaturated**: Received nearly too many messages.
- **OnTarget:** Received the right amount of messages.
- **Undersaturated**: Received too few messages.
- **Default**: used when the frequency has not been evaluated yet (too few data) or no other Path matches the current Person

**In each Path, you can add an entire experience or a single element**, entirely up to you. For example, you may send two emails in the Understarurated Path separated with a Wait for Amount of Time Element and in the Saturated Path, you can leverage the multi-channel capabilities of Marketing Cloud Next, and send a WhatsApp message or a SMS message. In the Component setting, there is a **Remove Path** button in case you may want to keep only specific path/s (the fallback being the Default Path which cannot be removed).

### Einstein Decision and Einstein Engagement Scoring

When selecting the Scoring Model, we are presented several options as **Scoring Metrics**, either the decision is based on the **profile** of the current person or on **specific engagement activities**:

- **Persona** (profile based): Select paths based on the customer engagement persona.
- **Likelihood** (Engagement):
  - Open: Select paths based on how likely the customer is to open a message.
  - Click: Select paths based on how likely the customer is to click a link in a message.
  - Subscribe: Select paths based on how likely the customer is to stay subscribed to your list.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-16.27.48-scaled.png) 

Available Scoring Metrics in a Scoring based Einstein Decision

Each Path can be removed (in the Decision right Panel, “Remove Path Button”) if you want to keep only certain Path for the chosen Scoring Metric. The Default Path works as in the Frequency Decision Model above

#### Persona Metrics

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-16.46.19-scaled.png) 

Paths availabe in the Persona Scoring Metric

Here is the meaning of each Path:

- **Loyalists**: Subscribers with high engagement scores.
- **Window Shoppers and Selective Subscribers**: Subscribers with mid-range engagement scores.
- **Winback/Dormant**: Subscribers with low engagement scores.

You can craft entire experiences or add a simple activity in each Path, for example promote your latest product in the Loyalists and share more top of funnel content sequence to the Dormants.

#### Engagement based Metrics

If you choose  Open, Click or Subscribe Likelihood, you will be presented the following Paths.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-27-at-16.52.24-scaled.png) 

The Open, Click Subscribe Paths are the same (Open here)

The default Path is, as ususal, the Path that a person matching no other Path will be guided to. You can create entire experiences or use a single element in each Path. For example, in a Least Likely Open Path, use another Channel and in a Most Likely Click Path promote your latest Product.
