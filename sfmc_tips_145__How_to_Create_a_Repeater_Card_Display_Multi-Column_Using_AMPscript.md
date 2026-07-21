# SFMC Tips #145 : How to Create a “Repeater” Card Display (Multi-Column) Using AMPscript

**Source:** https://medium.com/@marketingcloudtips/how-to-create-a-repeater-card-display-multi-column-using-ampscript-6d24e6f0762a

---

# SFMC Tips #145 : How to Create a “Repeater” Card Display (Multi-Column) Using AMPscript

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6d24e6f0762a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6d24e6f0762a---------------------------------------)

7 min read

·

Jun 30, 2025

--

Photo by [Cleyton Ewerton](https://unsplash.com/@cleytonewerton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I explained how to create a “repeater” list display (single-column) using AMPscript.

[## SFMC Tips #144 : How to Create a “Repeater” List Display (Single-Column) Using AMPscript

### With the release of the “Repeater” component in the Summer ’25 update for Marketing Cloud Next (Marketing Cloud Growth…

medium.com](/@marketingcloudtips/how-to-create-a-repeater-list-display-single-column-using-ampscript-750b4fd466de?source=post_page-----6d24e6f0762a---------------------------------------)

This time, I will demonstrate how to use AMPscript to create a “repeater” card display with two columns, and how to modify the script for a three-column layout.

## Steps to Create a Ranking List Using AMPscript

The final goal is to create an email that includes a product ranking list, as shown below. The left side features a two-column layout, while the right side demonstrates a three-column layout.

### Step 1: Preparing the Data

First, import the CSV file containing the ranking information into a data extension. Typically, this data is auto-generated within Marketing Cloud Engagement or directly integrated from an external system. For this example, however, I will manually import the data.

![]()

I’ll name the data extension that stores the ranking information **“RankingDE”**, which will be referenced later in the AMPscript code.

The data extension will look like this after importing the data:

![]()

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

**Utilizing a Pre-existing Single-column Layout**  
 In the email canvas, start with the existing “single-column layout” and make use of it for this implementation.

**Pro Tips:** Leveraging layouts is key. A layout allows you to manage multiple components as a single referenced content block, making it more efficient and easier to handle than creating multiple individual referenced content blocks.

**Design and Polish One Ranking Item**  
 Drag and drop the layout into the email canvas, then design and finalize the appearance of one ranking item. Since this single item will be displayed repeatedly in a loop, pay extra attention to its details.

**Dynamically Replace Information Using AMPscript**  
Use the AMPscript examples below to dynamically update the design you created:

**1. Image URL:**  
Replace the image source with: `%%=Field(@row,'ImageURL')=%%`  
Set the width to 100%.

![]()

**2. Link URL:**  
Use the following format: `%%=RedirectTo(Field(@row,'LinkURL'))=%%`. Note the use of `RedirectTo` to handle navigation links.

**3. Text Fields:**  
Replace text using `%%=Field(@row,'[FieldName]')=%%` (For example, Rank, Artist, Title, etc., in this case). To maintain consistent styles, work in the HTML Code Editor. However, for inserting URL links, use the WYSIWYG Editor.

**4. Price Display:**  
To format numbers with commas for every three digits, use the following:  
`%%=FormatNumber(Field(@row,'Price'),"N0")=%%`

*\*You need to adjust the display of this amount to match the format used in your country.*

**Save the Layout as a Template**  
At this stage, the preview screen may appear distorted — this is normal. Once the layout is finalized, save it as a template by clicking the save button in the bottom left corner.

**Retrieve the Content Block ID**  
After saving the template, you’ll be able to obtain the Content Block ID.

**Reference the Content Block Using its ID**  
Use this Content Block ID in the following format to reference it dynamically in AMPscript: `%%=ContentBlockById(44244735)=%%`

## AMPscript Loop Sample: 2-Column Display

To create a dynamic 2-column layout, use the following code to fetch data from a data extension and loop through it for rendering.

### 2-Column Display Code

```
<table width="100%">  
  <tr>  
    %%[   
      VAR @lookup, @count, @row, @totalItems, @extraTd  
      SET @lookup = LookupOrderedRows(  
        'RankingDE',   
        6,   
        'Rank asc',   
        'Genre', FavoriteGenre  
      )  
      SET @totalItems = RowCount(@lookup)  
  
      IF @totalItems > 0 THEN  
        FOR @count = 1 TO @totalItems DO   
          SET @row = Row(@lookup, @count)  
    ]%%  
  
    <td class="" style="width: 48%; padding-right: 10px; padding-left: 10px;" valign="top">  
  
  
    <!--- Insert reference content here --->  
    %%=ContentBlockById(44244735)=%%  
  
  
    </td>  
  
    %%[   
          IF Mod(@count, 2) == 0 THEN   
            OUTPUT(CONCAT("</tr><tr>"))   
          ENDIF  
        NEXT @count  
  
        IF @totalItems < 2 THEN  
          SET @extraTd = 2 - @totalItems  
          FOR @i = 1 TO @extraTd DO  
            OUTPUT(CONCAT("<td style='width: 48%;'></td>"))  
          NEXT @i  
        ENDIF  
      ENDIF   
    ]%%  
  </tr>  
</table>
```

### How It Works

By repeating `%%=ContentBlockById(44244735)=%%` within the loop, the ranking list is dynamically constructed and displayed in a two-column format.

### Editable Sections

1. `'RankingDE'`: The name of the data extension you are referencing.
2. `6`: The number of rows to display in the email.
3. `'Rank asc'`: Sorting order. Use `'asc'` for ascending or `'desc'` for descending.
4. `'Genre', FavoriteGenre`: Matching criteria. Example: `'Rock' = 'Rock'`.
5. `%%=ContentBlockById(44244735)=%%`: Replace with the ID of the template you want to display.

Other parts of the code usually do not require modification.

**Note:** Avoid using single quotes (`' '`) around `FavoriteGenre`. Using quotes will treat it as a literal value (`'FavoriteGenre'`), rather than the field value.

### Implementation Example

Add the AMPscript code to an **HTML block** in the email editor.

Add a `FavoriteGenre` field to your **sendable data extension**. Use this field to match with the `Genre` field in `RankingDE`. (Example: `'Rock' = 'Rock'`, `'Jazz' = 'Jazz'`).

Preview the email. The dynamic ranking list will display based on the value of `FavoriteGenre`:

**If** `FavoriteGenre` **is** `Rock`**:**

![]()

**If** `FavoriteGenre` **is** `Jazz`**:**

Success! While I won’t cover this here, you should also verify that link URLs redirect correctly. If links are not redirecting, ensure that they include the `RedirectTo` parameter.

## AMPscript Loop Sample: 3-Column Display

For displaying items in three columns, the following code can be used to fetch and render the content dynamically.

### 3-Column Display Code

```
<table width="100%">  
  <tr>  
    %%[   
      VAR @lookup, @count, @row, @totalItems, @extraTd  
      SET @lookup = LookupOrderedRows(  
        'RankingDE',   
        6,   
        'Rank asc',   
        'Genre', FavoriteGenre  
      )  
      SET @totalItems = RowCount(@lookup)  
  
      IF @totalItems > 0 THEN  
        FOR @count = 1 TO @totalItems DO   
          SET @row = Row(@lookup, @count)  
    ]%%  
  
    <td class="" style="width: 32%; padding-right: 3px; padding-left: 3px;" valign="top">  
  
  
    <!--- Insert reference content here --->  
    %%=ContentBlockById(44244735)=%%  
  
  
    </td>  
  
    %%[   
          IF Mod(@count, 3) == 0 THEN   
            OUTPUT(CONCAT("</tr><tr>"))   
          ENDIF  
        NEXT @count  
  
        IF @totalItems < 3 THEN  
          SET @extraTd = 3 - @totalItems  
          FOR @i = 1 TO @extraTd DO  
            OUTPUT(CONCAT("<td style='width: 32%;'></td>"))  
          NEXT @i  
        ENDIF  
      ENDIF   
    ]%%  
  </tr>  
</table>
```

### Preview and Results

After implementing this code and previewing your email, you should see a dynamic ranking list displayed as follows:

**If** `FavoriteGenre` **is** `Rock`**:**

![]()

**If** `FavoriteGenre` **is** `Jazz`**:**

![]()

Success!

## Conclusion

In the previous article, I introduced both “list display” and “card display”, and the fundamental implementation methods remain the same for both. However, in terms of ease of looping, “list display” is significantly simpler. On the other hand, “card display” requires slightly more complex handling, especially when dealing with scenarios like a single item or missing items in a row. This example has been designed with those considerations in mind.

Additionally, in this “card display” example, the image size is set simply to `width:100%`. While this works well for square images, it may cause layout issues if the images have other aspect ratios. Please be mindful of this when working with non-square images.

Finally, it’s important to note that content referenced by `ContentBlockById` is cached once a journey is activated and emails are sent. Even if the referenced content is updated, the cached version will not automatically reflect those changes in emails already queued or sent. For a technique to update such content, please refer to the article linked below.

[## SFMC Tips #74 : How to Update Content Referenced by ContentBlockById

### In Salesforce Marketing Cloud email creation, reusable content blocks are often called using AMPscript functions such…

medium.com](/@marketingcloudtips/how-to-update-content-referenced-by-contentblockbyid-c56741e90aa5?source=post_page-----6d24e6f0762a---------------------------------------)

That’s all for now — thank you for reading! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
