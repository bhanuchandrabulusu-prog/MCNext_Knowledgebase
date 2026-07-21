# SFMC Tips #13 : How to Identify Reasons for Failed Email Sends in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-identify-reasons-for-failed-email-sends-in-journey-builder-3731fde54ec5

---

# SFMC Tips #13 : How to Identify Reasons for Failed Email Sends in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3731fde54ec5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3731fde54ec5---------------------------------------)

8 min read

·

Dec 26, 2023

--

Photo by [Chris Lawton](https://unsplash.com/@chrislawton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In cases where email sends fail in the Journey Builder of Salesforce Marketing Cloud, you may want to investigate the reasons behind the unsuccessful delivery.

To examine why an email was not sent, there are several methods available. In this article, I will explore three methods:

- **Method 1: Check on the Email Activity in Journey Builder**
- **Method 2: Review in the History Tab of Journey Builder**
- **Method 3: Verify Using “Extract Not Sent” in Automation Studio**

Each of these methods has different scopes and data retention periods. Method 1 provides a narrow view, while Method 3 allows for broader insights.

Let’s go through each method step by step!

## Method 1: Check on the Email Activity in Journey Builder

This method is suitable for investigating reasons on a **per-Email-Activity basis**.

### Steps for Method 1:

1. Click on the **number** under the Email Activity.

![]()

2. Click on the **“View Contact Details”** link.

![]()

3. Click on the **“View Details”** link.

4. In the **“Status Details”** column under Hard Bounces, the reason for the unsuccessful send will be displayed. You can also search using the Contact Key.

### ***Note for Method 1:***

- Examples of hard errors include being on the (Auto-) Suppression List, domain exclusion, List Detective exclusion, invalid email address, or empty email address.
- Some cases, like Held, Unsubscribed or Exclusion Script, are processed as **“Success”** even though the email wasn’t sent. For such cases, use Method 3 for investigation.
- You can only search the **last 30 days**.

If you encounter issues with email sending in a specific email activity, give this method a spin. As mentioned in the above notes, please be aware that certain reasons for unsuccessful sends may not be searchable, so proceed with caution.

Additionally, **there isn’t a download button for contact lists on the screen**. However, by continuously pressing **‘Load More’** at the bottom of the page until reaching the last page, **you can copy and paste the displayed list into Excel**.

On the flip side, **if you opt for using the REST API, you can download the list of hard errors in CSV format**. Take a look at the following article for guidance on downloading the contact list. I’ve also included sample API code for your convenience.

[## Extracting Contacts Passing Through Wait activities Using Journey Builder REST API

### In the ever-evolving landscape of Salesforce Marketing Cloud, developers often grapple with the challenge of…

medium.com](/@marketingcloudtips/extracting-contacts-passing-through-wait-activities-using-journey-builder-rest-api-8d22ff0048a0?source=post_page-----3731fde54ec5---------------------------------------)

```
--- METHOD  
POST   
  
--- ENDPOINT  
https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/journeyhistory/download?columns=ContactKey,Result.Messages  
  
--- HEADERS   
Content-Type：application/json   
Authorization：Bearer [Access Token]   
x-direct-pipe：true  
  
--- BODY  
{  
  "activityIds": ["24da6e39-df68-4318-87ac-d864306cdb06"],  
  "statuses": ["Failed"]  
}
```

## Method 2: Review in the History Tab of Journey Builder

This method is useful for checking failures across an **entire journey or** **multiple journeys**.

### Steps for Method 2:

1. Open the **History** tab of Journey Builder and click the **Filter** button.

2. Set the filter parameters. The minimum unit for this method is the “Journey Version”. Email Activity level details cannot be checked.

After selecting the Journey Version, set **Activity to “Email”** and **Status to “Failed”**. Click **“Apply”**.

3. The results of the filtering will be displayed on the screen. By default, it shows data from the last 24 hours, so if needed, feel free to adjust the range to a maximum of 30 days.

### ***Note for Method 2:***

- Similar to Method 1, hard errors may include being on the (Auto-) Suppression List, domain exclusion, List Detective exclusion, invalid email address, or empty email address.
- For investigations into Held, Unsubscribed, or Exclusion Scripts, use Method 3.
- You can only search the **last 30 days**.

Now, Method 2 has a perk that Method 1 lacks. It comes with **the CSV download feature**.

However, there’s a slight drawback to this download feature. The inconvenience lies in the fact that **it only targets the currently displayed range**.

The default display count on this screen is 100 items. When downloading, if, as shown in the image above, you’re only downloading four items, it’s all good. But if, for instance, there are 10,000 items, you’ll need to scroll until all 10,000 are visible. Given the increment of 100 items per scroll, it becomes quite a task.

So, in cases like this, as explained earlier in Method 1, **consider leveraging the download through REST API**.

When downloading on a journey basis, use definitionIds instead of activity IDs. You can search using the following SQL, **where definitionIds represent the Journey Version ID**.

```
SELECT VersionID  
FROM _Journey  
WHERE JourneyName = 'Journey Name'  
AND VersionNumber = 'Journey Version Number'
```

The API code sample is as follows:

```
--- METHOD  
POST   
  
--- ENDPOINT  
https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/journeyhistory/download?columns=ContactKey,Result.Messages  
  
--- HEADERS   
Content-Type：application/json   
Authorization：Bearer [Access Token]   
x-direct-pipe：true  
  
--- BODY  
{  
  "definitionIds": ["24da6e39-df68-4318-87ac-d864306cdb06"],  
  "activityTypes": ["emailv2"],  
  "statuses": ["Failed"]  
}
```

## Method 3: Verify Using “Extract Not Sent” in Automation Studio

This method is used to **extract all history of unsuccessful sends in the Marketing Cloud account** and determine the reasons behind the failed email sends.

This includes email sends from Email Studio and Transactional Send Journeys.

### Steps for Method 3:

1. Set up a **new automation**.

2. In Step 1 of the automation, drag and drop a Data Extract activity.

3 Configure the new Data Extract Activity.

4. Name it appropriately. The file naming pattern should be **“\*.zip”**. After naming it, add the extension “.zip”.

Select **“Tracking Extract”** as the extraction type. If “Tracking Extract” is not visible, request support to enable the feature.

![]()

5. Set filter conditions. You can configure it to extract data for the **last 90 days**.

Choose **“Extract Not Sent”** as the extraction type.

6. In Automation Step 2, drag and drop the File Transfer Activity.

7. Choose **“Move a File From Safehouse”** here.

8. The file naming pattern here should be **the same as decided in the Data Extract Activity**. Enter the same name and don’t forget to add the “.zip” extension.

Select the FTP directory where the ZIP file will be stored as the destination.

![]()

9. The setup is now complete. Place the schedule in the Automation Settings screen. By scheduling, you make **“Run Once”** possible. No additional schedule settings are necessary. Press **“Save”** afterward.

10. Click **“Run Once”**.

11. Once this automation is complete, the ZIP file will be placed on the FTP. Download and unpack it.

The stored data includes information where you can check the reasons in the **“Reason”** column.

### ***Note for Method 3:***

- As the data is extracted in a ZIP file, please name the file as ‘.zip’. Ultimately, you’ll need to confirm the details in a CSV file, but it won’t extract correctly if named ‘.csv’.
- You can only search within the **last 90 days**. (Though the help documentation mentions the last 2 months, in reality, it seems you can extract data for the last 90 days.)
- For Email Studio email sends, the TriggeredSendExternalKey field will be **blank**.
- In the case of Transactional Send Journeys, the value in the TriggeredSendExternalKey field will be the **Event Definition Key**.
- There may be duplicate records due to different BatchIDs, so please be careful when checking quantities.
- When storing these files in a Data Extension, ensure that EmailAddress is stored as a **text type**, not as an email address type. If List Detective prevented sending due to a specific reason, the subscriber key will be entered.

### Reasons Why Emails Were Not Sent

Finally, here are some common reasons why emails were not sent, which can be found in the “Extract Not Sent” list. Please refer to them.

- **Held**  
  The subscriber status is set to “Held” (Undeliverable) in all subscriber lists.
- **Unsubscribed Master**  
  The subscriber status is set to “Unsubscribed” in all subscriber lists.
- **Account Level Opt Out**  
  The subscriber has globally unsubscribed at the account, enterprise, or business unit level. This usually appears redundantly with the “Unsubscribed Master” entry and can generally be ignored.
- **Send Failure**  
  The email failed to send for some reason. The specific cause is not provided.
- **Invalid Email Address**  
  The email address is invalid for some reason.  
  *Example: An address like “abc@yahoo.co”, where the final “m” is missing.*
- **Build Email Error**  
  An error occurred while attempting to build the email.
- **Excluded by Send Time Filter**  
  The subscriber was excluded by a send-time filter script.
- **Domain Exclusion**  
  The email address belongs to a domain excluded by the domain exclusion feature.
- **Suppression List Exclusion**  
  The email address is excluded due to being on the suppression list or automatic suppression list.
- **List Detective Exclusion**  
  The email address is excluded by the List Detective feature.

For other reasons why emails may not have been sent, please refer to the help documentation below.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=ja&id=sf.mc_es_email_send_error_codes.htm&type=5&source=post_page-----3731fde54ec5---------------------------------------)

## Conclusion

Feel free to choose the method that best suits your investigation needs in Journey Builder email sends. Each method has its advantages and ease of use, so select accordingly. This concludes our discussion on investigating reasons for failed email sends in Journey Builder.

Happy email unraveling! 🕵️‍♂️✉

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
