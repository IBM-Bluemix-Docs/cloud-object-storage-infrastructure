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


# Object operations

## Upload an object

A `PUT` specific a path to an object uploads the request body as an object. An SHA256 hash of the object is a required header. All objects are limited to 10 TB in size. This operation doesn't use operation-specific query parameters, or payload elements.

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}/{object-name} # path style
PUT https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Specific headers for SSE-C**

The following headers are available for buckets that use Server-side Encryption with Customer-Provided Keys (SSE-C). Any request that uses SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string.

Header | Type | Description
--- | ---- | ------------
`x-amz-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

```http
PUT /example-bucket/queen-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T183001Z
x-amz-content-sha256: 309721641329cf441f3fa16ef996cf24a2505f91be3e752ac9411688e3435429
Content-Type: text/plain; charset=utf-8
Host: s3-api.us-geo.objectstorage.softlayer.net

Content-Length: 533

 The 'queen' bee is developed from larvae selected by worker bees and fed a
 substance referred to as 'royal jelly'. After a short while the 'queen' is
 the mother of nearly every bee in the hive, and the colony will fight
 fiercely to protect her.

```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Thu, 25 Aug 2016 18:30:02 GMT
X-Clv-Request-Id: 9f0ca49a-ae13-4d2d-925b-117b157cf5c3
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.121
X-Clv-S3-Version: 2.5
x-amz-request-id: 9f0ca49a-ae13-4d2d-925b-117b157cf5c3
ETag: "3ca744fa96cb95e92081708887f63de5"
Content-Length: 0
```

**Sample Request** with SSE-C

```http
PUT /example-bucket/queen-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T183001Z
x-amz-content-sha256: 309721641329cf441f3fa16ef996cf24a2505f91be3e752ac9411688e3435429
x-amz-server-side-encryption-customer-algorithm: AES256
x-amz-server-side-encryption-customer-key: MjRCRTJCQTNDQjdFOTkyMzY0NjZEN0NBMDhGQTBGRUQwNzFBMjEwMkQyNjU4MjNEOEMyODU5MkQxQ0ZEMkQ1OQ==
x-amz-server-side-encryption-customer-key-MD5: HBbrEt+ZH5iIfDNeBju03w==
Content-Type: text/plain; charset=utf-8
Host: s3-api.us-geo.objectstorage.softlayer.net

Content-Length: 533

 The 'queen' bee is developed from larvae selected by worker bees and fed a
 substance referred to as 'royal jelly'. After a short while the 'queen' is
 the mother of nearly every bee in the hive, and the colony will fight
 fiercely to protect her.

```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Thu, 25 Aug 2016 18:30:02 GMT
X-Clv-Request-Id: 9f0ca49a-ae13-4d2d-925b-117b157cf5c3
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.121
X-Clv-S3-Version: 2.5
x-amz-request-id: 9f0ca49a-ae13-4d2d-925b-117b157cf5c3
ETag: "3ca744fa96cb95e92081708887f63de5"
x-amz-server-side-encryption-customer-algorithm: AES256
x-amz-server-side-encryption-customer-key-MD5: HBbrEt+ZH5iIfDNeBju03w==
Content-Length: 0
```

----

## Get an object's headers

A `HEAD` specific a path to an object retrieves that object's headers. This operation doesn't use operation-specific query parameters or payload elements.

**Syntax**

```bash
HEAD https://{endpoint}/{bucket-name}/{object-name} # path style
HEAD https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Optional Headers**

Header | Type | Description
--- | ---- | ------------
`range` | `string` | Returns the bytes of an object within the specified range.
`x-amz-copy-source-if-match` | `string` (`ETag`)| Return the metadata if the specified `ETag` matches the source object.
`x-amz-copy-source-if-none-match` | `string` (`ETag`)| Return the metadata if the specified `ETag` is different from the source object.
`x-amz-copy-source-if-unmodified-since` | `string (timestamp)`| Return the metadata if the the source object has not been modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).
`x-amz-copy-source-if-modified-since` | `string (timestamp)`| Return the metadata if the source object has been modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).

**Specific headers for SSE-C**

The following headers are available for buckets that use Server-side Encryption with Customer-Provided Keys (SSE-C). Any request that contain SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string.

Header | Type | Description
--- | ---- | ------------
`x-amz-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

```http
HEAD /example-bucket/soldier-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T183244Z
Host: s3-api.us-geo.objectstorage.softlayer.net

```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Thu, 25 Aug 2016 18:32:44 GMT
X-Clv-Request-Id: da214d69-1999-4461-a130-81ba33c484a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.121
X-Clv-S3-Version: 2.5
x-amz-request-id: da214d69-1999-4461-a130-81ba33c484a6
ETag: "37d4c94839ee181a2224d6242176c4b5"
Content-Type: text/plain; charset=UTF-8
Last-Modified: Thu, 25 Aug 2016 17:49:06 GMT
Content-Length: 11
```

----

## Download an object

A `GET` specific a path to an object downloads the object. This operation doesn't use operation-specific query parameters or payload elements.

**Syntax**

```bash
GET https://{endpoint}/{bucket-name}/{object-name} # path style
GET https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Optional Headers**

Header | Type | Description
--- | ---- | ------------
`range` | `string` | Returns the bytes of an object within the specified range.
`x-amz-copy-source-if-match` | `string` (`ETag`)| Return the object if the specified `ETag` matches the source object.
`x-amz-copy-source-if-none-match` | `string` (`ETag`)| Return the object if the specified `ETag` is different from the source object.
`x-amz-copy-source-if-unmodified-since` | `string (timestamp)`| Return the object if the the source object was not modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).
`x-amz-copy-source-if-modified-since` | `string (timestamp)`| Return the object if the the source object was modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).

**Specific headers for SSE-C**

The following headers are available for buckets that use Server-side Encryption with Customer-Provided Keys (SSE-C). Any request that uses SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string.

Header | Type | Description
--- | ---- | ------------
`x-amz-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

```http
GET /example-bucket/worker-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T183244Z
Host: s3-api.us-geo.objectstorage.softlayer.net

```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Thu, 25 Aug 2016 18:34:25 GMT
X-Clv-Request-Id: 116dcd6b-215d-4a81-bd30-30291fa38f93
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.121
X-Clv-S3-Version: 2.5
ETag: "d34d8aada2996fc42e6948b926513907"
Content-Type: text/plain; charset=UTF-8
Last-Modified: Thu, 25 Aug 2016 17:46:53 GMT
Content-Length: 467

 Female bees that are not fortunate enough to be selected to be the 'queen'
 while they were still larvae become known as 'worker' bees. These bees lack
 the ability to reproduce and instead ensure that the hive functions smoothly,
 acting almost as a single organism in fulfilling their purpose.
```

----

## Delete an object

A `DELETE` specific a path to an object deletes an object. This operation doesn't use operation-specific query parameters, headers, or payload elements.

**Syntax**

```bash
DELETE https://{endpoint}/{bucket-name}/{object-name} # path style
DELETE https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Sample Request**

```http
DELETE /example-bucket/soldier-bee HTTP/1.1
Authorization: {authorization-string}
Host: s3-api.us-geo.objectstorage.softlayer.net

```

**Sample Response**

```http
HTTP/1.1 204 No Content
Date: Thu, 25 Aug 2016 17:44:57 GMT
X-Clv-Request-Id: 8ff4dc32-a6f0-447f-86cf-427b564d5855
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.121
X-Clv-S3-Version: 2.5
```

----

## Copy an object

A `PUT` specific a path to a new object creates a new copy of another object specified by the `x-amz-copy-source` header. Unless otherwise altered the metadata remains the same, although any ACL is reset to `private` for the  account creating the copy. This operation doesn't use operation-specific query parameters or payload elements.


**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}/{object-name} # path style
PUT https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Optional Headers**

Header | Type | Description
--- | ---- | ------------
`x-amz-metadata-directive` | `string `(`COPY` or `REPLACE`) | `REPLACE` overwrites original metadata with new metadata that is provided.
`x-amz-copy-source-if-match` | `string `(`ETag`)| Creates a copy if the specified `ETag` matches the source object.
`x-amz-copy-source-if-none-match` | `string` (`ETag`)| Creates a copy if the specified `ETag` is different from the source object.
`x-amz-copy-source-if-unmodified-since` | `string (timestamp)`| Creates a copy if the the source object has not been modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).
`x-amz-copy-source-if-modified-since` | `string (timestamp)`| Creates a copy if the source object has been modified since the specified date.  Date must be a valid HTTP date (for example,`Wed, 30 Nov 2016 20:21:38 GMT`).

**Specific headers for SSE-C**

The following headers are available for objects being copied into buckets that have Server-side Encryption with Customer-Provided Keys (SSE-C). Any `PUT` request with SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string.

The specific SSE-C headers used to initially upload objects are required if the copy operation encrypts the copy of the data at the target destination. If the original source object was encrypted by using SSE-C, the specific headers used for copying objects need to be present to decrypt the object source. Copies of objects do not need to be encrypted with the same key.

Header | Type | Description
--- | ---- | ------------
`x-amz-copy-source-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-copy-source-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-copy-source-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-copy-source-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-copy-source-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

This basic example takes the `bee` object from the `garden` bucket, and creates a copy in the `example` bucket with the new key `wild-bee`.

```http
PUT /example-bucket/wild-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161130T195251Z
x-amz-copy-source: /garden/bee
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 30 Nov 2016 19:52:52 GMT
X-Clv-Request-Id: 72992a90-8f86-433f-b1a4-7b1b33714bed
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: 72992a90-8f86-433f-b1a4-7b1b33714bed
ETag: "853aab195ce770b0dfb294a4e9467e62"
Content-Type: application/xml
Content-Length: 240
```

```xml
<CopyObjectResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <LastModified>2016-11-30T19:52:53.125Z</LastModified>
  <ETag>"853aab195ce770b0dfb294a4e9467e62"</ETag>
</CopyObjectResult>
```

----

## Retrieve an object's ACL

A `GET` specific a path to an object specific the parameter `?acl=` retrieves the access control list for the object. This operation doesn't use operation-specific headers, additional query parameters  or payload elements.


**Syntax**

```bash
GET https://{endpoint}/{bucket-name}/{object-name}?acl= # path style
GET https://{bucket-name}.{endpoint}/{object-name}?acl= # virtual host style
```

**Sample Request**

```http
GET /example-bucket/queen-bee?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161207T155945Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 07 Dec 2016 15:59:46 GMT
X-Clv-Request-Id: 78541562-29bf-4800-9eb3-0c360f0a037a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: 78541562-29bf-4800-9eb3-0c360f0a037a
Content-Type: application/xml
Content-Length: 550
```

```xml
<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Owner>
    <ID>{owner-storage-account-uuid}</ID>
    <DisplayName>{owner-storage-account-uuid}</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{owner-storage-account-uuid}</ID>
        <DisplayName>{owner-storage-account-uuid}</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

----

## Create an ACL for an object

A `PUT` issued to an object with the proper parameters creates an access control list (ACL) for that object. Access control lists grant different sets of permissions to different storage accounts by using the account's ID, or by using a pre-made ACL.

Credentials are generated for each storage account, not for individual users.  As such, ACLs do not have the ability to restrict or grant access to a specific user, only to a storage account. However, `public-read-write` allows any other storage account to access the resource, as well as the general public.

The assigned permissions behave as follows:

| Permission | When granted on a bucket | When granted on an object |
|------------|--------------------------|---------------------------|
| `READ `| Allows grantee to list all objects in bucket | Allows grantee to read object data and metadata |
| `WRITE` | Allows grantee to create, overwrite and delete new objects in bucket. Cannot be granted independently from READ permission. | N/A |
| `READ_ACP` | This permission does not exist for buckets; default setting is FULL_CONTROL | Allows grantee to read object ACL |
| `WRITE_ACP` | Default setting is FULL_CONTROL | Allows grantee to write ACL for applicable object |
| `FULL_CONTROL` | Allows grantee READ, WRITE, READ_ACP and WRITE_ACP permissions on bucket | Allows grantee READ, READ_ACP and WRITE_ACP permissions on object |


The following canned ACLs are supported by {{site.data.keyword.cos_short}}. Values not listed here are not supported.

| Canned ACL | Applies to | Notes |
|------------|------------|-----------|
| Private | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |
| Public-read | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |
| Public-read-write | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |

It is not possible to grant granular `WRITE` access at the object level, only at the bucket level.

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}/{object-name}?acl= # path style
PUT https://{bucket-name}.{endpoint}/{object-name}?acl= # virtual host style
```

**Sample Request** (canned ACL)

```http
PUT /example-bucket/queen-bee?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161207T162842Z
x-amz-acl: public-read
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 07 Dec 2016 16:28:42 GMT
X-Clv-Request-Id: b8dea44f-af20-466d-83ec-2a8563f1617b
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: b8dea44f-af20-466d-83ec-2a8563f1617b
Content-Length: 0
```

**Sample Request** (canned ACL in header)

It is also possible to assign a canned ACL directly when uploading an object by passing the `x-amz-acl` header and a canned ACL value. This example makes the `queen-bee` object publicly and anonymously accessible.

```http
PUT /example-bucket/queen-bee HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161207T162842Z
x-amz-acl: public-read
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 07 Dec 2016 16:28:42 GMT
X-Clv-Request-Id: b8dea44f-af20-466d-83ec-2a8563f1617b
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: b8dea44f-af20-466d-83ec-2a8563f1617b
Content-Length: 0
```

**Sample Request** (custom ACL)

This is an example of specifying a custom ACL to allow for another account to view the ACL for the "queen-bee" object, but not to access object itself. Additionally, a third account is specific full access to the same object as another element of the same ACL.

```http
PUT /example-bucket/queen-bee?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161207T163315Z
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 564
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Owner>
    <ID>{owner-storage-account-uuid}</ID>
    <DisplayName>OwnerDisplayName</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{first-grantee-storage-account-uuid}</ID>
        <DisplayName>Grantee1DisplayName</DisplayName>
      </Grantee>
      <Permission>READ_ACP</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{second-grantee-storage-account-uuid}</ID>
        <DisplayName>Grantee2DisplayName</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 07 Dec 2016 17:11:51 GMT
X-Clv-Request-Id: ef02ea42-6fa6-4cc4-bec4-c59bc3fcc9f7
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: ef02ea42-6fa6-4cc4-bec4-c59bc3fcc9f7
Content-Length: 0
```

----

## Check an object's CORS configuration

An `OPTIONS` request that is given a path to an object along with an origin and request type checks to see if that object is accessible from that origin by using that request type. Unlike all other requests, an `OPTIONS` request does not require the `authorization` or `x-amx-date` headers.

**Syntax**

```bash
OPTIONS https://{endpoint}/{bucket-name}/{object-name} # path style
OPTIONS https://{bucket-name}.{endpoint}/{object-name} # virtual host style
```

**Sample Request**

```http
OPTIONS /example-bucket/queen-bee HTTP/1.1
Access-Control-Request-Method: PUT
Origin: http://ibm.com
Host: s3-api.us-geo.objectstorage.softlayer.net

```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 07 Dec 2016 16:23:14 GMT
X-Clv-Request-Id: 9a2ae3e1-76dd-4eec-a8f2-1a7f60f63483
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: 9a2ae3e1-76dd-4eec-a8f2-1a7f60f63483
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: PUT
Access-Control-Allow-Credentials: true
Vary: Origin, Access-Control-Request-Headers, Access-Control-Allow-Methods
Content-Length: 0

```

----

## Uploading objects in multiple parts

When working with larger objects, multipart upload operations are recommended to write objects into {{site.data.keyword.cos_short}}. An upload of a single object can be performed as a set of parts and these parts can be uploaded independently in any order and in parallel. Upon upload completion, {{site.data.keyword.cos_short}} then presents all parts as a single object. This provides many benefits: network interruptions do not cause large uploads to fail, uploads can be paused and restarted over time, and objects can be uploaded as they are being created.

Multipart uploads are only available for objects larger than 5MB. For objects smaller than 50GB, 500 parts sized 20MB to 100MB is recommended for optimum performance. For larger objects, part size can be increased without significant performance impact.  Multipart uploads are limited to no more than 10,000 parts of 5GB each and a maximum object size of 5TB.

Due to the additional complexity involved, it is recommended that Developers make use of S3 API libraries that provide multipart upload support.

Incomplete multipart uploads do persist until the object is deleted or the multipart upload is aborted with `AbortIncompleteMultipartUpload`. If an incomplete multipart upload is not aborted, the partial upload continues to use resources.  Interfaces should be designed with this point in mind, and clean up incomplete multipart uploads.

There are three phases to uploading an object in multiple parts:

1. The upload is initiated and an `UploadId` is created.
2. Individual parts are uploaded specifying their sequential part numbers and the `UploadId` for the object.
3. When all parts are finished uploading, the upload is completed by sending a request with the `UploadId` and an XML block that lists each part number and it's respective `Etag` value.

### Initiate a multipart upload

A `POST` issued to an object with the query parameter `upload` creates a new `UploadId` value, which is then be referenced by each part of the object being uploaded.

**Syntax**

```bash
POST https://{endpoint}/{bucket-name}/{object-name}?uploads= # path style
POST https://{bucket-name}.{endpoint}/{object-name}?uploads= # virtual host style
```

**Specific headers for SSE-C**

The following headers are available for buckets that use Server-side Encryption with Customer-Provided Keys (SSE-C). Any request that uses SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string. *These headers must be identical to those provided for each part of the multipart upload.*

Header | Type | Description
--- | ---- | ------------
`x-amz-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

```http
POST /some-bucket/multipart-object-123?uploads= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170303T203411Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Fri, 03 Mar 2017 20:34:12 GMT
X-Clv-Request-Id: 258fdd5a-f9be-40f0-990f-5f4225e0c8e5
Accept-Ranges: bytes
Server: Cleversafe/3.9.1.114
X-Clv-S3-Version: 2.5
Content-Type: application/xml
Content-Length: 276
```

```xml
<InitiateMultipartUploadResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Bucket>some-bucket</Bucket>
  <Key>multipart-object-123</Key>
  <UploadId>0000015a-95e1-4326-654e-a1b57887784f</UploadId>
</InitiateMultipartUploadResult>
```

----

### Upload a part

A `PUT` request issued to an object with query parameters `partNumber` and `uploadId` uploads one part of an object.  The parts may be uploaded serially or in parallel, but must be numbered in order.

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}/{object-name}?partNumber={sequential-integer}&uploadId={uploadId}= # path style
PUT https://{bucket-name}.{endpoint}/{object-name}?partNumber={sequential-integer}&uploadId={uploadId}= # virtual host style
```


**Specific headers for SSE-C**
{: #sse-c}

The following headers are available for buckets that use Server-side Encryption with Customer-Provided Keys (SSE-C). Any request that uses SSE-C headers must be sent by using SSL. The `ETag` values in response headers are *not* the MD5 hash of the object, but a randomly generated 32-byte hexadecimal string. *These headers must be identical to those provided when the multipart operation was initiated.*

Header | Type | Description
--- | ---- | ------------
`x-amz-server-side-encryption-customer-algorithm` | `string` | This header is used to specify the algorithm and key size to use with the encryption key stored in `x-amz-server-side-encryption-customer-key` header. This value must be set to the string `AES256`.
`x-amz-server-side-encryption-customer-key` | `string` | This header is used to transport the base 64 encoded byte string representation of the AES 256 key used in the server-side encryption process.
`x-amz-server-side-encryption-customer-key-MD5` | `string` | This header is used to transport the base64-encoded 128-bit MD5 digest of the encryption key according to RFC 1321. The object store uses this value to validate the key passes in the `x-amz-server-side-encryption-customer-key` has not been corrupted during transport and encoding process. The digest must be calculated on the key BEFORE the key is base 64 encoded.

**Sample Request**

```http
PUT /some-bucket/multipart-object-123?partNumber=1&uploadId=0000015a-df89-51d0-2790-dee1ac994053 HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170318T035641Z
Content-Type: application/pdf
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 13374550
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Sat, 18 Mar 2017 03:56:41 GMT
X-Clv-Request-Id: 17ba921d-1c27-4f31-8396-2e6588be5c6d
Accept-Ranges: bytes
Server: Cleversafe/3.9.1.114
X-Clv-S3-Version: 2.5
ETag: "7417ca8d45a71b692168f0419c17fe2f"
Content-Length: 0
```

----

### Complete a multipart upload

A `POST` request that is issued to an object with query parameter `uploadId` and the appropriate XML block in the body completes a multipart upload.

**Syntax**

```bash
POST https://{endpoint}/{bucket-name}/{object-name}?uploadId={uploadId}= # path style
POST https://{bucket-name}.{endpoint}/{object-name}?uploadId={uploadId}= # virtual host style
```

```xml
<CompleteMultipartUpload>
  <Part>
    <PartNumber>{sequential part number}</PartNumber>
    <ETag>{ETag value from part upload response header}</ETag>
  </Part>
</CompleteMultipartUpload>
```

**Sample Request**

```http
POST /some-bucket/multipart-object-123?uploadId=0000015a-df89-51d0-2790-dee1ac994053 HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170318T035641Z
Content-Type: text/plain; charset=utf-8
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 257
```

```xml
<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"7417ca8d45a71b692168f0419c17fe2f"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"7417ca8d45a71b692168f0419c17fe2f"</ETag>
  </Part>
</CompleteMultipartUpload>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Fri, 03 Mar 2017 19:18:44 GMT
X-Clv-Request-Id: c8be10e7-94c4-4c03-9960-6f242b42424d
Accept-Ranges: bytes
Server: Cleversafe/3.9.1.114
X-Clv-S3-Version: 2.5
ETag: "765ba3df36cf24e49f67fc6f689dfc6e-2"
Content-Type: application/xml
Content-Length: 364
```

```xml
<CompleteMultipartUploadResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Location>http://s3-api.us-geo.objectstorage.softlayer.net/example-bucket/multipart-object-123</Location>
  <Bucket>some-bucket</Bucket>
  <Key>multipart-object-123</Key>
  <ETag>"765ba3df36cf24e49f67fc6f689dfc6e-2"</ETag>
</CompleteMultipartUploadResult>
```

----

### Abort incomplete multipart uploads

A `DELETE` request that is issued to an object with query parameter `uploadId` deletes all unfinished parts of a multipart upload.

**Syntax**

```bash
DELETE https://{endpoint}/{bucket-name}/{object-name}?uploadId={uploadId}= # path style
DELETE https://{bucket-name}.{endpoint}/{object-name}?uploadId={uploadId}= # virtual host style
```

**Sample Request**

```http
DELETE /some-bucket/multipart-object-123?uploadId=0000015a-df89-51d0-2790-dee1ac994053 HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170318T035641Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 204 No Content
Date: Thu, 16 Mar 2017 22:07:48 GMT
X-Clv-Request-Id: 06d67542-6a3f-4616-be25-fc4dbdf242ad
Accept-Ranges: bytes
Server: Cleversafe/3.9.1.114
X-Clv-S3-Version: 2.5
```

----

## Temporarily restore an archived object

A `POST` request issued to an object with query parameter `restore` to request temporary restoration of an archived object.  A `Content-MD5` header is required as an integrity check for the payload.

An archived object must be restored before downloading or modifying the object.  The lifetime of the object must be specified, after which the temporary copy of the object is deleted.

There can be a delay of up to 15 hours before the restored copy is available for access. A `HEAD` request can check if the restored copy is available.

To permanently restore the object, it must be copied to a bucket that does not have an active lifecycle configuration.

**Syntax**

```bash
POST https://{endpoint}/{bucket-name}/{object-name}?restore # path style
POST https://{bucket-name}.{endpoint}/{object-name}?restore # virtual host style
```

**Payload Elements**

The body of the request must contain an XML block with the following schema.

|Element|Type|Children|Ancestor|Constraint|
|---|---|---|---|---|
|`RestoreRequest`|`Container`|`Days, GlacierJobParameters`|None|None|
|`Days`|`Integer`|None|`RestoreRequest`|Specified the lifetime of the temporarily restored object. The minimum number of days that a restored copy of the object can exist is 1. After the restore period has elapsed, temporary copy of the object is removed.|
|`GlacierJobParameters`|`String`|`Tier`|`RestoreRequest`|None|
|`Tier`|`String`|None|`GlacierJobParameters`|**Must** be set to `Bulk`.|

```xml
<RestoreRequest>
    <Days>{integer}</Days>
    <GlacierJobParameters>
        <Tier>Bulk</Tier>
    </GlacierJobParameters>
</RestoreRequest>
```

**Sample Request**

```http
POST /apiary/queenbee?restore HTTP/1.1
Authorization: {authorization-string}
Content-Type: text/plain
Content-MD5: rgRRGfd/OytcM7O5gIaQ==
Content-Length: 305
Host: s3-api.us-geo.objectstorage.softlayer.net
```

```xml
<RestoreRequest>
    <Days>3</Days>
    <GlacierJobParameters>
        <Tier>Bulk</Tier>
    </GlacierJobParameters>
</RestoreRequest>
```

**Sample Response**

```http
HTTP/1.1 202 Accepted
Date: Thu, 16 Mar 2017 22:07:48 GMT
X-Clv-Request-Id: 06d67542-6a3f-4616-be25-fc4dbdf242ad
Accept-Ranges: bytes
Server: Cleversafe/3.9.1.114
X-Clv-S3-Version: 2.5
```
