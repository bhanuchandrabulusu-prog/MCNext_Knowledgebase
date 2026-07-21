# SFMC Tips #113 : Marketing Cloud Next: Einstein Engagement Frequency & Engagement Scoring

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-einstein-engagement-frequency-and-scoring-a8c75c105b47

---

# SFMC Tips #113 : Marketing Cloud Next: Einstein Engagement Frequency & Engagement Scoring

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a8c75c105b47---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a8c75c105b47---------------------------------------)

4 min read

·

May 10, 2025

--

Photo by [Erol Ahmed](https://unsplash.com/@erol?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the **Marketing Cloud Advanced Edition** (Marketing Cloud Next), you can unlock two powerful AI-driven features:

1. **Einstein Engagement Frequency**
2. **Einstein Engagement Scoring**

These features empower you to optimize email deliverability, ensuring you avoid over-emailing subscribers while maintaining engagement with loyal customers.

## Getting Started: Configuring the Data Graph

To use these features, you must configure your **Data Graph**, akin to Data Designer in Marketing Cloud Engagement’s Contact Builder. Learn more in the article below:

[## SFMC Tips #96 : Marketing Cloud on Core: Personalization

### In Marketing Cloud on Core (Marketing Cloud Growth Edition / Advanced Edition), you can deliver personalized messages…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026?source=post_page-----a8c75c105b47---------------------------------------)

## Setting Up the Data Graph

### **1. Define Unified Individual**

- Set **Unified Individual** as the Primary Data Model Object.

### **2. Create Connections**

- Bridge **Unified Link Individual** to connect the **Individual**.
- Link **Contact Point Email** to enable key metrics.

These steps unlock the following Einstein AI capabilities:

- **Email Engagement Frequency**
- **Email Engagement Score**

**Key Point:** Linking **Contact Point Email** is crucial, as these metrics rely on data tied to **email addresses as the primary key**.

## Configuration Steps

### **1. Email Engagement Frequency**

Select **“Email Engagement Classification”** as the metric.

\*This field classifies subscribers based on delivery frequency after analysis.

### **2. Email Engagement Scoring**

Configure the following fields to gain actionable insights:

- **Email Engagement Persona**
- **Email Open Likelihood**
- **Email Click Likelihood**
- **Email Subscribe Likelihood**

\*These fields capture data on subscriber personas and engagement probabilities, enabling precise targeting and optimization.

## Einstein Engagement Frequency

This AI-driven feature recommends the optimal email delivery frequency for each contact, helping to:

- Prevent email fatigue
- Reduce unsubscribe rates
- Enhance customer satisfaction

### Requirements for Use

To generate a model:

- You need at least **10 recipients** in the account.
- A minimum of **5 promotional emails** must have been sent within the past 28 days.

### How It Works

Einstein evaluates the last 28 days of email engagement data to classify recipients into four categories:

### **1. Saturated**

- Receiving too many emails.
- Recommendation: Reduce frequency to avoid stress.

### **2. Almost Saturated**

- Close to saturation; adjustments needed.

### **3. On Target**

- Ideal frequency; maintain consistency.

### **4. Undersaturated**

- Receiving too few emails.
- Recommendation: Increase frequency to maximize engagement.

**Note:** Contacts with insufficient data are routed through a **default** path.

## Einstein Engagement Scoring

This feature provides insights into subscriber personas and engagement likelihoods, enabling you to craft more targeted strategies.

### Requirements for Use

- Requires each recipient to have received at least one email.

### How It Works

Einstein analyzes 90 days of engagement data and classifies subscribers into personas and likelihood splits:

### **Subscriber Personas**

### **1. Loyalist**

- High open and click likelihood.
- Strategies: Increase email frequency, create lookalike audiences, send exclusive offers.

### **2. Selective Subscriber**

- Low open but high click likelihood.
- Strategies: Optimize subject lines, personalize content based on past purchases.

### **3. Window Shopper**

- High open but low click likelihood.
- Strategies: Add recommendations, test CTAs and incentives.

### **4. Winback/Dormant**

- Low open and click likelihood.
- Strategies: Use surveys, alternative channels (e.g., SMS), or win-back campaigns.

### **Engagement Likelihood Splits**

Subscribers are also categorized into likelihood tiers for:

- **Open Likelihood Split**
- **Click Likelihood Split**
- **Subscription Retention Likelihood Split**

The tiers include:

- **Most Likely**
- **More Likely**
- **Less Likely**
- **Least Likely**

### **Note:**

- Contacts with insufficient data are routed through the **default** path.
- The **Conversion Likelihood Split** (available in Marketing Cloud Engagement) is not supported in Marketing Cloud Growth & Advanced Edition.

## Next Steps: Leveraging AI Features

Once the data graph is configured, select email engagement frequency or email engagement score to create branches in your flow using decision elements. Alternatively, leveraging them for segmentation can also be effective. Consider displaying the Einstein Score on the CRM record page as well.

Maximize the potential of these AI-driven features to boost engagement and drive results!

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
