# SFMC Tips #235 : Agentforce: Adaptive Response Formats with Apex

**Source:** https://medium.com/@marketingcloudtips/agentforce-adaptive-response-formats-with-apex-65adccf18547

---

# SFMC Tips #235 : Agentforce: Adaptive Response Formats with Apex

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--65adccf18547---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--65adccf18547---------------------------------------)

11 min read

·

Jan 15, 2026

--

Photo by [Oswald Elsaboath](https://unsplash.com/@ozzzyphotos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous and the one before that articles, I introduced UI customization for Agentforce chat using “**Custom Lightning Types**”.

[## SFMC Tips #233 : Agentforce: Custom Lightning Types (Collection Renderer Override)

### In Agentforce, standard Lightning Types are typically used by default, so the UI tends to be simple.

medium.com](/@marketingcloudtips/sfmc-tips-233-agentforce-custom-lightning-types-collection-renderer-override-c3b7ad840303?source=post_page-----65adccf18547---------------------------------------)

[## SFMC Tips #234 : Agentforce: Custom Lightning Types (Editor + Renderer Override)

### In the previous article, I introduced how to display a rich UI in Agentforce by using Custom Lightning Types with a…

medium.com](/@marketingcloudtips/agentforce-custom-lightning-types-editor-renderer-override-c4e408bc7819?source=post_page-----65adccf18547---------------------------------------)

Custom Lightning Types are implemented as code-based solutions using LWC, which makes them highly flexible and expressive. However, in addition to Apex, they require frontend development knowledge such as JavaScript, HTML, and CSS.

To complement that hurdle, the “**Adaptive Response Formats**” was introduced.  
By using this feature, the agent automatically selects the optimal response display (text / links / images, etc.) within the conversation according to the returned data structure.

> *At the time of writing this article, it is available for* ***Service Agents****.*

![]()

## Enabling / Disabling the Adaptive Response Formats

The “**Adaptive Response Formats**” is enabled **by default** when creating a new agent.  
If you want to disable it, configure the setting from the “**Connections**” menu in Agent Builder.

![]()

> *In my screen above, the* ***new “Connections” screen is enabled****, but note that the Adaptive Response Formats does not work with “Enhanced Chat v2” and is available only in the “****Messaging (Enhanced Chat v1)****” channel.*

## 💡 Should it always be enabled?

Since this feature provides richer displays, you might think, “Isn’t it fine to always keep it enabled?”  
However, if the response structure is simple and you only want text-based interactions, disabling it is recommended.

For example, in cases where:

- An image URL does not exist
- Only a link URL is included

the display can become half-baked and not very visually appealing.

## Available Response Formats (2 Types)

Currently, the following two types are provided.

**Rich Choice Response**  
Rich UI Question Display with Customer-Specific Records

**Rich Link Response**  
Web page link display with a text title and image

## What We Will Verify This Time

This time, we will try an implementation using Salesforce’s official sample data.  
Since the data is hard-coded, there is no need to prepare new objects or records.

With this action, it is possible to implement a scenario where, in response to the question “**What’s on the menu?**”,  
“**food options and their detailed information are provided to the user**”.

Now, let’s take a look at the setup steps!

## Setup Steps

## 1. Create an Apex Class

From the setup screen, search for **Apex Classes** and save the following code as a new Apex class.

```
public class GetFoodDetailsInvocable {  
  
    @InvocableMethod(  
        label='Get Food Details'  
        description='Returns linkURL, linkTitle, image linkURL, image MIME Type, and description text for a given food name'  
    )  
    public static List<FoodDetailResponse> getFoodDetails(List<FoodDetailRequest> requests) {  
        List<FoodDetailResponse> responses = new List<FoodDetailResponse>();  
  
        for (FoodDetailRequest request : requests) {  
            FoodDetailResponse response = new FoodDetailResponse();  
            FoodDetail foodDetail = new FoodDetail();  
  
            String foodName = (request.foodName == null) ? '' : request.foodName.toLowerCase();  
  
            // Populate food details dynamically from selections  
            if (foodName.contains('pizza')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/pizza';  
                foodDetail.linkTitle = 'Delicious Pizza';  
                foodDetail.linkImageURL = 'https://www.publicdomainpictures.net/pictures/240000/velka/pizza-1508086895mrm.jpg';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'Our pizza is made with the most flavorful tomato sauce and fresh cheese so that you can indulge all of your senses.';  
            } else if (foodName.contains('pasta')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/pasta';  
                foodDetail.linkTitle = 'Tasty Pasta';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1606761568499-5ddd45e43b32';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'Our pasta is topped with the most flavorful tomato sauce and fresh cheese so that you can indulge all of your senses.';  
            } else if (foodName.contains('tiramisu')) {  
                foodDetail.linkURL = 'https://tastesbetterfromscratch.com/easy-tiramisu/';  
                foodDetail.linkTitle = 'Classic Tiramisu';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1571877227200-a0d98ea607e9';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'Our tiramisu is made with the freshest ingredients so that you can indulge all of your senses.';  
            } else if (foodName.contains('tacos')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/tacos';  
                foodDetail.linkTitle = 'Authentic Mexican Tacos';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1551504734-5ee1c4a127da';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'Our tacos are made with the freshest ingredients so that you can indulge all of your senses.';  
            } else if (foodName.contains('quesadilla')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/quesadilla';  
                foodDetail.linkTitle = 'Cheesy Quesadilla';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1613952273499-5de42c1789c7';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('nachos')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/nachos';  
                foodDetail.linkTitle = 'Loaded Nachos';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1606755962773-b35f5d518c46';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('croissant')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/croissant';  
                foodDetail.linkTitle = 'Fresh Croissant';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1587049352907-23d8ff0ceac3';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('ratatouille')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/ratatouille';  
                foodDetail.linkTitle = 'Traditional Ratatouille';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1633527076476-f847fc6d16a2';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('creme brulee')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/creme-brulee';  
                foodDetail.linkTitle = 'French Crème Brûlée';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1609767400465-45e06f28a680';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('sushi')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/sushi';  
                foodDetail.linkTitle = 'Japanese Sushi';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1589308078050-cf38fe054d63';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('ramen')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/ramen';  
                foodDetail.linkTitle = 'Delicious Ramen';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1602334872613-3ab02f3c95a7';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('tempura')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/tempura';  
                foodDetail.linkTitle = 'Crispy Tempura';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1571771439241-89b31f5092c7';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('dumplings')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/dumplings';  
                foodDetail.linkTitle = 'Chinese Dumplings';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1617196036851-20ce58a15b1b';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('peking duck')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/peking-duck';  
                foodDetail.linkTitle = 'Peking Duck';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1643989946129-73e3a872ad80';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('spring rolls')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/spring-rolls';  
                foodDetail.linkTitle = 'Fresh Spring Rolls';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1604328698692-80d9b81baf4d';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('burger')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/burger';  
                foodDetail.linkTitle = 'Classic Burger';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1551782450-a2132b4ba21d';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('hot dog')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/hot-dog';  
                foodDetail.linkTitle = 'Grilled Hot Dog';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1621248313959-d6c0e480c54e';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else if (foodName.contains('apple pie')) {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/apple-pie';  
                foodDetail.linkTitle = 'Homemade Apple Pie';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1606760225157-145fe46c0b7f';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            } else {  
                foodDetail.linkURL = 'https://www.foodwebsite.com/food';  
                foodDetail.linkTitle = 'Unknown Food';  
                foodDetail.linkImageURL = 'https://images.unsplash.com/photo-1606851093480-b24197b5fd6a';  
                foodDetail.linkImageMimeType = 'image/jpeg';  
                foodDetail.linkDescriptionText = 'All of our food is delicious.';  
            }  
  
            response.foodDetails.add(foodDetail);  
            responses.add(response);  
        }  
  
        return responses;  
    }  
  
    // Request Wrapper Class  
    public class FoodDetailRequest {  
        @InvocableVariable(label='Food Name' description='The name of the food item' required=true)  
        public String foodName;  
    }  
  
    // Food detail structure  
    public class FoodDetail {   
        public String linkURL;  
        public String linkTitle;  
        public String linkImageURL;  
        public String linkImageMimeType;  
        public String linkDescriptionText;  
    }  
  
    // Response Wrapper Class  
    public class FoodDetailResponse {  
        @InvocableVariable(label='Food Details' description='Shows details, image, and link for the selected food' required=true)  
        public List<FoodDetail> foodDetails;  
  
        public FoodDetailResponse() {  
            this.foodDetails = new List<FoodDetail>();  
        }  
    }  
}
```

What’s important here is the **data structure**, as shown below.  
You don’t need to use these exact names, but it’s recommended to choose clear and descriptive names so that the agent can understand them easily.

- **name** (String)  
   A label name for a product or similar item
- **imageUrl** (String)  
   An image URL for a product or similar item
- **linkUrl** (String)  
   A link URL for a product or similar item
- **description** (String) *(\*optional)*  
   Descriptive text for a product or similar item
- **mimeType** (String) *(\*optional)*  
   A string that specifies the MIME type of the image

> *Specifying the MIME type is not mandatory, but from a performance perspective, it is recommended because it can improve client-side rendering and processing efficiency.*

**MIME Types**

- `image/apng`: Animated Portable Network Graphics (APNG)
- `image/avif`: AV1 Image File Format (AVIF)
- `image/gif`: Graphics Interchange Format (GIF)
- `image/jpeg`: Joint Photographic Experts Group image (JPEG)
- `image/png`: Portable Network Graphics (PNG)
- `image/svg+xml`: Scalable Vector Graphics (SVG)
- `image/webp`: Web Picture format (WEBP)

## 2. Grant Access to the Apex Class

Next, grant access to this Apex class to the Service Agent user.

> ***Important:*** *Without this access, the agent cannot respond.*

1. Create a new permission set.

- **Permission Set Name:** Agent Apex Actions (Custom)

2. Select **Apex Class Access**.

3. Select the **GetFoodDetailsInvocable** you created this time and save.

4. After creation, be sure to **assign** it to the **Service Agent User**.

## 3. Configure Trusted URLs

[With a new feature in Winter ’26](https://help.salesforce.com/s/articleView?language=en_US&id=release-notes.rn_einstein_agentforce_urls.htm&release=258&type=5),  
links that are not registered in the **Trusted URL list** are blocked in agent conversations.

> ***Note:*** *Unapproved URLs are replaced with* `URL_Redacted`*.*

1. From Setup, open **Trusted URLs**.

2. This time, since “Classic Tiramisu” is used for the choice selection, register only the following two entries. You can add other URLs as needed.

**For link URLs**

- API Name: tastesbetterfromscratch
- URL: https://tastesbetterfromscratch.com

**For image URLs**

- API Name: unsplash
- URL: https://images.unsplash.com

## Service Agent Configuration

## 1. Create a Topic

1. Create a new topic.

2. Enter the following to get started.

`This topic provides the user a list of food options and details.`

3. Edit the topic details as follows.

**Classification Description**

- This topic provides the user a list of food options and details. For example, use this topic when the user says: “What’s on the menu?”

**Scope**

- Your job is only to provide food options and details.

**Instructions (3 items)**

- Use Get\_Food\_Details action to get food options and details.
- When the user says: “What’s on the menu?”, always give a list of food options. For example, Classic Tiramisu, Homemade Apple Pie, and Delicious Ramen. Then the user is expected to select a food option. Using the food option name selected by user, pass the name to the Get\_Food\_Details action to get details about the item.
- When user selects a food option, use the Get\_Food\_Details action to give the user the link and image for the food option. For example, if user selects Delicious Ramen, then send Delicious Ramen as input to the Get\_Food\_Details action.

4. Do not add an action and click Finish.

## 2. Create an Action

1. Select the topic you created.

2. Open **Actions for this topic**.

3. Click **Create New Action**.

4. Select the following.

- Reference Action Type: **Apex**
- Reference Action Category: **Invocable Method**

5. Select **Get Food Details** as the reference action.

6. In **Agent Action Configuration**, enter the following and save.

**Agent Action Instructions**

- Returns linkURL, linkTitle, image linkURL, image MIME Type, and description text for a given food name

**Loading Text**

- Getting food details…

**Food Name Instructions**

- The name of the food item  
   ※ Check **Require input** only

**Food Details Instructions**

- Shows details, image, and link for the selected food  
   ※ Check **Show in conversation** only

## Operation Check

Let’s check the actual behavior.

## ① Adaptive Response Formats: Disabled

1. First, select **Connections** from the menu and open **Messaging**.

2. Set **Adaptive Response Formats** to **Disabled**.

3. Next, activate the agent.

4. Launch the Service Agent and ask, “What’s on the menu?”

![]()

5. Since the Adaptive Response Formats is disabled, the food options are displayed in text format, and the user must respond via text input.

Here, enter **Classic Tiramisu** and send.

![]()

6. The following is displayed.

![]()

Even in this case, images are displayed, so it does not look bad. However, the interaction remains a **traditional text-based experience**.

## ② Adaptive Response Formats: Enabled

1. Next, return to **Connections** in Agent Builder, enable **Adaptive Response Formats**, and confirm.

2. Ask “What’s on the menu?” in the same way as before.

![]()

3. This time, the menu is displayed in a button format.

![]()

The major advantage of this display format is that the user does not need to enter text. By simply clicking a button, the selection is automatically entered and sent.

4. Next, the following screen is displayed.

![]()

This is a **Rich Link Response**, which displays a web page link combining a text title and an image.

Compared to before, the images are not unnecessarily large, and the link is easier to click as a URL. Success.

## Additional Notes

This Adaptive Response Formats can also be used in external messaging channels such as **LINE Channel**.

## Conclusion

Although the Adaptive Response Formats does not offer as much flexibility as Custom Lightning Types using LWC, its major appeal is that it can enrich the conversational experience **without requiring frontend development skills**.

On the other hand, it is not a feature that should always be enabled. For example:

- When you want to prioritize simple, text-centered responses
- When images and links are not sufficiently prepared

in such cases, deliberately disabling it may result in a more natural appearance and user experience.

As shown in this example, for scenarios where:

- You want to present choices to users
- You want to guide users intuitively with images and links

the Adaptive Response Formats is a very good fit, and it has been confirmed that **UX can be greatly improved simply by switching the setting**.

It is recommended to start with a simple Apex implementation and then, as needed, gradually switch from **Adaptive Response Formats → Custom Lightning Types**.

Please try using it in real use cases.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
