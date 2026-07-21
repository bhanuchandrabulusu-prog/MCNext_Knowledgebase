# SFMC Tips #174 : Marketing Cloud Next: How to Set Up Dynamic Content (Email and Landing Pages)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-set-up-dynamic-content-3c8ba2c53036

---

# SFMC Tips #174 : Marketing Cloud Next: **How to Set Up Dynamic Content (Email and Landing Pages)**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3c8ba2c53036---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3c8ba2c53036---------------------------------------)

5 min read

·

Sep 17, 2025

--

Photo by [Nastia Petruk](https://unsplash.com/@mineral_of_demon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Edition, you can create dynamic content tailored to the attributes of each recipient. The key to this process is the **Personalization Point**.

***Note:*** *With the* [*Spring ’26 new feature release*](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb)*, dynamic content is now available not only for email but also for landing pages in production environments. However, dynamic content for landing pages is available only in organizations created in Spring ’25 or later, and it is not available in SDOs.*

## Personalization Point (①)

- **A reusable container** that stores dynamic conditions (Variations and Decisions).
- Within a single piece of content, it can be **linked** and used in multiple places in **sync**, or unlinked to apply individual conditions.
- It can also be copied and reused in other email content.
- By setting a default condition, you can control what is displayed when none of the conditions are met.
- The same Personalization Point name can be used multiple times within an account.

## Elements of a Personalization Point

### **Variation and Decision (②)**

- Named targeting rules.
- It’s a good practice to establish a naming convention for searching and managing them.
- The same Variations and Decisions name can be used multiple times within an account.

### **Targeting Rule (③)**

- Define under what conditions specific content should be displayed.
- Example: Favorite Genre equals Rock
- Composite conditions using AND / OR are also possible.

### **Priority (④)**

- When a customer matches multiple targeting rules, the rule with the higher priority will be applied first.
- Especially useful in cases with vague conditions like “contains ~” or when using composite conditions.

## Configuration Steps

1. Drag and drop components such as “Paragraph” or “Image”, and the “**Dynamic Content**” management section will appear. First, click **+New Variation**.

2. From the **New Variation** button in the upper right, you can create a new condition. If you want to reuse a previously used Personalization Point, select it from the list at the bottom. You can also click View All to open the search screen.

3. If dynamic content has already been set up in the same Email, the Personalization Point used at that time will be labeled as “**Current**”.

4. When you click the applicable Personalization Point, you’ll see that it is already being used in the current email. You can then choose whether to reuse it as a **Link** (synchronized condition) or reuse it by copying.

5. If you use it as a **Link**, the setup is completed immediately, and a “**Linked**” mark appears as shown. You can unlink it later if needed.

6. On the other hand, if you want to create a new one, enter the **Variation and Decision Name** and set the **Targeting Rule**, then save.

> *Note: This is not the name of the Personalization Point.*

7. Once you register the first variation, you’ll be able to add additional variations from the dropdown menu.

8. For each additional variation, also set the **Variation and Decision Name** and the **Targeting Rule**, then save.

9. After creating all variations, click the **Edit Priorities**.

10. Here, configure the **Personalization Point Name** and the **Priority**, then save.

11. Once all the condition settings are complete, create the content for each variation.

> *Note: Content itself* ***cannot be reused****, so each component must be set up individually.*

12. To handle cases where none of the conditions apply, register a **Default Content** as a fallback.

13. Finally, use **Preview** to confirm and check that your settings are correct.

## Considerations

**Number of Personalization Points**  
You can configure up to **25 Personalization Points** in a single email. This allows you to personalize up to 25 components under completely different conditions.

**Number of Variation and Decisions**  
Each Personalization Point can contain up to **15 Variations and Decisions**.

**Reusing Variations**  
The configured content itself (e.g., images or text) is **not reused**. Each component requires its own content setup. What gets reused are the **targeting rules only**.

**Unlinking**  
When you unlink, a new Personalization Point is created and the connection is removed, as shown in the figure below.

## Final Thoughts

When managing this dynamic content, I believe the most important aspect is the **naming convention**. These Personalization Points are used not only for dynamic content but also for other features such as path experiments in segment-triggered flows, which means the number of points will steadily increase. For this reason, it’s essential to organize and save them in a way that makes future reuse easy.

Also, since searches are performed using the **Variation and Decision names**, avoid naming them randomly. Instead, establish a consistent naming standard that makes them easier to find later.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
