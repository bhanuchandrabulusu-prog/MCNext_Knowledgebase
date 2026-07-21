# SFMC Tips #99 : Spring ’25 Spotlight: Revolutionizing MobilePush with Test Sends

**Source:** https://medium.com/@marketingcloudtips/spring-25-spotlight-revolutionizing-mobilepush-with-test-sends-a2274920d18f

---

# SFMC Tips #99 : Spring ’25 Spotlight: Revolutionizing MobilePush with Test Sends

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a2274920d18f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a2274920d18f---------------------------------------)

6 min read

·

Apr 11, 2025

--

Photo by [omid armin](https://unsplash.com/@itsomidarmin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud Engagement has introduced a long-awaited feature in the Spring ’25 release: the ability to test send MobilePush messages. This feature allows users to preview push notifications, in-app messages, and inbox messages, including personalization, text layout, and content, before they are sent.

It seems that Marketing Cloud Engagement has finally added a test send screen for MobilePush. Let’s take a closer look at how it works!

## Background

Until now, MobilePush lacked a test send function, meaning users had no choice but to test their messages using live sends. This often required extra caution during live operations to avoid errors. However, with this release, test sending has become much easier — a revolutionary improvement!

That said, if you use this feature without fully understanding the setup steps and precautions, there is a risk of accidental sends. Let’s review the correct steps to use this feature safely.

## Message Types Supported by Test Sends

Test sends are available for the following types of messages:

- **Push Notifications** (Outbound Push Messages)
- **In-App Messages**
- **Inbox Messages**

## Setup Steps

**1. Create the Message in Content Builder**  
Start by creating your message in Content Builder as usual. However, note that Content Builder itself does not include a test send function.

**2. Perform the Test Send in Journey Builder**  
Next, navigate to Journey Builder, where you can add a **Push Notification activity**. Select the content you want to test, and use the **“Send Test”** button in the **Message Configuration** tab to execute the test.

## Options for Selecting Test Send Targets

When performing a test send, you can choose from the following four options:

1. **Test Audience**  
    Send to mobile lists or data extensions.
2. **System Token**  
    Target a specific device using a unique system token.
3. **Device ID**  
    Target a specific device using a unique device ID.
4. **Contact Key**  
    Specify an individual contact key to send a test. Note that if a contact key is associated with more than 50 registered devices, the test send is limited to a maximum of 50 devices.

## Important Considerations

### 1. No Confirmation Screen

For all four sending methods, there is no confirmation screen before executing the test send. The final button is labeled **“Next”**, so if you accidentally select a customer data extension, you might end up sending messages to real customers. Exercise caution!

### 2. Handling Multiple Devices

If a single contact key is associated with multiple devices, such as an iPhone and an iPad, selecting that contact key will send messages to all associated devices. To target a specific device, use **System Token** or **Device ID** instead.

### 3. **SuperMessage Consumption**

Test sends also consume SuperMessages.

## Test Audience

When selecting the **Test Audience**, you can choose between a MobilePush mobile list or a data extension created in **Contact Builder**.

The **Next** button appears at the bottom of the screen. Be cautious — clicking this button will immediately begin the send process.

### Important Note

While you can choose to send to a **mobile list** instead of a **data extension**, issues such as missing personalization strings or send errors may occur if the data extension lacks the necessary field data.

Upon clicking **Next**, the sending process progresses as shown below. By the time this screen is displayed, the test send has already been completed.

## System Token & Device ID

For **System Token** and **Device ID**, the interface is the same. Enter the system token or device ID in the input field at the center of the screen to proceed with the send.

Just like with Test Audience, clicking the **Next** button will immediately initiate the send process. Be sure to verify the details of the contact beforehand.

### Sample Query to Retrieve System Token and Device ID

Use the following sample query to retrieve the system token and device ID using the **Contact ID**. Note that the data view **\_PushAddress** does not support contact keys, so you must use the Contact ID.

```
SELECT    
    _ContactID AS [ContactID],    
    _DeviceID AS [DeviceID],    
    _SystemToken AS [SystemToken],    
    _HardwareId AS [HardwareId],    
    _Platform AS [Platform],    
    _PlatformVersion AS [PlatformVersion],    
    _CreatedDate AS [CreatedDate]    
FROM _PushAddress    
WHERE _ContactID = '7549958'
```

The **Contact ID** can be found in the **Attributes** tab.

## Contact Key

For **Contact Key**, begin by entering the contact key and clicking **Next**. At this point, the send process has not yet started.

On the next screen, you’ll be prompted to select the device. However, the interface does not indicate whether the device is an iPhone or an iPad.

Clicking **Next** at this stage will initiate the send process, so proceed with caution.

## Test Send Results

The results of the test send can be verified in **Contact Builder**. The message definition name will have a **“TEST-”** prefix, and the **Address** will display the device ID, allowing you to see the results per device.

## Additional Notes

- The newly introduced **Carousel Push Notifications**, available in the Spring ’25 release, do **not** support test sends.
- For **standard push notifications**, test sends are not available if the content was created with buttons in **Content Builder** or **Journey Builder**. However, if you create a standard push notification without buttons, you can use this feature to test the title, subtitle, message, media, and open behavior.

## Final Thoughts

This Spring ’25 release might have been a jackpot for users who frequently use MobilePush. It’s known that the following updates were included in this release. While my exploration stops here due to the involvement of development efforts, simply being aware of these added features can be quite handy.

### **Inbox 2.0**:

With Inbox 2.0, you’re no longer limited to using a CloudPage as the only call to action. Now, you can select from a variety of calls to action, such as an app or web URL, and include personalized subject and message components in your send message. You also have the option to make your messages accessible to a mobile user’s inbox even if push delivery fails or the push notification is accidentally dismissed. ([Dev](https://developer.salesforce.com/docs/marketing/mobilepush/guide/implement-inbox-messaging-ios.html), [Help](https://help.salesforce.com/s/articleView?id=mktg.mc_mp_create_and_send_inbox_2_message.htm&type=5))

### **Carousel Push Notifications**:

Use the Carousel template to create a push notification that can have up to 6 images. This lets you show multiple images in one notification. ([Dev](https://developer.salesforce.com/docs/marketing/mobilepush/guide/ios-extension-sdk-integration.html), [Help](https://help.salesforce.com/s/articleView?id=mktg.mc_ceb_create_carousel_push_notification.htm&type=5))

### **Test Sends**:

Send a test push notification, In-App Message (IAM), or inbox message to a user or device to verify content and personalization before scheduling or triggering the actual send. ([Help](https://help.salesforce.com/s/articleView?id=mktg.mc_mp_test_send.htm&type=5))

### **New Event** Notifications:

Receive near real-time updates on user engagement with new MobilePush events introduced in Event Notification Service (ENS). Get notified if a user installs and opens your app for the first time with the Install event. Use the Inactive Devices event to identify when users stop using your app so that you can re-engage them with targeted campaigns through other channels. ([Dev](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/mobilepush_events.html), [Dev](https://developer.salesforce.com/docs/marketing/mobilepush/guide/ios-extension-sdk-integration.html), [Help](https://help.salesforce.com/s/articleView?id=mktg.mc_mobilepush_events.htm&type=5))

Additionally, although this time I focused on explaining Journey Builder, the test send interface in MobilePush offers similar functionalities — so be sure to give it a try!

That’s it for now — thank you for reading!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
