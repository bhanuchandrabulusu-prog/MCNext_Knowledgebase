# SFMC Tips #135 : Marketing Cloud Next: Einstein Decision Element in Flow Builder

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-einstein-powered-decision-element-in-flow-builder-26c34372b92c

---

# SFMC Tips #135 : Marketing Cloud Next: Einstein Decision Element in Flow Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--26c34372b92c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--26c34372b92c---------------------------------------)

4 min read

·

Jun 10, 2025

--

Photo by [Andrew Gwizdowski](https://unsplash.com/@andrew_gwiz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**New Feature: Summer ’25 Release**  
In the Summer ’25 release, Flow Builder introduces a new decision element, “**Einstein Decision**”, which leverages AI (Einstein).

This feature allows users to easily create splits utilizing two AI analytics tools: **Einstein Engagement Scoring** and **Einstein Engagement Frequency**. Note that these Einstein features are available exclusively in the **Marketing Cloud Advanced Edition**.

## Key Features of Einstein Decision

For users familiar with **Marketing Cloud Engagement**, the interface will feel intuitive, but the setup process has been significantly streamlined compared to before.

Previously, configuring each path required manual effort, one step at a time. With Einstein Decision, paths are automatically generated with just a few clicks.

For example, selecting the **Persona Splits** option within **Einstein Engagement Scoring** generates splits like the following:

Unnecessary paths can be easily removed, so you won’t need to worry about irrelevant options cluttering your workflow.

### Persona Classification Use Cases

Let’s revisit the subscriber persona classifications introduced in a [previous article](/@marketingcloudtips/marketing-cloud-on-core-einstein-engagement-frequency-and-scoring-a8c75c105b47) and explore strategic approaches tailored to each type.

### Loyalists

High likelihood of both opens and clicks.

- Create audiences resembling your top-performing recipients.
- Increase sending frequency.
- Send exclusive offers.

### Selective Shoppers

Low open rate but high click likelihood.

- Test subject line optimization.
- Personalize content based on past purchases.

### Window Shoppers

High open rate but low click likelihood.

- Add personalization and recommendations to emails.
- Test different CTAs.
- Experiment with targeted incentives.

### Winback/Dormant

Low likelihood of both opens and clicks.

- Send simple yes/no surveys.
- Try alternate channels like SMS or WhatsApp.
- Launch win-back campaigns with offers.

**Note:** Contacts without data will flow into the “Default Result” path.

The same approach applies to **Einstein Engagement Frequency**.

Unnecessary paths can be removed with a single click.

### Engagement Frequency Use Cases

To further enhance your strategy, let’s revisit how **Einstein Engagement Frequency** classifies engagement levels.

Einstein analyzes the past 28 days of promotional email engagement data and categorizes sending frequency into the following four groups:

### Saturated

(Too many sends)

- Suggests optimal send frequency based on open and click rates.
- Helps reduce subscriber fatigue.

### Almost Saturated

(Near saturation)

- Sending frequency isn’t yet excessive but is on the higher side.

### On Target

(Optimal frequency)

- Maintain the current frequency to maximize results.

### Undersaturated

(Not enough sends)

- Increase sending frequency to capture missed opportunities and drive more revenue.

**Note:** Contacts without data will flow into the “Default Result” path.

## Conclusion

These AI features, such as **Einstein Engagement Scoring** and **Einstein Engagement Frequency**, are incredibly handy tools that can be utilized anytime once the **data graph** is set up. I encourage you to take full advantage of these capabilities to drive more efficient and impactful marketing activities.

⚠️ Finally, let me explain how to configure the Data Graph. If the following Data Graph settings are not completed, **“Einstein Decision” cannot be enabled in the flow**.

## Setting Up the Data Graph

### 1. Define Unified Individual

- Set **Unified Individual** as the Primary Data Model Object.

### 2. Create Connections

- Bridge **Unified Link Individual** to connect the **Individual**.
- Link **Contact Point Email** to enable key metrics.

These steps unlock the following Einstein AI capabilities:

- **Email Engagement Frequency**
- **Email Engagement Score**

**Key Point:** Linking **Contact Point Email** is crucial, as these metrics rely on data tied to **email addresses as the primary key**.

## Configuration Steps

### 1. Email Engagement Frequency

Select **“Email Engagement Classification”** as the metric.

\*This field classifies subscribers based on delivery frequency after analysis.

### 2. Email Engagement Scoring

Configure the following fields to gain actionable insights:

- **Email Engagement Persona**
- **Email Open Likelihood**
- **Email Click Likelihood**
- **Email Subscribe Likelihood**

\*These fields capture data on subscriber personas and engagement probabilities, enabling precise targeting and optimization.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
