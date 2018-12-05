---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-03"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}


# About the COS API

{{site.data.keyword.cos_full}} provides two separate APIs for managing and using object storage.

* Account and credential administration uses the SL API
* Interacting with buckets and objects uses an implementation of the S3 API

More information about how to use the SL API to create or delete credentials, check capacity usage, retrieve a UUID, and other account functions, see the [SLDN ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://sldn.softlayer.com/reference/services/SoftLayer_Network_Storage_Hub_Cleversafe_Account).

The following tables describe the complete set of supported operations you can use with the S3 API to access {{site.data.keyword.cos_notm}}. For more information, about how to use the operations, including examples, see the API reference pages for [buckets](buckets.html) and [objects](objects.html).

## Operations on the account

The only operation that is performed directly at the account level is to get a list of buckets owned by that account. Accounts are limited to 100 buckets.
{:tip}

| Account operation | Note |
|:----|:---|
| `GET` account | Used to retrieve a list of all buckets belonging to an account. |
{:.opstable}

### Operations on buckets

These operations create, destroy, get information about, and control behavior of buckets.

The 'version 2' method of listing objects within a bucket is not supported. The 'version 1' syntax is needed.
{:important}

| Bucket operation | Note |
|:----|:---|
| `DELETE` Bucket | Deletes an empty bucket.   |
| `DELETE` Bucket CORS | Deletes any cross-origin resource sharing configuration set on a bucket. |
| `DELETE` Bucket LIFECYCLE | Deletes the lifecycle settings for a bucket.  Existing transition rules will be maintained for existing objects. |
| `GET` Bucket | Lists objects contained in a bucket.  Limited to listing 1,000 objects at once. |
| `GET` Bucket ACL |Retrieves the access control list for a bucket.|
| `GET` Bucket CORS |Retrieves any cross-origin resource sharing configuration set on a bucket.|
| `GET` Bucket LIFECYCLE | Retrieves the lifecycle settings for a bucket |
| `HEAD` Bucket | Retrieves a bucket's headers. |
| `GET` multipart uploads | Lists multipart uploads that have not completed or been canceled. |
| `PUT` Bucket | Buckets have naming restrictions. Accounts are limited to 100 buckets. |
| `PUT` Bucket ACL | Creates an access control list for a bucket. |
| `PUT` Bucket CORS | Creates a cross-origin resource sharing configuration for a bucket.|
| `PUT` Bucket LIFECYCLE | Creates the lifecycle settings for a bucket.  Applies to only new objects added to the bucket. |
{:.opstable}

## Operations on objects

These operations create, destroy, get information about, and control behavior of objects.

| Object operation | Note |
| :---------------| :------|
| `DELETE` Object | Deletes an object from a bucket.
| `DELETE` Multiple Objects  | Deletes multiple objects from a bucket.
| `GET` Object | Retrieves an object from a bucket.
| `GET` Object ACL | Retrieves an object's access control list.
| `HEAD` Object | Retrieves an object's headers.
| `OPTIONS` Object | Checks CORS configuration to see if a specific request can be sent.
| `POST` Object | Adds an object to a bucket using HTML forms.
| `POST` Object RESTORE | Temporarily restores an archived object. |
| `PUT` Object | Adds an object to a bucket.
| `PUT` Object ACL | Creates an access control list for an object.
| `PUT` Object (Copy) | Creates a copy of an object. |
| Initiate Multipart Upload | Creates an upload ID for a given set of parts to be uploaded.
| Upload Part | Uploads a part of an object associated with an upload ID.
| Upload Part (Copy) | Uploads a part of an existing object associated with an upload ID.
| Complete Multipart Upload | Assembles an object from parts associated with an upload ID.
| Abort Multipart Upload | Aborts upload and deletes outstanding parts associated with an upload ID.
| List Parts | Returns a list of parts associated with an upload ID
{:.opstable}

Some additional operations, such as tagging and versioning, are supported in private cloud implementations of {{site.data.keyword.cos_notm}}, but not in the public cloud. For more information about custom object storage solutions, see [{{site.data.keyword.objectstorageshort}} at ibm.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/products/storage/object-storage/cloud/).
