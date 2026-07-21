# SFMC Tips #33 : How to Set Layout Within Layout in Content Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-set-layout-within-layout-in-content-builder-21720f80a1d1

---

# SFMC Tips #33 : How to Set Layout Within Layout in Content Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--21720f80a1d1---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--21720f80a1d1---------------------------------------)

4 min read

·

Mar 13, 2024

--

Photo by [Kees Streefkerk](https://unsplash.com/@kees_streefkerk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Have you ever wished for more freedom to design your emails beyond the standard layouts offered by Content Builder?

This time, we desire a design for our email as follows:

For desktop view, we want a display with 3-column like this:

![]()

However, for mobile view, we’d like to have 2-column displayed on the top and 1-column at the bottom like this:

![]()

Such a standard layout isn’t available in Content Builder.

You might think simply putting one layout inside another would suffice. However, unfortunately, using drag-and-drop within Content Builder’s interface, it’s not possible to set another layout within a layout.

So, what’s the solution?

**This is resolved by utilizing the “%%=ContentBlockById()=%%” function in AMPscript**.

Let’s explain what this looks like.

Firstly, to implement this, you need to prepare the content for the “red” and “blue” nested content as a 2-column layout content block.

To create a 2-column layout content block beforehand, follow these steps in Content Builder. In this case, set the “red” and “blue” content to be 50% each and set Mobile column stacking to “none”.

![]()

*\*The layout automatically includes “Padding 10px.” If unnecessary, change it to “0 px”.*

After creating the layout with the above steps, open the layout’s properties and copy the value of “ID” from here. This will be the ID of your content block.

*\*You can also select the layout from the screen later using the “Browse” function without copying the layout’s “ID”.*

Next, in the email creation screen, place the 2-column layout as the larger nested side. Place the “green” content on the right side. Set the proportions as 50% each, but for Mobile column stacking, choose “left to right” as we want it stacked vertically.

Then, on the left side of the layout, place an HTML block. In this HTML block, insert the AMPscript “%%=ContentBlockById()=%%” with the ID of the layout you created earlier. If the ID is “8464929” in this case, it should be written as follows, **with quotation marks around the numbers**:

%%=ContentBlockById(“8464929”)=%%

That concludes the layout setup. Now, let’s quickly check it in **“Preview and Test”**.

In desktop view, it should appear as follows:

And in mobile view:

![]()

With this Tip, you can extend beyond what seems to be the limit of 5-column in the standard layout to possibilities like 6-column. To achieve this, arrange two sets of 3-column layouts side by side as follows.

![]()

*\*When using “Mobile column stacking”, it’s not possible to adjust the “top and bottom” spacing using the layout’s Spacing option. Therefore, please adjust the spacing within each content block contained within the layout.*

Feel free to make the most of it.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
