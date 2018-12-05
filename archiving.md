---

copyright:
  years: 2018
lastupdated: "2018-12-05"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Archiving data

{{site.data.keyword.cos_full}} Archive is our [lowest cost ![External link icon](../../icons/launch-glyph.svg "External link icon")](
https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage){:new_window} option for data that is rarely accessed. You can store data by transitioning from any of the storage tiers (Standard, Vault, Cold Vault and Flex) to long-term off-line archive or use the on-line Cold Vault option.

You can archive objects using the web console, REST API, and third-party tools that are integrated with {{site.data.keyword.cos_notm}}.

## Adding or managing an archive policy on a bucket

When you create or modify an archive policy for a bucket, consider the following:

* An archive policy can be added to a new or existing bucket at any time.
* An existing archive policy can be modified or disabled.
* A newly added or modified archive policy applies to new objects that are uploaded and does not affect existing objects.

To immediately archive new objects that are uploaded to a bucket, enter 0 days on the archive policy.
{:tip}

## Restore an archived object

To access an archived object, you must restore it to the original storage tier. When you restore an object, you can specify the number of days you want the object to be available. At the end of the specified period, the restored copy is deleted.

The restoration process can take up to 15 hours.
{:tip}

The archived object sub-states are:

* Archived - An object in the archived state has been moved from its online storage tier (Standard, Vault, Cold Vault and Flex) to the off-line archive tier based on the archive policy on the bucket.
* Restoring - An object in the restoring state is in the process of generating a copy from the archived state to its original on-line storage tier.
* Restored - An object in the restored state is a copy of the archived object that was restored to its original on-line storage tier for a specified amount of time. At the end of the period, the copy of the object is deleted, while maintaining the archived object.
