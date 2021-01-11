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


# Storing and retrieving data
{: #iaas-data}

The user interface portal provides a high-level view of a storage account. It is possible to create buckets and upload objects through he portal, but typically most interaction with the object store is done through the API by a client application.

## Buckets
{: #iaas-buckets}

1. Click the Account Name in the accounts list to open the details page for that account.
2. The details page shows the following information on the header bar.
   * Name of the account that is currently being viewed
   * The current region that is being viewed
   * The total capacity usage in the current billing cycle
   * The total bandwidth usage in the current billing cycle
3. The page also shows the list of buckets that are present in the account.
4. A new bucket can be added by clicking on the **+** button at the right of the first row.
5. The new bucket name can be entered and the new bucket added, by clicking the **Add** button.
   Bucket names must be DNS-compliant. Names must be 3 - 63 characters long, must be made of lowercase letters, numbers, and dashes, must be globally unique, and cannot appear to be an IP address. A common approach to ensuring uniqueness is to append a UUID or other distinctive suffix to bucket names.
   {:tip}

6. A bucket can be deleted, by clicking the red **-** button to the extreme right of the bucket name. This action opens a confirmation window.
   Only empty buckets can be deleted**. Attempting to delete a non-empty bucket results in an error.
   {:tip}

7. Click the **Delete** button to remove the bucket from the account.


## Objects
{: #iaas-objects}

1. The objects present within a bucket can be viewed, by clicking the bucket name on the buckets list.
2. The header is updated to include the following information.
  * Name of the account that is currently being viewed
  * The current region that is being viewed
  * The name of the bucket whose objects are currently displayed
  * The type of the bucket whose objects are currently displayed
3. Above the grid on the left, there is a link with the name of the bucket that is currently viewed. Click the link to show the list of buckets again.
4. The grid shows the list of objects in the bucket.
5. A new object can be added, by clicking the **+** button at the right of the first row.
6. The file can be selected from the file system, by clicking the **select** button and the new file can be uploaded by clicking the **Add** button.
   When you use the portal to add an object, file size is limited to 20 megabytes.
   All objects are limited to 5 TB when you use the API, including multipart uploads which are capped at 10-k parts of no larger than 5 GB each.
   {:tip}

7. An object can be deleted, by clicking on the red **-** button to the right of the object name. This action opens a confirmation window.
8. Click the **Delete** button to remove the object from the bucket.
