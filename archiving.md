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


# Archiving Data

Cloud Object Storage Archive is our [lowest cost option](
https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage) option for data that is rarely accessed. Archive works with our existing storage class tiers. You can leverage our on-line cold vault option or transition data from any of the storage tiers to long term offline archive.

You can archive objects using web console, REST API, and 3rd party tools that are integrated with Cloud Object Storage. 


## Add and manage Archive policy on a bucket

A new archive policy can be added to a new bucket when you are creating it or on an existing bucket at any time for any storage tier class (Standard, Vault, Cold Vault and Flex). An existing archive policy on a bucket can be updated at any time. Keep in mind, the newly added archive policy or modified policy applies to the new objects uploaded, does not affect the existing objects.


To immediately archive new objects uploaded on a bucket, enter 0 days on the archive policy.
{:tip}

You can enable/disable the archive policy on a bucket at any time. This affects the newly uploaded objects only.


## Restore an archived object

In order to access an archived object, you must restore it to the original storage tier. The restoration process can take up to 15 hours. Once the object is restored, a copy of the archived object is available for you to access. When restoring an object, you can specify number of days you want the object to be available. At the end of specified period, the restored copy is deleted.

An archived object can be in sub-states below:

* Archived: The object in archived state has been moved from its online storage tier (Standard, Vault, Cold Vault, Flex) to offline Archive tier based on the Archive policy on the bucket.

* Restoring: The object in restoring state is in the process of generating a copy from the archived state to the online storage tier.

* Restored: The object in restored state is when a copy of the archived object is restored to the online storage tier for a specified amount of time. At the end of this specified period, the copy of the object is deleted, while maintaining the archived object.
