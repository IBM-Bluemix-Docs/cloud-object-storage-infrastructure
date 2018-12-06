---

copyright:
  years: 2017
lastupdated: "2018-02-15"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# FAQ

## API Questions

**Are COS bucket names case-sensitive?**

Bucket names are required to be DNS addressable, and thus not case-sensitive.

**What is the maximum number of characters that can be used in an Object name?**

1024

## Offering Questions

**Do we offer a free tier option for {{site.data.keyword.cos_full_notm}}?**

Yes, use promo code `COSFREE` to obtain 25 GB of storage and a bunch of operations per month.

**Is there a 100-bucket limit to an account?  What happens if we need more?**

Yes, 100 is the current bucket limit. Generally, prefixes are a better way to group objects in a bucket, unless the data needs to be in a different region or storage class.  For example, to group patient records, you would use one prefix per patient. If this is not a workable solution, contact customer support.

**If I want to store my data in {{site.data.keyword.cos_full_notm}} Vault or Cold Vault, do I need to create another account?**

No, storage classes (and regions as well) are defined at the bucket level. Simply create a bucket that is set to the wanted storage class.

**When I create a bucket with the API, how do I set the storage class?**

The storage class (for example `us-flex`) is assigned to the `LocationConstraint` configuration variable for that bucket. This is because of a key difference between the was AWS S3 and {{site.data.keyword.cos_full_notm}} handle storage classes.  {{site.data.keyword.cos_full_notm}} sets storage classes at the bucket level, while AWS S3 assigns a storage class to an individual object.

**Can the storage class of a bucket be changed?  For example, if you have production data in 'standard', can we easily switch it to 'vault' for billing purposes if we are not using it frequently?**

Today changing of storage class requires manually moving or copying the data from one bucket to another bucket with the wanted storage class.


## Performance Questions

**Does data consistency in COS come with a performance impact?**

Consistency with any distributed system comes with a cost, but the efficiency of the {{site.data.keyword.cos_full_notm}} dispersed storage system is higher, and overhead is lower compared to systems with multiple synchronous copies.

**Aren't there performance implications if my application needs to manipulate large objects?**

For performance optimization, objects can be uploaded and downloaded in multiple parts, in parallel.


## Encryption Questions

**Does {{site.data.keyword.cos_full_notm}} provide encryption at rest and in motion?**

Yes.  Data at rest is encrypted with automatic provider side Advanced Encryption Standard (AES) 256-bit encryption and Secure Hash Algorithm (SHA)-256 hash. Data in motion is secured by using built-in carrier grade Transport Layer Security/Secure Sockets Layer (TLS/SSL) or SNMPv3 with AES encryption.

**What is the typical encryption overhead if a customer wants to encrypt their data?**

Server side encryption is always on for customer data. Compared to the hashing required in S3 authentication and the erasure coding, encryption is not a significant part of the processing cost of COS.

**Does {{site.data.keyword.cos_full_notm}} encrypt all data?**

Yes, {{site.data.keyword.cos_full_notm}} encrypts all data.

**Does {{site.data.keyword.cos_full_notm}} have FIPS 140-2 compliance for the encryption algorithms?**

Yes, {{site.data.keyword.cos_full_notm}} Federal offering is approved for FedRAMP Moderate Security controls, which require a validated FIPS configuration. {{site.data.keyword.cos_full_notm}} Federal is certified at FIPS 140-2 level 1. For more information about the Federal Offering, see [our Federal site ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/federal#AlternateAction).

## General questions

**How many objects can fit in a single bucket?**

There is no practical limit to the number of objects in a single bucket.

**Can I nest buckets inside one another?**

No, buckets can't be nested. If a greater level of organization is required within a bucket, the use of prefixes is supported: `{endpoint}/{bucket-name}/{object-prefix}/{object-name}`. The object's key remains the combination `{object-prefix}/{object-name}`.

**What is the difference between 'Class A' and 'Class B' requests?**

'Class A' requests are operations that involve modification or listing. This includes creating buckets, uploading or copying objects, creating or changing configurations, listing buckets, and listing the contents of buckets.'Class B' requests are operations that are related to retrieving objects or their associated metadata and configurations from the system. There is no charge for deleting buckets or objects from the system.

**What is the best way to structure your data in {{site.data.keyword.cos_short}} so that you can 'look' at it and find what you are looking for?  Without a directory structure, having 1000s of files at one level seems hard to view.**

You can use metadata associated with each object to find the objects you are looking for. The biggest advantage of {{site.data.keyword.cos_short}} is the metadata associated with each object. Each object can have up to 4 MB of metadata in {{site.data.keyword.cos_full_notm}}.  When offloaded to a database, metadata provides excellent search capabilities. Many (key, value) pairs can be stored in 4 MB. You can also use Prefix searching to find what you are looking for. For example, if you use buckets to separate each customer data, you can use prefixes within buckets for organization. For example,  ``/bucket1/folder/objec`t where 'folder/' is the prefix.

**Can you confirm that {{site.data.keyword.cos_full_notm}} is ‘immediately consistent’, as opposed to ‘eventually consistent’?**

COS is ‘immediately consistent’ for data and ‘eventually consistent’ for usage accounting.


**Can {{site.data.keyword.cos_full_notm}} partition the data automatically for me like HDFS, so I can read the partitions in parallel, for example,  with Spark?**

{{site.data.keyword.cos_full_notm}} supports a ranged GET on the object, so an application can do a distributed striped read type operation.  Doing the striping would be on the application to manage.
