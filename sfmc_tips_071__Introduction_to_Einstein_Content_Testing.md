# SFMC Tips #71 : Introduction to Einstein Content Testing

**Source:** https://medium.com/@marketingcloudtips/introduction-to-einstein-content-testing-62a8477656ff

---

# SFMC Tips #71 : Introduction to Einstein Content Testing

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--62a8477656ff---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--62a8477656ff---------------------------------------)

5 min read

·

Jan 2, 2025

--

Photo by [Lacie Slezak](https://unsplash.com/@nbb_photos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud offers two AI-powered A/B/n image testing features:

- **Einstein Content Selection**
- **Einstein Content Testing**

While “Einstein Content Selection” was released earlier, its complexity made it less accessible to most Marketing Cloud users.

In response, the simpler “Einstein Content Testing” was introduced as a new feature in Winter ’23. This article will provide an overview of this powerful new feature.

## What is Einstein Content Selection (Content Testing) ?

Let me start by explaining the overview of “Einstein Content Selection” and “Einstein Content Testing”. These features ultimately serve the same purpose.

1. **AI-Driven Image Optimization**  
   This feature automatically selects the best-performing image from a pre-uploaded set based on factors like time of day or day of the week and displays it in your emails.
2. **Real-Time Optimization**  
   Using engagement data from sent emails (such as opens and clicks), Einstein optimizes the images displayed for recipients who open emails later.
3. **Image-Level Analytics**  
   You can analyze performance metrics, such as click rates, for each image.

## Differences from Other Features

1. **Comparison with A/B Testing in Email Studio**  
   A/B Testing determines the winner based on engagement metrics (like click rates) collected over a set period. In contrast, Einstein Content Selection uses AI to select the winner in real-time.
2. **Comparison with Einstein Recommendations**  
   Einstein Recommendations determines the images to display based on online behavior by embedding tags into e-commerce sites and similar platforms. On the other hand, “Einstein Content Selection” and “Einstein Content Testing” optimize content based on real-time email engagement, such as opens and clicks.

## How to Set Up Einstein Content Testing

Einstein Content Testing is user-friendly and ideal for beginners. Follow these steps to get started:

### 1. Create a Content Test

- **Navigation**: Go to the “Einstein Content Testing” section from the Einstein feature list in the App Switcher and click “**New Test**”.

- **Name and Description**: Enter a name for the test and optionally add a description to inform other users about its purpose.

### 2. Set Test Images

You can test up to **32 images**. For each image, provide:

- Image file
- Image name
- Link URL

Images can be uploaded manually or selected from:

- Content stored in Content Builder
- Image URLs
- Images added to Einstein Content Selection (ECS)

### 3. Choose Test Mode

**Automated Testing**: Uses AI (Einstein) to automatically select the winner.

**Manual Control**: Similar to A/B testing in Email Studio, where you can:

- Choose the winner manually.
- Select the winner based on the highest click rate after a set number of clicks (user-defined threshold).

### 4. Review and Publish

Review your settings and click “Publish” to finalize the test.

### 5. Use in Content Builder

Once published, the test will be available as a content block in Content Builder.

## Frequently Asked Questions (FAQ)

### **Q: Are auto-opens caused by Apple Mail app’s MPP or Gmail app’s background updates treated as “opens” in Content Testing?**

**A:** Yes, they are treated as “opens”. Shortly after sending the email, the “**Total Selections**” (i.e., the number of cases processed by Einstein) may be counted immediately. This count includes contacts that were marked as opened due to backend processing, even though the recipient has not yet actually opened the email.

**⚠️** This auto-open behavior can be a challenge when using Einstein Content Testing or Einstein Content Selection. These features aim to display the optimal image upon opening, but auto-opens may finalize the displayed image before Einstein or the user determines the “winner”.

### **Q: How can I manually control and “choose the winner” myself?**

**A:** You can manually choose the final image by selecting “Stop Test” in the management interface and then selecting the desired image. This requires visiting the interface at the appropriate time to make the selection.

![]()

### **Q: How are super messages consumed?**

**A:** Both Einstein Content Testing and Einstein Content Selection consume impressions. Specifically, an additional **2 super messages** are consumed at the time of opening. This means each contact requires **1 super message for sending** and **2 super messages upon opening**, totaling **3 super messages per contact**.

Additionally, once an asset is displayed upon opening, it will remain the same for **90 days**. If the email is opened again after 90 days, a new asset will be displayed, but no additional super messages are consumed for this update. Importantly, super messages are only consumed on the **first open**; even if a contact opens the email 10 times, it won’t consume super messages 10 times. Similarly, after 90 days, new assets will load without consuming additional super messages.

For plain text versions of emails, enabling this feature will only display URL links. Opening such emails will not incur any charges, but clicking the link will consume **2 super messages**.

### **Q: I conducted a test with a small number of users, but the “Total Selections” (cases processed by Einstein) slightly exceeds the total number of emails sent. Why?**

**A:** The images displayed in the “Summary” of the Email Studio tracking screen are counted as Einstein Content Selection impressions.

Also, while previewing an email using “Preview and Test” in Email Studio does not consume Einstein Content Selection impressions, test sends followed by opening the email will consume them.

## Conclusion

Einstein Content Testing is an easy-to-use AI feature within Salesforce Marketing Cloud. Why not give it a try and see how it enhances your email campaigns?

That’s it for now — thank you for reading!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
