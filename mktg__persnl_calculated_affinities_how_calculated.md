# How Affinities are Calculated

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_calculated_affinities_how_calculated.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
How Affinities are Calculated

Personalization uses a standard summation model when calculating affinity. This model uses various factors that dictate affinity scoring output.

FACTOR	SCORE EFFECT
Engagement Signals	Engagement signals defined on the calculated affinity object function as event definitions. When an engagement signal is registered that is referenced in a calculated affinity (eg. product view), the affinity score is automatically updated. Real-time CA’s update in real-time.
Signal Strength	Engagement signals strength is classified as high, medium, or low. A high strength signal affects a score by 5 points, a medium signal by 3 points, and a low signal by 1 point. Signal strength values impact the overall score in either the positive or negative direction, depending on their individual impact settings.
Signal Impact	You can define whether engagement signals have a positive or negative impact on the affinity score. For example, you can define certain signals (views, add to carts, or purchases) as positive, and other signals (returns or complaints) as negative. Positive signals add points to the affinity score. Negative signals subtract points from the score.
Lookback Window	The lookback window defines how far back engagement events are referenced for affinity calculations. For example, for a lookback of 30 days, the affinity calculation includes only engagement events that occurred in the last 30 days.
Decay	

Affinity decay considers how recently, and how often, engagement occurs within the lookback window, and uses an exponential model when calculating the decay of the affinity value.

Following the calculated insight refresh schedule (every hour for real-time calculated insights), Personalization calculates affinity decay using a batch process. The decay calculation exponentially decreases the affinity to 1% of its starting value over the defined lookback window in days.

To better understand how affinity is calculated, refer to this example configuration.

CONFIGURATION SETTING	VALUE
Affinity Type	Real-Time
Lookback Window	30 days
Decay	Enabled
Affinity Object	Goods Product
Selected Object Fields	Brand
Engagement Signal (Strength; Impact)	
Product View (Low; Positive)
Add to Cart (Medium; Positive)
Purchase (High; Positive)
Return (Medium; Negative)

When you save these configuration settings, a real-time affinity calculated insight is created and added to the profile data graph you selected when defining the calculated affinity. As engagement signals are registered, the affinity calculation updates the score based on signal strength and impact. As an example, this table shows an engagement pattern for a single day, and the associated score impact for each engagement.

SIGNAL REGISTERED	IMPACT	BRAND SCORE
View	+1	BrandA: 1
View	+1	BrandA: 2
View	+1	BrandA: 3
Add to Cart	+3	BrandA: 6
Purchase	+5	BrandA: 11

The affinity score starts at 0, increases for positive engagement signals, and decreases for negative engagement signals. Decay is factored in using a batch process that’s based on the calculated insight refresh schedule.

IMPORTANT When defining affinity engagement scoring for use with targeting rules, segmentation logic, and recommendation filters, make sure to consider the rate at which engagement signal scores can increase or decrease. Creating a rule or segment that targets people with a very high affinity score can require a lot of engagement events before reaching the affinity level you set. For example, defining only two, low-strength engagement signals for an affinity, but creating a rule or segment with an affinity score minimum of 70, can result in very few people becoming eligible for the rule or segment.
SEE ALSO
Using Calculated Affinities
Engagement Signals
Configure a Real-Time Calculated Affinity
Calculated Affinities
