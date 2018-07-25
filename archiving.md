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


# Archiving data

{{site.data.keyword.cos_full}} Archive is our [lowest cost](
https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage) option for data that is rarely accessed. You can store the data by transitioning from any of the storage tiers (Standard, Vault, Cold Vault and Flex) to long-term offline archive or use online cold vault option. 

You can archive objects using web console, REST API, and 3rd party tools that are integrated with IBM Cloud Object Storage. 

## Add and manage archive policy on a bucket

A new archive policy can be added on a new bucket or on an existing bucket at any time. An existing archive policy can be modified or disabled at any time. Keep in mind, the newly added archive or modified policy applies to the new objects uploaded, does not affect existing objects.

To immediately archive new objects uploaded on a bucket, enter 0 days on the archive policy.
{:tip}

## Restore an archived object

In order to access an archived object, you must restore it to the original storage tier.  When restoring an object, you can specify the number of days you want the object to be available. At the end of the specified period, the restored copy will be deleted. The restoration process can take up to 15 hours.

An archived object can be in sub-states below:

* Archived: An object in the archived state has been moved from its online storage tier (Standard, Vault, Cold Vault and Flex) to offline archive tier based on the archive policy on the bucket.

* Restoring: An object in restoring state is in the process of generating a copy from the archived state to its original online storage tier.

* Restored: An object in the restored state is a copy of the archived object that has been restored to its original online storage tier for a specified amount of time. At the end of the period, the copy of the object will be deleted, while maintaining the archived object.
