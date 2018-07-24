---

copyright:
  years: 2018
lastupdated: "2018-07-24"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Archiving objects

Cloud Object Storage Archive is our lowest cost option for data that is rarely accessed. Archive works with our existing storage class tiers, enabling you to reduce storage costs even further by storing data offline with our lowest priced storage. You can leverage our on-line cold vault option or transition data from any of storage tiers to long term offline archive.

To access the archive storage tier, we provide a web user interface, REST API, AWS S3 API, IBM object storage SDK, and a number of other tools to  integrate with IBM object storage. With the help of these interfaces you can create a bucket, define an Archive policy for the bucket, upload new objects, restore, delete and overwrite any object in any bucket.

## Store an object with an archive policy

Objects are stored in buckets and each bucket is a container for a collection of objects. You organize stored objects in a storage tier class. You can create a unique Archive policy (associated with each bucket) for transition of stored objects from the current storage tier to archive, based on the age of the object. An Archive policy for the bucket can be applied with any Cloud Object Storage tier class (Standard, Vault, Cold Vault,and Flex). You can use the same operations across all the storage tiers and utilize archive policies against their objects. There is no limit to how many objects you can store in each bucket.

A new Archive policy can be created for an existing or a new bucket at any time in any storage tier class. Similarly, an existing Archive policy associated with a bucket can be modified/disabled at any time. For any Archive policy changes on a bucket, only new objects uploaded to the bucket are affected by the change in policy (with no impact to the existing objects in the bucket).

Query archived data

Use IBM SQL Query to quickly analyze data in Cloud Object Storage. No Extract Transform Load (ETL). 

## Restoring an object

In order to read objects stored in the Archive tier, the objects must first be restored to the original storage tier from where the object was archived. This object restoration process can take up to 15 hours. An archived objecthas the following sub-states:

* Archived: The object is moved from its originating online storage tier (Standard, Vault, Cold Vault, Flex) to offline Archive tier based on the effective Archive policy of the bucket.

* Restored: A copy of the archived object is restored in the originating storage tier for a specified amount of time. At the end of this specified period, the copy of the object will be deleted from the storage tier it was restored to, while maintaining the archived copy in the archive tier.

* Restoring: A restoring object is in the process of generating a copy from the archived state to the original storage tier where it was last created.

## Deleting an archived object

There is no deletion penalty for objects deleted from the four active storage tiers (Standard, Vault, Cold Vault or Flex) or from the archive tier. 