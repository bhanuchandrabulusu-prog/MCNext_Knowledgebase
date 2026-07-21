# Create a Custom Objective

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_create_custom_objective.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create a Custom Objective

Using specific engagement signals, you can create custom business objectives to use with objective-based recommenders. You can reuse this objective to enhance the customer journey and deliver real-time, personalized recommendations, simplifying setup and boosting customer engagement.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure recommenders:	Change and Edit Recommenders
Complete steps 1 through 8 in Configure an Objective-Based Recommender.
To create a custom objective, select New Objective.
Name the objective and add an optional description.
The API name is auto-generated.
Select a recommender purpose.
PURPOSE	DESCRIPTION
Maximize	This recommender is designed to maximize a specific business goal. When selected, it provides recommendations aimed at enhancing positive business outcomes, such as increasing orders or signups.
Minimize	This recommender is designed to minimize a specific negative business outcome. When selected, it provides recommendations aimed at reducing issues like cart abandonments.
Select an engagement signal metric, and click Next.
NOTE The metrics available for selection are count-based and use an underlying engagement signal that references an engagement object and mapped fields on the selected profile data graph, as well as the root DMO and the field of the recommended item data graph.
Select any other engagement signals that you want to use to train the machine language learning model.
NOTE Only the engagement signals compatible with the selected profile and item data graphs are available for selection. For example, when recommending products, signals like Product Browsing, Add to Cart, or Purchases may be available as these signals can enhance model performance and improve recommendations.
Click Next.
(Optional) Add filters.
You can add filters to a recommender at any time. See Add Recommendation Filters.
Save the recommender.
SEE ALSO
Engagement Signals and Metrics
Salesforce Help: Engagement Signals
