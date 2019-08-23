---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2018-08-22"

subcollection: cloud-object-storage-infrastructure

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}_
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Bucket operations

## List buckets belonging to an account

A `GET` that is issued to the endpoint root returns a list of buckets that are owned by the requesting account. This operation doesn't use operation-specific headers, query parameters, or payload elements.

**Syntax**

```bash
GET https://{endpoint}/
```

**Sample Request**

```http
GET / HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160822T030815Z
Authorization: {authorization-string}
```

**Sample Response**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ListAllMyBucketsResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <Owner>
        <ID>{access-key}</ID>
        <DisplayName>{access-key}</DisplayName>
    </Owner>
    <Buckets>
        <Bucket>
            <Name>bucket-27200-lwx4cfvcue</Name>
            <CreationDate>2016-08-18T14:21:36.593Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-27590-drqmydpfdv</Name>
            <CreationDate>2016-08-18T14:22:32.366Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-27852-290jtb0n2y</Name>
            <CreationDate>2016-08-18T14:23:03.141Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-28731-k0o1gde2rm</Name>
            <CreationDate>2016-08-18T14:25:09.599Z</CreationDate>
        </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

----

## Create a bucket

A `PUT` that is issued to the endpoint root and followed  by a string creates a bucket and uses that string for a name. Bucket names must be unique, and storage instances are limited to 100 buckets.  Bucket names are required to be DNS-compliant; names must be 3 - 63 characters long must be made of lowercase letters, numbers, and dashes. Bucket names must begin and end with a lowercase letter or number. Bucket names that resemble IP addresses are not allowed, although dot characters (`.`) are permitted. This operation doesn't use operation-specific headers or query parameters.

Valid provisioning codes for `LocationConstraint` are: <br>
&emsp;&emsp;  `us-standard` / `us-vault` / `us-cold` / `us-flex` <br>
&emsp;&emsp;  `us-east-standard` / `us-east-vault`  / `us-east-cold` / `us-east-flex` <br>
&emsp;&emsp;  `us-south-standard` / `us-south-vault`  / `us-south-cold` / `us-south-flex` <br>
&emsp;&emsp;  `eu-standard` / `eu-vault` / `eu-cold` / `eu-flex` <br>
&emsp;&emsp;  `eu-gb-standard` / `eu-gb-vault` / `eu-gb-cold` / `eu-gb-flex` <br>
&emsp;&emsp;  `ap-standard` / `ap-vault` / `ap-cold` / `ap-flex` <br>
&emsp;&emsp;  `ap-tok-standard` / `ap-tok-vault` / `ap-tok-cold` / `ap-tok-flex` <br>
&emsp;&emsp;  `au-syd-standard` / `au-syd-vault` / `au-syd-cold` / `au-syd-flex` <br>
&emsp;&emsp;  `ams03-standard` / `ams03-vault` / `ams03-cold` / `ams03-flex` <br>
&emsp;&emsp;  `che01-standard` / `che01-vault` / `che01-cold` / `che01-flex` <br>
&emsp;&emsp;  `mel01-standard` / `mel01-vault` / `mel01-cold` / `mel01-flex` <br>
&emsp;&emsp;  `mex01-standard` / `mex01-vault` / `mex01-cold` / `mel01-flex` <br>
&emsp;&emsp;  `mon01-standard` / `mon01-vault` / `mon01-cold` / `mon01-flex` <br>
&emsp;&emsp;  `osl01-standard` / `osl01-vault` / `osl01-cold` / `osl01-flex` <br>
&emsp;&emsp;  `sao01-standard` / `sao01-vault` / `sao01-cold` / `sao01-flex` <br>
&emsp;&emsp;  `seo01-standard` / `seo01-vault` / `seo01-cold` / `seo01-flex` <br>
&emsp;&emsp;  `tor01-standard` / `tor01-vault` / `tor01-cold` / `tor01-flex` <br>

**Syntax**

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

**Optional payload elements**

If an XML block specifies a `LocationConstraint` it must correspond with a valid provisioning code (for example, `us-standard`). If the request payload is left empty, the default provisioning code is used.

```xml
<CreateBucketConfiguration>
  <LocationConstraint>{provisioning-code}</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Request**

```http
PUT /images HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160821T052842Z
Authorization:{authorization-string}
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:45:25 GMT
X-Clv-Request-Id: dca204eb-72b5-4e2a-a142-808d2a5c2a87
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: dca204eb-72b5-4e2a-a142-808d2a5c2a87
Content-Length: 0
```

----

### Create a Vault bucket

To create a Vault bucket, send an XML block specifying a bucket configuration with a `LocationConstraint` of `us-vault` in the body of a `PUT` request to a bucket endpoint.

Valid provisioning codes for `LocationConstraint` are: <br>
&emsp;&emsp;  `us-standard` / `us-vault` / `us-cold` / `us-flex` <br>
&emsp;&emsp;  `us-east-standard` / `us-east-vault`  / `us-east-cold` / `us-east-flex` <br>
&emsp;&emsp;  `us-south-standard` / `us-south-vault`  / `us-south-cold` / `us-south-flex` <br>
&emsp;&emsp;  `eu-standard` / `eu-vault` / `eu-cold` / `eu-flex` <br>
&emsp;&emsp;  `eu-gb-standard` / `eu-gb-vault` / `eu-gb-cold` / `eu-gb-flex` <br>
&emsp;&emsp;  `ap-standard` / `ap-vault` / `ap-cold` / `ap-flex` <br>
&emsp;&emsp;  `che01-standard` / `che01-vault` / `che01-cold` / `che01-flex` <br>
&emsp;&emsp;  `mel01-standard` / `mel01-vault` / `mel01-cold` / `mel01-flex` <br>
&emsp;&emsp;  `tor01-standard` / `tor01-vault` / `tor01-cold` / `tor01-flex` <br>

**Syntax**

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-vault</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Request**

Creating a new bucket that is called `images`.

```http
PUT /vault-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```
```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-vault</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

----

### Create a Cold Vault bucket

To create a Vault bucket, send an XML block that specifies a bucket configuration with a `LocationConstraint` of `{code}-cold` in the body of a `PUT` request to a bucket endpoint.

Valid provisioning codes for `LocationConstraint` are: <br>
&emsp;&emsp;  `us-standard` / `us-vault` / `us-cold` / `us-flex` <br>
&emsp;&emsp;  `us-east-standard` / `us-east-vault`  / `us-east-cold` / `us-east-flex` <br>
&emsp;&emsp;  `us-south-standard` / `us-south-vault`  / `us-south-cold` / `us-south-flex` <br>
&emsp;&emsp;  `eu-standard` / `eu-vault` / `eu-cold` / `eu-flex` <br>
&emsp;&emsp;  `eu-gb-standard` / `eu-gb-vault` / `eu-gb-cold` / `eu-gb-flex` <br>
&emsp;&emsp;  `ap-standard` / `ap-vault` / `ap-cold` / `ap-flex` <br>
&emsp;&emsp;  `che01-standard` / `che01-vault` / `che01-cold` / `che01-flex` <br>
&emsp;&emsp;  `mel01-standard` / `mel01-vault` / `mel01-cold` / `mel01-flex` <br>
&emsp;&emsp;  `tor01-standard` / `tor01-vault` / `tor01-cold` / `tor01-flex` <br>


**Syntax**

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-cold</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Request**

Create a bucket that is called `cold-vault-images`.

```http
PUT /cold-vault-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```
```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-cold</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

----

### Create a Flex bucket

To create a Flex bucket, send an XML block that specifies a bucket configuration with a `LocationConstraint` of `{code}-flex` in the body of a `PUT` request to a bucket endpoint.

Valid provisioning codes for `LocationConstraint` are: <br>
&emsp;&emsp;  `us-standard` / `us-vault` / `us-cold` / `us-flex` <br>
&emsp;&emsp;  `us-east-standard` / `us-east-vault`  / `us-east-cold` / `us-east-flex` <br>
&emsp;&emsp;  `us-south-standard` / `us-south-vault`  / `us-south-cold` / `us-south-flex` <br>
&emsp;&emsp;  `eu-standard` / `eu-vault` / `eu-cold` / `eu-flex` <br>
&emsp;&emsp;  `eu-gb-standard` / `eu-gb-vault` / `eu-gb-cold` / `eu-gb-flex` <br>
&emsp;&emsp;  `ap-standard` / `ap-vault` / `ap-cold` / `ap-flex` <br>
&emsp;&emsp;  `che01-standard` / `che01-vault` / `che01-cold` / `che01-flex` <br>
&emsp;&emsp;  `mel01-standard` / `mel01-vault` / `mel01-cold` / `mel01-flex` <br>
&emsp;&emsp;  `tor01-standard` / `tor01-vault` / `tor01-cold` / `tor01-flex` <br>

**Syntax**

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-flex</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Request**

Create a bucket called `flex-images`.

```http
PUT /flex-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-flex</LocationConstraint>
</CreateBucketConfiguration>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

----

## Retrieve a bucket's headers

A `HEAD` that is issued to a bucket resource returns the headers for that bucket. This operation doesn't use operation-specific headers, query parameters, or payload elements.

**Syntax**

```bash
HEAD https://{endpoint}/{bucket-name} # path style
HEAD https://{bucket-name}.{endpoint} # virtual host style
```

**Sample Request**

Fetch the headers for the `images` bucket.

```http
HEAD /images HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160821T052842Z
Authorization:{authorization-string}
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:46:35 GMT
X-Clv-Request-Id: 0c2832e3-3c51-4ea6-96a3-cd8482aca08a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: 0c2832e3-3c51-4ea6-96a3-cd8482aca08a
Content-Length: 0
```

----

## List objects in a specific bucket

A `GET` request that is addressed to a bucket returns a list of objects, limited to 1,000 at a time and returned in non-lexicographical order. The `StorageClass` value that is returned in the response is a default value as storage class operations are not implemented in {{site.data.keyword.cos_full_notm}}. This operation doesn't use operation-specific headers or payload elements.

**Syntax**

The`version 2` method of listing objects within a bucket is not supported. The `version 1` syntax is needed.
{:tip}

```bash
GET https://{endpoint}/{bucket-name} # path style
GET https://{bucket-name}.{endpoint} # virtual host style
```

**Optional query parameters**

Name | Type | Description
--- | ---- | ------------
`prefix` | `string` | Constrains response to object names that begin with `prefix`.
`delimiter` | `string` | Groups objects between the `prefix` and the `delimiter`.
`encoding-type` | `string` | If Unicode characters that are not supported by XML are used in an object name, this parameter can be set to `url` to properly encode the response.
`max-keys` | `string` | Restricts the number of objects to display in the response. Default and maximum values are 1,000.
`marker` | `string` | Specifies the object from where the listing should begin, in UTF-8 binary order.

**Sample Request**

List the objects inside the `apiary` bucket.

```http
GET /apiary HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160822T225156Z
Authorization: {authorization-string}
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:36:24 GMT
X-Clv-Request-Id: 9f39ff2e-55d1-461b-a6f1-2d0b75138861
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: 9f39ff2e-55d1-461b-a6f1-2d0b75138861
Content-Type: application/xml
Content-Length: 909
```

```xml
<ListBucketResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Name>apiary</Name>
  <Prefix/>
  <Marker/>
  <MaxKeys>1000</MaxKeys>
  <Delimiter/>
  <IsTruncated>false</IsTruncated>
  <Contents>
    <Key>drone-bee</Key>
    <LastModified>2016-08-25T17:38:38.549Z</LastModified>
    <ETag>"0cbc6611f5540bd0809a388dc95a615b"</ETag>
    <Size>4</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
  <Contents>
    <Key>soldier-bee</Key>
    <LastModified>2016-08-25T17:49:06.006Z</LastModified>
    <ETag>"37d4c94839ee181a2224d6242176c4b5"</ETag>
    <Size>11</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
  <Contents>
    <Key>worker-bee</Key>
    <LastModified>2016-08-25T17:46:53.288Z</LastModified>
    <ETag>"d34d8aada2996fc42e6948b926513907"</ETag>
    <Size>467</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
</ListBucketResult>
```

----

## Delete a bucket

A `DELETE` that is issued to an empty bucket deletes the bucket. When the bucket is deleted, the name is held in reserve by the system for 10 minutes, after which it is released for re-use.  *Only empty buckets can be deleted.* This operation doesn't use operation-specific headers, query parameters, or payload elements.

**Syntax**

```bash
DELETE https://{endpoint}/{bucket-name} # path style
DELETE https://{bucket-name}.{endpoint} # virtual host style
```

**Sample Request**

```http
DELETE /images HTTP/1.1
Host: s3-api.us-geo.objectstorage.softlayer.net
x-amz-date: 20160822T064812Z
Authorization: {authorization-string}
```

The server responds with `204 No Content`.

If a non-empty bucket is requested for deletion, the server responds with `409 Conflict`.

**Sample Request**

```http
DELETE /apiary HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T174049Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```xml
<Error>
  <Code>BucketNotEmpty</Code>
  <Message>The bucket you tried to delete is not empty.</Message>
  <Resource>/apiary/</Resource>
  <RequestId>9d2bbc00-2827-4210-b40a-8107863f4386</RequestId>
  <httpStatusCode>409</httpStatusCode>
</Error>
```

----

## Create an access control list for a bucket

A `PUT` that is issued to a bucket with the necessary query parameter creates or replaces an access control list (ACL) for that bucket. Access control lists allow for granting different sets of permissions to different storage accounts by using the account's ID, or by using a pre-made ACL.

Credentials are generated for each storage account, not for individual users. As such, ACLs can't restrict or grant access to a specific user, only to a storage account. However, `public-read-write` allows any other {{site.data.keyword.cos_full_notm}} account to access the resource, as well as the general public.
{:tip}

ACLs can use pre-made permissions sets (or `canned ACLs`) or be customized in the body of the request. Pre-made ACLs are specified using the `x-amz-acl` header and custom ACLs are specified using XML in the request payload. Only one method (header or payload) can be used in a single request.

This operation doesn't use extra operation-specific query parameters.

ACL grantees must be other {{site.data.keyword.cos_full_notm}} instances, and their UUID can be found along with credentials in the web portal.

The assigned permissions behave as follows:

| Permission | When granted on a bucket | When granted on an object |
|------------|--------------------------|---------------------------|
| READ | Allows grantee to list all objects in bucket | Allows grantee to read object data and metadata |
| WRITE | Allows grantee to create, overwrite, and delete objects in bucket. Cannot be granted independently from READ permission. | N/A |
| READ_ACP | This permission does not exist for buckets; default setting is FULL_CONTROL | Allows grantee to read object ACL |
| WRITE_ACP | Default setting is FULL_CONTROL | Allows grantee to write ACL for applicable object |
| FULL_CONTROL | Allows grantee READ, WRITE, READ_ACP and WRITE_ACP permissions on bucket | Allows grantee READ, READ_ACP and WRITE_ACP permissions on object |

The following canned ACLs are supported by {{site.data.keyword.cos_full_notm}}.  Values that are not listed here are not supported.

| Canned ACL | Applies to | Notes |
|------------|------------|-----------|
| Private | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |
| Public-read | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |
| Public-read-write | Bucket and object | When set on a bucket, the requester is interpreted as the bucket owner. |

`READ` access, including `public-read`, when granted on a bucket does not allow for the actual access of objects themselves, only the ability to list them.
{:tip}

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}?acl= # path style
PUT https://{bucket-name}.{endpoint}?acl= # virtual host style
```

**Sample Request** Basic pre-made ACL

Specify a pre-made ACL to allow for `public-read` access to the `apiary` bucket. This operation allows any storage account to view the bucket's contents and ACL details.

```http
PUT /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
x-amz-acl: public-read
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Tue, 4 Oct 2016 19:03:55 GMT
X-Clv-Request-Id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Content-Length: 0
```

**Sample Request** Custom ACL

Specify a custom ACL to allow for another user using their user name to view the ACL for the `apiary` bucket, but not to list objects stored inside the bucket. A third account is given full access to the same bucket as another element of the same ACL. All authenticated users of the system can list objects in the bucket.

```http
PUT /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
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
Date: Tue, 4 Oct 2016 19:03:55 GMT
X-Clv-Request-Id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
```

----

## Retrieve the access control list for a bucket

A `GET` issued to a bucket with the proper parameters retrieves the ACL for a bucket. This operation doesn't use operation-specific headers, extra query parameters, or payload elements.

**Syntax**

```bash
GET https://{endpoint}/{bucket-name}?acl= # path style
GET https://{bucket-name}.{endpoint}?acl= # virtual host style
```

**Sample Request**

Retrieve a bucket ACL.

```http
GET /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 14:14:34 GMT
X-Clv-Request-Id: eb57e60e-d84e-4237-b18a-be9c2bb0deb8
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: eb57e60e-d84e-4237-b18a-be9c2bb0deb8
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

## Deleting multiple objects

A `POST` that is given a path to a bucket and proper parameters deletes a specified set of objects. This command requires a `Content-MD5` header in addition to the `x-amz-content-sha256` header. This operation doesn't use operation-specific query parameters, headers, or payload elements.

**Syntax**

```bash
POST https://{endpoint}/{bucket-name}/?delete= # path style
POST https://{bucket-name}.{endpoint}/?delete= # virtual host style
```

**Sample Request**

```http
POST /example?delete= HTTP/1.1
Authorization: {authorization-string}
Host: s3-api.us-geo.objectstorage.softlayer.net
x-amz-date: 20161205T231624Z
x-amz-content-sha256: 3ade096cd9471017539ede10c4d8aa05a1ecd015a16f4f090e9fcee92a816cf4
Content-MD5: zhi+TmIAhD2U3GfoYayyTQ==
Content-Type: text/plain; charset=utf-8
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Delete>
    <Object>
         <Key>surplus-bee</Key>
    </Object>
    <Object>
         <Key>unnecessary-bee</Key>
    </Object>
</Delete>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 30 Nov 2016 18:54:53 GMT
X-Clv-Request-Id: a6232735-c3b7-4c13-a7b2-cd40c4728d51
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.137
X-Clv-S3-Version: 2.5
x-amz-request-id: a6232735-c3b7-4c13-a7b2-cd40c4728d51
Content-Type: application/xml
Content-Length: 207
```
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeleteResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <Deleted>
         <Key>surplus-bee</Key>
    </Deleted>
    <Deleted>
         <Key>unnecessary-bee</Key>
    </Deleted>
</DeleteResult>
```

----

## List the cancelled or incomplete multi-part uploads for a bucket

A `GET` that is issued to a bucket with the proper parameters retrieves information about any cancelled or incomplete multi-part uploads for a bucket. This operation doesn't use operation-specific headers, extra query parameters, or payload elements.

**Syntax**

```bash
GET https://{endpoint}/{bucket-name}?uploads= # path style
GET https://{bucket-name}.{endpoint}?uploads= # virtual host style
```

**Parameters**

Name | Type | Description
--- | ---- | ------------
`prefix` | `string` | Constrains response to object names that begin with `{prefix}`.
`delimiter` | `string` | Groups objects between the `prefix` and the `delimiter`.
`encoding-type` | `string` | If Unicode characters that are not supported by XML are used in an object name, this parameter can be set to `url` to properly encode the response.
`max-uploads` | `integer` | Restricts the number of objects to display in the response. Default and maximum values are 1,000.
`key-marker` | `string` | Specifies from where the listing begins.
`upload-id-marker` | `string` | Ignored if `key-marker` is not specified, otherwise sets a point at which to begin listing parts before `upload-id-marker`.

**Sample Request**

Retrieve all current cancelled and incomplete multipart uploads.

```http
GET /apiary?uploads= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response** (no multipart uploads in progress)

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:22:27 GMT
X-Clv-Request-Id: 9fa96daa-9f37-42ee-ab79-0bcda049c671
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 9fa96daa-9f37-42ee-ab79-0bcda049c671
Content-Type: application/xml
Content-Length: 374
```

```xml
<ListMultipartUploadsResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Bucket>apiary</Bucket>
  <KeyMarker/>
  <UploadIdMarker/>
  <NextKeyMarker>multipart-object-123</NextKeyMarker>
  <NextUploadIdMarker>0000015a-df89-51d0-2790-dee1ac994053</NextUploadIdMarker>
  <MaxUploads>1000</MaxUploads>
  <IsTruncated>false</IsTruncated>
  <Upload>
    <Key>file</Key>
    <UploadId>0000015a-d92a-bc4a-c312-8c1c2a0e89db</UploadId>
    <Initiator>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Initiator>
    <Owner>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2017-03-16T22:09:01.002Z</Initiated>
  </Upload>
  <Upload>
    <Key>multipart-object-123</Key>
    <UploadId>0000015a-df89-51d0-2790-dee1ac994053</UploadId>
    <Initiator>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Initiator>
    <Owner>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2017-03-18T03:50:02.960Z</Initiated>
  </Upload>
</ListMultipartUploadsResult>
```

----

## List any cross-origin resource-sharing configuration for a bucket

A `GET` that is issued to a bucket with the proper parameters retrieves information about cross-origin resource-sharing (CORS) configuration for a bucket. This operation doesn't use operation-specific headers, extra query parameters, or payload elements.

**Syntax**

```bash
GET https://{endpoint}/{bucket-name}?cors= # path style
GET https://{bucket-name}.{endpoint}?cors= # virtual host style
```

**Sample Request**

List the CORS configuration on the `apiary` bucket.

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

**Sample Response** No CORS configuration set

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:20:30 GMT
X-Clv-Request-Id: 0b69bce1-8420-4f93-a04a-35d7542799e6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 0b69bce1-8420-4f93-a04a-35d7542799e6
Content-Type: application/xml
Content-Length: 123
```

```xml
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/"/>
```

----

## Create a cross-origin resource-sharing configuration for a bucket

A `PUT` that is issued to a bucket with the proper parameters creates or replaces a cross-origin resource-sharing (CORS) configuration for a bucket. In addition to an SHA256 hash of the body, a `Content-MD5` header is required as well. This operation doesn't use operation-specific headers or extra query parameters.

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}?cors= # path style
PUT https://{bucket-name}.{endpoint}?cors= # virtual host style
```

**Optional payload elements**

The XML block that defines the key CORS elements (`AllowedOrigin` and `AllowedMethod`) contains two other elements that can be optionally specified.

| Element | Description |
| --- | --- |
| `MaxAgeSeconds` | Time in seconds that the browser caches the response to the pre-flight OPTIONS request for the specified resource. |
| `ExposeHeader` | Defines specific headers that are exposed to external applications. |

**Sample Request**

Add a CORS configuration that allows requests from `www.ibm.com` to issue `GET`, `PUT`, and `POST` requests to the bucket.

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
x-amz-content-sha256: 2938f51643d63c864fdbea618fe71b13579570a86f39da2837c922bae68d72df
Content-MD5: GQmpTNpruOyK6YrxHnpj7g==
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 237
```

```xml
<CORSConfiguration>
  <CORSRule>
    <AllowedOrigin>http:www.ibm.com</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>POST</AllowedMethod>
  </CORSRule>
</CORSConfiguration>
```

**Sample Response**

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:39:38 GMT
X-Clv-Request-Id: 7afca6d8-e209-4519-8f2c-1af3f1540b42
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 7afca6d8-e209-4519-8f2c-1af3f1540b42
Content-Length: 0
```

----

## Delete any cross-origin resource-sharing configuration for a bucket

A `DELETE` that is issued to a bucket with the proper parameters creates or replaces a cross-origin resource-sharing (CORS) configuration for a bucket.

**Syntax**

```bash
DELETE https://{endpoint}/{bucket-name}?cors= # path style
DELETE https://{bucket-name}.{endpoint}?cors= # virtual host style
```

**Sample Request**

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

The server responds with `204 No Content`.

----

## Create a bucket lifecycle configuration

A `PUT` operation uses the lifecycle query parameter to set lifecycle settings for the bucket.  A `Content-MD5` header is required as an integrity check for the payload.

**Syntax**

```bash
PUT https://{endpoint}/{bucket-name}?lifecycle # path style
PUT https://{bucket-name}.{endpoint}?lifecycle # virtual host style
```

**Payload Elements**

The body of the request must contain an XML block with the following schema.

|Element|Type|Children|Ancestor|Constraint|
|---|---|---|---|---|
|`LifecycleConfiguration`|`Container`|`Rule`|None|Limit 1|
|`Rule`|`Container`|`ID`, `Status`, `Filter`, `Transition`|`LifecycleConfiguration`|Limit 1|
|`ID`|`String`|None|`Rule`|**Must** consist of `(a-z,A- Z0-9)` and the following symbols:`` !`_ .*'()- ``|
|`Filter`|`String`|`Prefix`|`Rule`|**Must** contain a `Prefix` element.|
|`Prefix`|`String`|None|`Filter`|**Must** be set to <Prefix/>.|
|`Transition`|`Container`|`Days`, `StorageClass`|Rule|Limit 1.|
|`Days`|`Non-negative integer`|None|`Transition`|**Must** be a value greater than 0.|
|`Date`|`Date`|None|`Transition`|**Must** be in ISO 8601 Format and the date must be in the future.|
|`StorageClass`|`String`|None|`Transition`|**Must** be set to GLACIER.|

```xml
<LifecycleConfiguration>
    <Rule>
        <ID>{string}</ID>
        <Status>Enabled</Status>
        <Filter>
            <Prefix/>
        </Filter>
        <Transition>
            <Days>{integer}</Days>
            <StorageClass>GLACIER</StorageClass>
        </Transition>
    </Rule>
</LifecycleConfiguration>
```

**Sample Request**

```http
GET / HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Authorization: {authorization-string}
Content-Type: text/plain
Content-MD5: M625BaNwd/OytcM7O5gIaQ==
Content-Length: 305
```

```xml
<LifecycleConfiguration>
    <Rule>
        <ID>my-archive-policy</ID>
        <Filter>
            <Prefix/>
        </Filter>
        <Status>Enabled</Status>
        <Transition>
            <Days>20</Days>
            <StorageClass>GLACIER</StorageClass>
        </Transition>
    </Rule>
</LifecycleConfiguration>
```

The server responds with `200 OK`.

----

## Retrieve a bucket lifecycle configuration

A `GET` operation uses the lifecycle query parameter to retrieve lifecycle settings for the bucket.

**Syntax**

```bash
GET https://{endpoint}/{bucket-name}?lifecycle # path style
GET https://{bucket-name}.{endpoint}?lifecycle # virtual host style
```

**Sample Request**

```http
GET / HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Authorization: {authorization-string}
```

**Sample Response**

```xml
<LifecycleConfiguration>
    <Rule>
        <ID>my-archive-policy</ID>
        <Filter>
            <Prefix/>
        </Filter>
        <Status>Enabled</Status>
        <Transition>
            <Days>20</Days>
            <StorageClass>GLACIER</StorageClass>
        </Transition>
    </Rule>
</LifecycleConfiguration>
```

----

## Delete the lifecycle configuration for a bucket

A `DELETE` issued to a bucket with the proper parameters removes any lifecycle configurations for a bucket.

**Syntax**

```bash
DELETE https://{endpoint}/{bucket-name}?lifecycle # path style
DELETE https://{bucket-name}.{endpoint}?lifecycle # virtual host style
```

**Sample Request**

```http
GET /apiary?lifecycle HTTP/1.1
Authorization: {authorization-string}
Host: s3-api.us-geo.objectstorage.softlayer.net
```

The server responds with `204 No Content`.
