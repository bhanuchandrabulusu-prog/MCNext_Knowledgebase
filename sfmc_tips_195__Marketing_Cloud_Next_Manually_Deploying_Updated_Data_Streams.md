# SFMC Tips #195 : Marketing Cloud Next: Manually Deploying Updated Data Streams

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-manually-deploying-updated-data-streams-8655b4a56296

---

# SFMC Tips #195 : Marketing Cloud Next: Manually Deploying Updated Data Streams

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8655b4a56296---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8655b4a56296---------------------------------------)

3 min read

·

Oct 18, 2025

--

Photo by [COSMOH](https://unsplash.com/@cosmoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When you install a **Data Kit** from the Marketing Cloud setup screen in **Marketing Cloud Next Growth & Advanced Edition**, objects and fields used to store marketing data are automatically added — you may already be somewhat familiar with this.

By deploying these data sets as **data streams**, the captured information becomes available for use across marketing tools and processes.

In most cases, the required data streams are deployed automatically. However, some data streams must be **manually deployed or updated** by a user with **Data Cloud Architect** permissions. Be sure not to overlook these manual updates.

> ***Note:*** *Even for manually deployed items, the* ***data stream names, fields, and categories*** *are predefined by the package and* ***cannot be modified****.*

### **Steps for Manual Deployment**

1. Go to **Data Streams** and click **New**.

2. Select **Installed Data Kits & Packages**, then click **Next**.

3. Choose the **Data Space** you want to use, and open the **Installed Packages** tab.

4. From the list of displayed **Data Streams**, select one item at a time using the radio button, then click **Next**. (The displayed names are **API names**.)   
⚠️ You cannot deploy multiple data streams at once.

5. The next screen is the **Review Screen**. Simply click **Next** to proceed.

6. On the following screen, review the details and click **Deploy**.

7. Once deployment is complete, any data stream that requires mapping to a **DMO (Data Model Object)** will be **automatically mapped**. Data streams that stop at the **DLO (Data Lake Object)** level and do not require DMO mapping (e.g., audit data) will not have any mapping.

8. Repeat this same process for all data streams until every one of them is deployed.

## Verifying Deployment Completion

9. After deployment, the deployed data streams will disappear from the package list. Once the list is completely empty, it indicates that **all updated data streams have been successfully deployed**.

## Conclusion

The manual deployment process described here typically occurs **after each of the three major annual releases**, when new **Marketing Data Kits** are installed.

Whenever you introduce a new Data Kit, be sure to follow these steps to complete the manual deployment.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
