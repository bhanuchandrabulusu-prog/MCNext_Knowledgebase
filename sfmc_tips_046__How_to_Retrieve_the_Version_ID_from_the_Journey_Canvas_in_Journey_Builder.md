# SFMC Tips #46 : How to Retrieve the Version ID from the Journey Canvas in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-retrieve-the-version-id-from-the-journey-canvas-in-journey-builder-85771539302c

---

# SFMC Tips #46 : How to Retrieve the Version ID from the Journey Canvas in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--85771539302c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--85771539302c---------------------------------------)

3 min read

·

Jun 18, 2024

--

Photo by [Nik](https://unsplash.com/@helloimnik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Summer ’24 release of Salesforce Marketing Cloud, **you can now obtain the Version ID of a journey directly from the Journey Builder canvas**. This is a significant improvement, making it much easier to access for troubleshooting purposes.

[## SFMC Tips #42 : Summer ’24 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Summer ’24, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/summer-24-release-highlights-notable-new-features-in-marketing-cloud-0d9ba139c988?source=post_page-----85771539302c---------------------------------------)

Previously, **you could retrieve the Journey ID**, which is a higher-level ID compared to the Version ID, from the screen. **The Journey ID was displayed in the URL, and you could obtain it by copying the part of the URL after “%23”**.

Additionally, **you could also retrieve the Activity ID**, a lower-level ID compared to the Version ID, from the screen. I’ve previously written a standalone article on this topic, which you can refer to for more details.

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----85771539302c---------------------------------------)

![]()

Now, let’s see where you can find the Version ID. **By clicking the arrow next to the journey name, the Definition ID will be displayed**. This Definition ID is actually the Version ID.

To confirm that this Definition ID (e.g., 494bf347–3083–463f-a8b3-f2436542e7a6) is indeed the Version ID, you can query the data view as follows:

```
SELECT JourneyID,  
       VersionNumber,  
       VersionID  
FROM _Journey  
WHERE JourneyID = '7af07913-1dbc-46b8-b8e3-d0dac692bea5'  
AND VersionNumber = '181'
```

As you can see, this confirms that the Definition ID is the Version ID.

In addition to displaying the Version ID, **the Summer ’24 release also shows the number of activities on the journey canvas**. This feature is quite useful, as Salesforce recommends a maximum of 150 to 200 activities. Having this count automatically displayed can help manage your journeys more effectively.

That’s all for now.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
