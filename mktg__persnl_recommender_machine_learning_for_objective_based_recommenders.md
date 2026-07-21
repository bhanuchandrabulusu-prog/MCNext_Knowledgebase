# Machine Learning for Objective-Based Recommenders

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_machine_learning_for_objective_based_recommenders.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Machine Learning for Objective-Based Recommenders

The Salesforce Personalization recommendation system uses machine learning and AI to analyze user behavior along with data from profile and item data graphs. The system then predicts user actions that support business goals, such as increasing revenue or reducing unsubscribes. When you understand how the system works, you can provide adequate inputs that influence the learning and lead to better recommendations.

Engagement Signals for Recommendation Training

The selection of engagement signals is crucial, because it determines which user behaviors the system prioritizes during the learning process. For example, to optimize for maximizing add-to-cart actions, engagement signals used for recommendation training might include Product View, Product Click, Add to Cart, and Product Purchased. Engagement signals can be configured based on your engagement sources, which may include Salesforce channels and non-Salesforce channels, depending on the engagement data you feed into Data 360. For more information, see Engagement Signals.

To encourage effective training, your custom objective should, by default, include all engagement signals found within your profile and item data graphs. You should actively exclude only the specific signals you’ve determined are unsuitable for influencing the model's recommendations.

The Learning Feedback Loop

The custom objective-based recommendation system learns by recommending items and observing the rewards it gets. Then, it evaluates the relationships based on whether the recommended items helped achieve the defined business objectives.

Think of it as a continuous feedback loop.

Recommendation:
The system makes a recommendation to a user based on past interactions and the defined objective.
Observation
The system observes what happens after the recommendation. Did the user take an action that contributed to the objective?
Reward
When the recommendation leads to a positive outcome that’s aligned with the objective, the system receives a reward. The value of this reward depends on how significant the outcome is for the business goal.
Learning
The system analyzes the rewards it receives to understand which recommendations were most effective in achieving the business goal. It then updates its algorithms and models to prioritize similar recommendations in the future.
How the System Thinks: From User Journeys to Recommendations

To better understand how to design your event capture and recommenders, it helps to understand how the machine learning model works. The system uses a sophisticated method to predict user actions by analyzing the sequence of their behavior.

A Multi-Step Journey, Not Just a Single Step
The model supports multiple steps to achieve a desired outcome. It analyzes the entire series of signals from a natural customer journey on your website or app. For example, it can trace a path from viewing a category page, to clicking a specific product, to viewing a related accessory, and finally to adding an item to the cart. Both the journey's signals (such as clicks and views) and the outcome (such as a purchase) are expressed as Engagement Signals.
Learning from Collective User Behavior
The model doesn't learn only from a single user's journey in isolation. It learns by analyzing the paths of all users on your website. By looking at collective behavior, it identifies which items have a high probability of being interacted with, given the sequence of actions a user has taken so far. This allows the system to recommend items that are relevant to the user's current journey, based on patterns learned from thousands of similar journeys.
Predicting the Next Action in the Journey
At its core, the model is designed to answer the question: "Based on everything this user has done so far, what is the next item they are most likely to be interested in?" It calculates the likelihood of a user interacting with a specific item (Item Y) given their unique history of interactions (Item X1, X2, and so on).

During the training process, the system reviews all historical user journeys. It learns which item a user typically interacts with after a specific sequence of actions. The system then fine-tunes its logic to get better at predicting that next-best item, making it highly effective at recommending the right product to the right person at the right time. This method of learning from sequences is known as autoregressive modeling.

Aligning Recommendations with Business Goals
The model doesn't just predict the most likely next interaction; it aligns those predictions with your business objectives. Each potential item is assigned a reward value, which represents its importance to your goal. For a "Maximize Revenue" goal, the reward is the total order value. For other goals, it could be a different value that you define.

The system then combines these two pieces of information:

The likelihood that a user will interact with an item.
The reward value of that item for your business.

This system makes sure that the final recommendation isn’t just relevant and personalized to the user's journey but also highly valuable for achieving your specific business goal.

Limitations

Over time, through the continuous process of recommending, observing, and learning from the rewards, the recommendation system becomes increasingly effective at guiding users towards actions that benefit your business objectives.

The system currently focuses on maximizing the immediate reward of each item recommendation. This means it's learning to make the best personalized suggestions right now to drive the desired outcome. This approach is used because user behavior can be influenced by many factors on the platform, such as search results and promotions. Since the recommendation model might not be the only one at play, it can be challenging to directly link a single recommendation to long-term future actions.

SEE ALSO
Engagement Signals and Metrics
Salesforce Help: Engagement Signals
