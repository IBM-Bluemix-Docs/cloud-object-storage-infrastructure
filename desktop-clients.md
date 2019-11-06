---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2018-08-22"

subcollection: cloud-object-storage-infrastructure

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Using a desktop client

GUI tools exist for accessing S3 API compatible {{site.data.keyword.cos_short}} and for basic tasks, such as configuring routine backup or shared hosting for large files.

## Cyberduck

Cyberduck is a popular, open source, and easy to use FTP client that is also capable of calculating the correct authorization signatures that are needed to connect to {{site.data.keyword.cos_full_notm}}.  Cyberduck can be downloaded from [cyberduck.io ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cyberduck.io/).

To use Cyberduck to create a connection to {{site.data.keyword.cos_full_notm}} and synchronize a folder of local files to a bucket, follow these steps.

 1. Download, install, and start Cyberduck.
 2. The main window of the application opens, where you can create a connection to {{site.data.keyword.cos_full_notm}}. Click **Open Connection** to configure a connection to {{site.data.keyword.cos_full_notm}}.
 3. A new window opens. From the menu, select **S3 storage**. Enter information into the following fields, and then click Connect.
   * Server: enter the nearest endpoint of {{site.data.keyword.cos_full_notm}}. For more information, see [available regions and endpoints](/docs/infrastructure/cloud-object-storage-infrastructure?topic=cloud-object-storage-infrastructure-select-regions-and-endpoints).
   * Access Key ID
   * Secret Access Key
   
   You can obtain your Access Key ID and Secret Access Key from the [IBM Cloud Console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/) through **Classic Infrastructure** > **Storage** > **Object Storage**. Click the account name. In the account details page, click **Access & Permissions** to see your credentials and access keys.
   {:tip}

 4. Cyberduck takes you to the root of the account where buckets can be created. Right-click within the main panel and select **New Folder**. (The application deals with many transfer protocols where Folder is the more common container construct). Enter the bucket name and then click **Create**.
 5. After the bucket is created, double-click the bucket to view it. Within the bucket you can perform various functions such as upload files to the bucket, list bucket contents, download objects from the bucket, synchronize local files to a bucket, synchronize objects to another bucket, or create an archive of a bucket.
 6. Right-click within the bucket and select **Synchronize**. A pop-up panel opens where you can browse to the folder that you want to synchronize to the bucket. Select the folder and click Choose.
 7. After you select the folder, a new pop-up panel opens. Here, a drop-down menu is available where you select the synchronization operation with the bucket. Three possible synchronize options are available from the menu.
   * Download - This option downloads changed and missing objects from the bucket.
   * Upload - This option uploads changed and missing files to the bucket.
   * Mirror - This option performs both download and upload operations, ensuring that all new and updated files and objects are synchronized between the local folder and the bucket.

 8. Another window opens to show active and historical transfer requests. After the synchronization request is complete, the main window performs a list operation on the bucket to reflect updated content in the bucket.

## Cloudberry

Cloudberry is a flexible backup utility that allows users to back up some or all of a local file system to an S3 API compatible {{site.data.keyword.cos_short}} system. It can be configured to be run either manually or scheduled based on need, and can back up different directories to different buckets if needed. Cloudberry can be downloaded from [cloudberrylab.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.cloudberrylab.com/).

When you configure Cloudberry, select `S3 Compatible` from the list of options.
{:tip}

The current release of the Cloudberry Client for Windows uses TLSv1.0 for establishing secure data transmission over the public Internet. IBM Cloud requires the more modern TLSv1.1 or TLSv1.2 to establish a secure connection. Connections from the Cloudberry Client for Windows fail unless the `Use SSL` box is left **unchecked** during configuration.
{:tip}
