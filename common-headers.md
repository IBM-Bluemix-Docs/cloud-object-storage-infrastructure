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


# Common headers

## Common Request Headers

The following table describes supported common request headers. {{site.data.keyword.objectstorageshort}} ignores any common headers that are not listed in the table, if they are sent in a request. Although, some requests might support other headers as defined in this documentation. For more information about creating the authorization header, see ["Authentication"](manage-access.html#authentication).


| Header             | Note                               |
|--------------------|-------------------------------------|
| `Authorization`      | **Required** for all requests (AWS Signature Version 4).   |
| `Host`               | **Required** for all requests.                 |
| `x-amz-date`         | **Required** for all requests. Can also be specified as `Date`.               |
| `x-amz-content-sha256`| **Required** for uploading objects or any request with information in the body. |
| `Content-Length`     | **Required** for uploading objects, chunked encoding also supported.    |
| `Content-MD5`        | A 128-bit MD5 hash value of the request body being sent.                  |
| `Expect`             | `100-continue` waits for the headers to be accepted before sending the body.  |
| `Cache-Control` | Can be used to specify caching behavior along the request/reply chain. For more information, see http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9 |
{:.opstable}

## Common Response Headers

The following table describes common response headers.

|  Header        | Note |
|----------------|------|
| `Content-Length`| The length of the request body in bytes.      |
| `Connection`    |  Indicates whether the connection is open or closed.     |
| `Date`        | Timestamp of the request.     |
| `ETag`          | MD5 hash value of the request.     |
| `Server`        | Name of the responding server.     |
| `X-Clv-Request-Id`|  Unique identifier generated per request. |
| `x-amz-restore`|Included if the object has been restored or if a restoration is in progress.|
| `x-amz-storage-class`|Returns GLACIER if archived or temporarily restored.|
| `x-ibm-archive-transition-time` | Returns the date and time when the object is scheduled to transition to the archive tier.|
| `x-ibm-transition`|Included if the object has transition metadata and returns the tier and original time of transition.|
| `x-ibm-restored-copy-storage-class`|Included if an object is in the `RestoreInProgress` or `Restored` states and returns the storage class of the bucket.|
{:.opstable}
