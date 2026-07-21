# SFMC Tips #79 : How to Transfer Files from Google Cloud Storage to Marketing Cloud

**Source:** https://medium.com/@marketingcloudtips/how-to-transfer-files-from-google-cloud-storage-to-marketing-cloud-f2306d6434f8

---

# SFMC Tips #79 : How to Transfer Files from Google Cloud Storage to Marketing Cloud

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--f2306d6434f8---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--f2306d6434f8---------------------------------------)

7 min read

·

Feb 6, 2025

--

Photo by [Ameer Basheer](https://unsplash.com/@24ameer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I wrote step-by-step instructions on transferring files from Amazon S3 to Salesforce Marketing Cloud.

[## SFMC Tips #69 : How to Transfer Files from Amazon S3 to Marketing Cloud

### Salesforce Marketing Cloud supports file transfers not only with SFTP but also with Amazon S3, Google Cloud Storage…

medium.com](/@marketingcloudtips/how-to-transfer-files-from-amazon-s3-to-marketing-cloud-85f9af08b16f?source=post_page-----f2306d6434f8---------------------------------------)

This time, I will provide similar step-by-step instructions for transferring files from Google Cloud Storage to Salesforce Marketing Cloud.

## Basic Setup for Google Cloud Storage

First, you need to start with the Google Cloud products and services. Access the following site: <https://cloud.google.com/free>

Just like AWS, Google Cloud products and services offer a “free tier”. If you have a Google account and a Credit Card, you can start easily.

To access Google Cloud Storage from Marketing Cloud, you’ll need the following information. Let’s walk through the steps to obtain it:

### Required Information

1. Credential JSON file
2. Bucket name
3. Folder name within the bucket (optional)

**Note:** Unlike Amazon S3, which uses an Access Key and Secret Access Key for Credential, Google Cloud Storage requires a more secure **JSON file for Credential**. Keep this in mind.

Once the Google Cloud products and services are set up, you’ll be redirected to a page like the one below. Click the **Navigation Menu** in the top left corner.

From **IAM & Admin**, select **Service Accounts**.

Click **+ Create Service Account**.

Enter the **Service Account Name**. In this example, I used “SFMC\_service\_account”.

The **Service Account ID** will be auto-generated and can only include lowercase letters, numbers, and hyphens.

Optionally, you can add a description for the service account.

Then, click **Create and Continue**.

Next, select a **Role**. Choose **Storage Admin** from **Cloud Storage**.

**Important:** If you do not select “**Storage Admin**” as the role, an error will occur later during the “**Validation**” step in Marketing Cloud.

Click **Continue**.

For the final step, skip Step 3 and click **Done**.

Then, click the link for the created service account.

Go to the **Keys** tab.

From **Add Key**, click **Create New Key**.

Keep the **Key Type** as “JSON”, then click **Create**.

![]()

The JSON file will be downloaded to your local machine.

![]()

This downloaded file is your **Credential JSON file**.

### 💡Reference: For Data Cloud

In the case of Data Cloud, instead of an Credential JSON file, you use an **Access Key** and **Secret Key**.

**Note:** If you are using folders, be sure to end the folder path with a “/”.

You can generate the **Access Key** and **Secret Key** from the **Interoperability** tab under Google Cloud Storage settings by clicking **+ Create a Key for Another Service Account**.

The keys will be displayed as shown below. Note that the Secret Key will only be shown at this point, so make sure to take note of it. If you miss it, you’ll need to regenerate the key.

## Google Cloud Storage Bucket Setup

Next, use the search bar at the top of the page to search for **Buckets**.

Click **+ Create**.

Enter a name for the bucket, ensuring it is globally unique. Once you’ve entered the bucket name, leave the rest as default and click **Create** at the bottom of the page.

Click **Confirm**.

![]()

This creates the bucket. Take note of the **Bucket Name**, as you will need it for the Marketing Cloud setup.

### Optional: Creating a Folder Within the Bucket

You can create a folder within the bucket to store files. Click **Create Folder**.

**Note:** You can also store files directly in the bucket without creating a folder.

Choose a folder name and click **Create**. For simplicity, I named it “folder”.

![]()

The folder is now created within the bucket. Take note of the **Folder Name**, as you may need it for the Marketing Cloud setup.

Finally, upload the CSV file you want to import into the Data Extension to the created folder. Click on the folder.

Browse for the CSV file and click **Upload**.

For this example, I uploaded a file named **MasterSubscribers\_Import.csv**.

This completes the setup on the Google Cloud Storage side. Next, let’s proceed with the setup on the Marketing Cloud side.

## Setting Up Marketing Cloud

In Marketing Cloud, navigate to **Setup > File Locations** and create a new file location. Enter a definition name for the file location and select **Google Cloud Storage** as the location type.

Next, input the **Bucket Name** and **Relative Path** you noted earlier, and upload the **Credential File** (JSON).

When specifying the **Relative Path**, omit the leading `/` if the folder is directly under the bucket. Simply input the folder name (e.g., `folder`). For subfolders, use `/` to separate levels, like `File1/output`.

Once all fields are filled in, click **Validate** to ensure the connection is secure. If the validation succeeds, you’ll see a message like below. Click **Save** to complete the configuration.

## Importing CSV Files from Google Cloud Storage

With the file location set, let’s import a CSV file from the Google Cloud Storage bucket into a Data Extension. First, create an empty Data Extension like this:

Next, configure an **Import Activity** in Automation Studio. Select the file location you just created and specify the file naming pattern corresponding to the CSV file stored in the bucket.

Once the Import Activity setup is complete, run the activity.

As shown below, the file has been successfully imported into the Data Extension. Success!

## Final Thoughts

I hope this guide helped clarify the necessary steps to connect and transfer files from Google Cloud Storage to Marketing Cloud. By following this process, you should now understand the minimum requirements for setting up and importing files.

Having covered both Amazon S3 and Google Cloud Storage in this series, I plan to write a similar article for **Microsoft Azure Blob Storage** in the near future. Stay tuned!

Thank you for reading!!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
