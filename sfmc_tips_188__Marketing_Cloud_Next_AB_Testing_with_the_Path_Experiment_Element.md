# SFMC Tips #188 : Marketing Cloud Next: A/B Testing with the “Path Experiment” Element

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-a-b-testing-with-the-path-experiment-element-5e39af4e0210

---

# SFMC Tips #188 : Marketing Cloud Next: A/B Testing with the “Path Experiment” Element

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--5e39af4e0210---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--5e39af4e0210---------------------------------------)

5 min read

·

Oct 9, 2025

--

Photo by [mehrab zahedbeigi](https://unsplash.com/@estoymhrb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The **“Path Experiment”** element in Marketing Cloud Next Growth & Advanced Edition combines the capabilities of **“Random Split”** and **“Path Optimizer”** in Marketing Cloud Engagement.

With this element, you can randomly divide audiences into different paths or run full-fledged **A/B tests** within your marketing flows.

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843), a new feature was introduced that **automatically** determines the winning path based on specific engagement results, enabling more efficient and data-driven test management. In this article, I’d like to introduce an overview of this new functionality.

> *Note: The “Path Experiment” element is available exclusively in the* ***Advanced Edition****.*

## **What Is a Random Split?**

A **Random Split** is a feature that divides recipients into multiple paths based on **predefined percentages**. By using this function, you can compare and analyze engagement results across each path and later identify which path performed most effectively.

**Basic Usage**  
For example, if you set the split to **34% : 33% : 33%**, the system aims to distribute contacts evenly across three paths. However, this is only a statistical expectation — **there’s no guarantee that the results will be perfectly even**.

**How It Works**  
The mechanism that randomly assigns contacts to each path is similar to a **coin toss**. For instance, if there are 10 contacts, it’s possible — by chance — that they might be distributed as 10 to 0 or 7 to 3. It’s important to understand that such randomness is an inherent part of this feature.

![]()

### **How to Configure a Random Split**

1. Open the **Path Experiment** configuration screen and set the **label** **name** and **API name**. Then, under Configure Path Selection, click **Manual**, and **uncheck** “Test a subset of the audience”.

- ✅ Checked: **Path Optimizer** (Manual Test)
- ⛔ Unchecked: **Random Split**

2. You can add up to **10 paths** and freely adjust the percentage allocation for each.

3. It’s also easy to evenly distribute percentages across paths or rearrange their order.

## **What Is Path Optimizer?**

**Path Optimizer** is a feature that compares engagement results for each path among test recipients during a defined testing period. It then determines the most effective path (the winning path) and sends the remaining recipients to that path, either **automatically** or **manually**.

> *Note: Although the official name “Path Optimizer” is not used in Marketing Cloud Next, this article uses the term for convenience.*

You can choose between the following two selection methods for determining the winning path:

- **Automated** (new in Winter ’26)
- **Manual**

### ① How to Configure Path Optimizer (Automated)

1. Open the **Path Experiment** configuration screen and set the **label name** and **API name**. Then, under Configure Path Selection, click **Automated**, and select which metric will be used to determine the winning path.

2. Available metrics include standard options such as:

- **Higher email click rate**
- **Higher email open rate**
- **Lower email opt out rate**

In addition to these, you can also select **custom metrics** using **Engagement Signals**.

3. Set the **test group percentage** and **test duration**. After the test period ends, if you select **“Select the Best Performer”,** the remaining recipients will automatically be sent down the **winning path**.

4. You can add up to **10 paths** and freely adjust the percentage allocation for each.

5. Even after the flow is activated, you can monitor the test results during the testing period and manually select the winning path if necessary.

### ② How to Configure Path Optimizer (Manual)

1. Open the **Path Experiment** configuration screen and set the **label name** and **API name**. Then, under Configure Path Selection, click **Manual**, and **check** “Test a subset of the audience”.

- ✅ Checked: **Path Optimizer** (Manual Test)
- ⛔ Unchecked: **Random Split**

2. Set the **test group percentage** and **test duration**.

3. You can add up to **10 paths** and freely adjust the percentage allocation for each.

4. After activating the flow, analyze the results during the test period and manually select the **winning path**.

> ***Note:*** *If you do not manually select a winning path during the test period, the remaining group will* ***exit the flow at the Path Experiment element*** *and will not proceed to any subsequent activities. ⚠️*

## Additional Notes

The **Path Experiment** feature is part of **Salesforce Personalization**. While it cannot be reused, the conditions you set are recorded as two separate records when the flow is **activated**. These records are managed based on the **Label Name** of the Path Experiment element:

- **Personalization Points**

- **Experiments**

Be cautious when creating multiple Path Experiments with the same label name, as it may become difficult to distinguish which record corresponds to which experiment.

Additionally, since enhancements were made in Spring ’26, I have written an article about them below.

### Four New Features Added in Spring ’26

1. **Automatic notifications of Path Experiment results**
2. **Manual path selection during debug execution**
3. **Change tracking via the History tab**
4. **Enhanced Analytics tab (viewable within the canvas)**

[## SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

### In the Spring ’26 new feature release of Marketing Cloud Next, several important enhancements have been made to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961?source=post_page-----5e39af4e0210---------------------------------------)

That’s all for this overview.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
