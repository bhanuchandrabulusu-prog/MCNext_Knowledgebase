# SFMC Tips #43 : Fine-tuning Permissions for Marketing Cloud SFTP Users

**Source:** https://medium.com/@marketingcloudtips/fine-tuning-permissions-for-marketing-cloud-sftp-users-81579b56d72a

---

# SFMC Tips #43 : Fine-tuning Permissions for Marketing Cloud SFTP Users

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--81579b56d72a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--81579b56d72a---------------------------------------)

2 min read

·

May 31, 2024

--

Photo by [Jason Rosewell](https://unsplash.com/@jasonrosewell?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Currently, you can create up to 10 SFTP users in Marketing Cloud. **With the new Summer ’24 release, we are enhancing security by allowing various levels of access permissions for these SFTP users**.

*Note: These permissions are for SFTP users,* ***not individual Marketing Cloud users****.*

With this update, **you can assign specific access rights — viewing, editing, downloading, and uploading — at each top-level directory (down to subdirectories) for each SFTP user**.

You can also select a “home directory” as the default for each SFTP user. This means **each SFTP user will have access only to the selected directory and its subdirectories**.

*Note: Directories above the selected “home directory” will not be visible.*

*Release Timing: This feature is being rolled out gradually from May 2024, ahead of the Summer ’24 release period.*

I’ve already tested this feature, and **I can confirm that it prevents downloading files from SFTP as expected**. When setting a lower-level directory as the home directory, **higher-level directories are no longer visible**. I wanted to share this update with you.

## Conclusion

The existing features like the **“IP Allowlist”** setting and **“public key authentication for login”** will continue to be strong allies in ensuring the security of SFTP.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
