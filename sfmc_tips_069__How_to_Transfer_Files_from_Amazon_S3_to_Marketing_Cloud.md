# SFMC Tips #69 : How to Transfer Files from Amazon S3 to Marketing Cloud

**Source:** https://medium.com/@marketingcloudtips/how-to-transfer-files-from-amazon-s3-to-marketing-cloud-85f9af08b16f

---

# SFMC Tips #69 : How to Transfer Files from Amazon S3 to Marketing Cloud

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--85f9af08b16f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--85f9af08b16f---------------------------------------)

7 min read

·

Dec 19, 2024

--

Photo by [Kasra Askari](https://unsplash.com/@kasraskari?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud supports file transfers not only with SFTP but also with Amazon S3, Google Cloud Storage, and Microsoft Azure Blob Storage. These direct transfers are faster compared to file transfers using SFTP.

This time, we’ll dive into the method for file transfer using Amazon S3 as an example.

## ■ Basic AWS Setup

First, you need to create an AWS account. Please create an account via the following website:

[## Free Cloud Computing Services - AWS Free Tier

### Gain hands-on experience with the AWS platform, products, and services for free with the AWS Free Tier offerings…

aws.amazon.com](https://aws.amazon.com/free/?source=post_page-----85f9af08b16f---------------------------------------)

Amazon S3 uses a pay-as-you-go pricing model based on storage, data transfers, and the number of requests. However, **a free usage tier is available for one year**.

To allow Marketing Cloud to access Amazon S3, the following information is required. Let’s go through the steps to obtain it:

1. **Access Key**
2. **Secret Access Key**
3. **Bucket Name**
4. **Folder Name within the Bucket (optional)**

Once your account is created, you’ll arrive at the Amazon S3 console home.

## Step 1: Create an IAM User

First, create an IAM user, which is a user within the account for performing daily tasks. Enter “IAM” in the search bar at the top of the page and select IAM from the results.

This takes you to the IAM dashboard. You’ll notice that the current number of users is “0”. Click on this number.

Next, click the “Create User” button.

You’ll be taken to the screen where you can name the IAM user. Enter a name and click “Next”.

On the permissions screen, leave the settings as default for now and click “Next”. Permissions can be assigned later.

On the review screen, click “Create User” to proceed.

Your IAM user is now created. Next, create an Access Key and Secret Access Key. Click on the link for the newly created IAM user.

Click “Create Access Key”.

Choose “Third-party services” as the use case and click “Next”.

On the description tag screen, you can optionally enter details as needed. Once done, click the “Create Access Key” button.

The Access Key and Secret Access Key will now be displayed.

The Access Key will remain visible on the IAM user dashboard, but **the Secret Access Key is only displayed at this moment**. Be sure to record it securely.

Now, you have obtained:

1. **Access Key**
2. **Secret Access Key**

## Step 2: Configure Amazon S3

Amazon S3 (Amazon Simple Storage Service) is a storage service provided by Amazon.

To get started, access Amazon S3 by entering “S3” in the search bar at the top of the page and selecting S3 from the results.

On the next screen, create a new bucket. A bucket is like a container for uploading, downloading, and storing data.

First, name your bucket. Note that the naming rules are somewhat strict — existing names cannot be reused, **uppercase letters cannot be used**, and **underscores (\_) are not allowed**.

Most other settings can be left as default, but you can configure them as needed. Click “Create Bucket”.

Your bucket is now created. Note down the bucket name, as it will be required for Marketing Cloud setup.

3. **Bucket Name**

Next, create a folder within the bucket. Click the “Create Folder” button.

Enter a folder name. The naming rules differ from buckets, so uppercase letters and other characters are allowed. Once named, click “Create Folder”.

The folder is now created within the bucket. Note down the folder name as it will also be required for Marketing Cloud setup.

4. **Folder Name within the Bucket (optional)**

## Step 3: Upload a File to the Folder

Next, upload a CSV file to the folder you just created.

Click the “Add Files” button.

Select the CSV file and click “Upload”.

The CSV file has been successfully uploaded.

## Step 4: Grant Access to Amazon S3

Finally, assign access permissions for the IAM user to Amazon S3.

*Note: If permissions are not assigned, you’ll encounter a validation error during the “File Location” setup in Marketing Cloud.*

Open the IAM user you created earlier. At the top, there is an option to configure permission policies. Select “Add Permission”.

On the next screen, choose “Attach Policies Directly” on the right side. Search for “S3” and select “**AmazonS3FullAccess**”.

Click “Add Permission” to proceed.

This grants the IAM user full access to Amazon S3.

## ■ Marketing Cloud Setup

In Marketing Cloud, go to Setup and open “File Locations”. Create a new file location, enter a definition name, and select “Amazon Simple Storage Service” as the location type.

For authentication type, select “Access Key”. Enter the pre-noted “AWS Bucket Name”, “AWS Relative Path”, “Access Key ID”, and “Secret Access Key”. Also, specify the “Region Name”. After entering all details, validate the connection. If successful, save the setup.

For “AWS Relative Path”, **no “/” is required for folders directly under the bucket — simply enter the folder name**. For subfolders, **use a format like “File1/output”**.

*Note: Each time you edit the file location definition, you will need to re-enter the Secret Access Key.*

## Step 5: Import the File into a Data Extension

Now that the file location is set up, import the CSV file from Amazon S3 into a data extension. Start by creating an empty data extension, as shown below:

Next, in Automation Studio, configure an import activity. Select the previously created file location and specify the file naming pattern with the CSV file name stored in Amazon S3.

Once all settings for the import activity are complete, execute it once.

As shown below, the file has been successfully imported.

That’s it!

Through these steps, you should now have a clear understanding of the required configurations. I plan to write similar articles for Google Cloud Storage and Microsoft Azure Blob Storage in the future.

This concludes the tutorial.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)

By using the “**Trigger**” Starting Source in Automation Studio, you can configure a mechanism to start an automation when a file is dropped into an S3 bucket. This implementation is explained in an article by **Oscar McCall**, a Marketing Cloud Specialist and Cloud Architect. Please note that this process involves using AWS Lambda.

[## SFMC and AWS S3 (Cloud Storage Triggers Beta)

### For awhile SFMC has had the ability to ingest data from AWS S3 buckets into Data Extensions, however, there were…

oscarmccall.medium.com](https://oscarmccall.medium.com/sfmc-and-aws-s3-cloud-storage-triggers-beta-ff02f801a760?source=post_page-----85f9af08b16f---------------------------------------)
