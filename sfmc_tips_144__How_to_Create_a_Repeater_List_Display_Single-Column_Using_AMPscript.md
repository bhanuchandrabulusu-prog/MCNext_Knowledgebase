# SFMC Tips #144 : How to Create a “Repeater” List Display (Single-Column) Using AMPscript

**Source:** https://medium.com/@marketingcloudtips/how-to-create-a-repeater-list-display-single-column-using-ampscript-750b4fd466de

---

# SFMC Tips #144 : How to Create a “Repeater” List Display (Single-Column) Using AMPscript

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--750b4fd466de---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--750b4fd466de---------------------------------------)

7 min read

·

Jun 26, 2025

--

Photo by [Jonathan Cooper](https://unsplash.com/@theshuttervision?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the release of the “Repeater” component in the Summer ’25 update for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), creating personalized “repeater” content has become significantly easier. For more details, please check the article linked below.

[## SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

### With the Summer ’25 release of Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Content Builder’s…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----750b4fd466de---------------------------------------)

On the other hand, in the traditional Marketing Cloud Engagement, achieving similar “repeater” content requires leveraging AMPscript.

In this article, I will introduce a method to create a single-column “repeater” list display using AMPscript loop techniques. This approach is based on my personal methods, so there may be room for discussion regarding more efficient or simpler alternatives. I hope this serves as a helpful reference for anyone facing similar challenges. If you already have other methods, feel free to compare them and adopt whichever works best for you.

## Steps to Create a Ranking List Using AMPscript

The ultimate goal of this guide is to create an email that includes a product ranking list, as shown below:

![]()

### Step 1: Preparing the Data

First, import the CSV file containing the ranking information into a data extension. Typically, this data is auto-generated within Marketing Cloud Engagement or directly integrated from an external system. For this example, however, I will manually import the data.

I’ll name the data extension that stores the ranking information **“RankingDE”**, which will be referenced later in the AMPscript code.

The data extension will look like this after importing the data:

The imported data extension contains the following fields, each serving a specific purpose:

- **Id**: Primary key
- **Rank**: Determines the order of the ranking
- **Genre**: Specifies the genre
- **Artist**, **Title**, **Price**: Product details
- **ImageURL**: URL for the product image
- **LinkURL**: URL for the product link

For the **Genre** field, the goal is to personalize the ranking based on the value in the **“FavoriteGenre”** field within the sendable data extension (e.g., Rock or Jazz).

### Practice Data

To practice, I’ve uploaded the sample CSV file used in this example. Feel free to edit it and use your own data. If you’d like to use the provided CSV file, set it up with the following configurations:

- **Rank** and **Price**: Number type (or Decimal type)
- All URL fields: Text type (2000 characters)

Click below to download the file:

![]()

<https://image.s12.sfmc-content.com/lib/fe2c11737164047d721379/m/1/RankingDE.xlsx>

### Step 2: Creating the Email Layout

In the email canvas, create a layout using the **“Image + Text”** structure. Position the image on the left side and the text on the right side, as shown below.

**Pro Tips:** Utilizing “layouts” is the key. Layouts allow you to group multiple components into a single reference content block, making it more efficient and easier to manage compared to preparing individual reference content blocks for each component.

Next, use AMPscript to dynamically replace the content in the layout as follows:

**1. Image URL:**  
 Replace the image source with: `%%=Field(@row,'ImageURL')=%%`  
 Set the width to 100%.

![]()

**2. Link URL:**  
 Use the following syntax for the link: `%%=RedirectTo(Field(@row,'LinkURL'))=%%`  
Note the use of `RedirectTo`, which ensures the link functions as a redirection URL.

**3. Text Fields:**  
 Replace text fields with: `%%=Field(@row,'[FieldName]')=%%`  
 (For example, Rank, Artist, Title, etc., in this case). To maintain the styles you’ve set up, work within the **HTML Code Editor**. However, use the **WYSIWYG Editor** for adding clickable URLs.

**4. Price Display:**  
 To display prices with commas as thousand separators, use the following syntax: `%%=FormatNumber(Field(@row,'Price'),"N0")=%%`

*\*You need to adjust the display of this amount to match the format used in your country.*

### Saving the Layout as a Template

After completing the layout, the preview may appear distorted. This is normal. Finalize the layout by saving it as a template using the save button at the bottom left of the screen.

Once saved, you will obtain a **Content Block ID** for the template.

Use this Content Block ID in the following format to reference it dynamically in AMPscript: `%%=ContentBlockById(43772515)=%%`

### AMPscript Sample for Loops

In this case, I will use the following code to retrieve data from a data extension and display it using a loop:

```
%%[  
    VAR @lookup, @count, @row  
    SET @lookup = lookuporderedrows(  
        'RankingDE',   
        5,   
        'Rank asc',   
        'Genre', FavoriteGenre  
    )  
    FOR @count = 1 TO rowcount(@lookup) DO  
        SET @row = row(@lookup, @count)  
]%%  
  
  
<!--- Insert reference content here --->  
%%=ContentBlockById(43772515)=%%  
  
  
%%[ NEXT @count ]%%
```

By looping through this `%%=ContentBlockById(43772515)=%%`, the dynamic ranking list will be constructed and displayed in the email.

### Explanation of Editable Sections

Here’s a breakdown of the parts you might need to adjust when using this code:

- `'RankingDE'`: The name of the data extension you are referencing.
- `5`: The number of rows to display in the email.
- `'Rank asc'`: Defines the sorting order. Specify `'asc'` for ascending or `'desc'` for descending.
- `'Genre', FavoriteGenre`: The matching criteria (e.g., Rock = Rock).
- `%%=ContentBlockById(43772515)=%%`: The ID of the content block you want to display.

The rest of the code does not need modification.

**Important Note**: Avoid enclosing `FavoriteGenre` in quotes (`' '`). Doing so will treat it as a fixed value of `'FavoriteGenre'`.

### Implementation Example

Place the AMPscript in an HTML block within the email editor.

Next, add a `FavoriteGenre` field to your sendable data extension. This field will be used to match with the `Genre` column in the `RankingDE`. For example, Rock = Rock or Jazz = Jazz.

Finally, use this sendable data extension to preview the email. You should see a dynamic ranking list like the examples below:

### When `FavoriteGenre` is Rock

![]()

### When `FavoriteGenre` is Jazz

![]()

Success! While I won’t cover this here, you should also verify that link URLs redirect correctly. If links are not redirecting, ensure that they include the `RedirectTo` parameter.

### Conclusion

What did you think?

By the way, content referenced using `ContentBlockById` is cached once the journey is activated and the email is sent. This means that even if you update the referenced content, the content being used in an active journey will not automatically reflect those changes. I’ve shared a technique to modify such cached content in the article linked below, so feel free to check it out as well.

[## SFMC Tips #74 : How to Update Content Referenced by ContentBlockById

### In Salesforce Marketing Cloud email creation, reusable content blocks are often called using AMPscript functions such…

medium.com](/@marketingcloudtips/how-to-update-content-referenced-by-contentblockbyid-c56741e90aa5?source=post_page-----750b4fd466de---------------------------------------)

Through the steps outlined in this article, I hope you’ve gained a clear understanding of how to replicate the functionality of the “Repeater” component in Marketing Cloud Next using AMPscript in Marketing Cloud Engagement.

In this example, I created a slightly more complex layout with images and text. However, in most cases, you’ll likely use a simpler setup, such as aligning banner images in a single column or listing news article text in a straightforward layout.

In the next article, I’ll focus on implementing a “Card Display” using AMPscript, introducing even more advanced techniques. Stay tuned!

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
