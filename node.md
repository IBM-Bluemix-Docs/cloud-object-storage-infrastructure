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


# Using Node.js

## Installing

The preferred way to install the {{site.data.keyword.cos_full}} SDK for Node.js is to use the [`npm` ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com) package manager for Node.js. Simply type the following into a terminal window:

```sh
npm install ibm-cos-sdk
```
{:pre}

Source code is hosted on [GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/ibm-cos-sdk-js).

For more information about individual methods and classes, see [the API documentation for the SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm.github.io/ibm-cos-sdk-js/).

## Getting Started

### Minimum requirements

To run the SDK, you  need **Node 4.x+**.

### Code example

```javascript
var AWS = require('ibm-cos-sdk');
var util = require('util');

var config = {
    endpoint: '<endpoint>',
    apiKeyId: '<api-key>',
    ibmAuthEndpoint: 'https://iam.ng.bluemix.net/oidc/token',
    serviceInstanceId: '<resource-instance-id>',
};

var cos = new AWS.S3(config);

function doCreateBucket() {
    console.log('Creating bucket');
    return cos.createBucket({
        Bucket: 'my-bucket',
        CreateBucketConfiguration: {
          LocationConstraint: 'us-standard'
        },
    }).promise();
}

function doCreateObject() {
    console.log('Creating object');
    return cos.putObject({
        Bucket: 'my-bucket',
        Key: 'foo',
        Body: 'bar'
    }).promise();
}

function doDeleteObject() {
    console.log('Deleting object');
    return cos.deleteObject({
        Bucket: 'my-bucket',
        Key: 'foo'
    }).promise();
}

function doDeleteBucket() {
    console.log('Deleting bucket');
    return cos.deleteBucket({
        Bucket: 'my-bucket'
    }).promise();
}

doCreateBucket()
    .then(doCreateObject)
    .then(doDeleteObject)
    .then(doDeleteBucket)
    .then(function() {
        console.log('Finished!');
    })
    .catch(function(err) {
        console.error('An error occurred:');
        console.error(util.inspect(err));
    });
```

## Using Key protect

```javascript
var params = {
  Bucket: 'STRING_VALUE', /* required */
  ACL: private | public-read | public-read-write | authenticated-read,
  CreateBucketConfiguration: {
    LocationConstraint: EU | eu-west-1 | us-west-1 | us-west-2 | ap-south-1 | ap-southeast-1 | ap-southeast-2 | ap-northeast-1 | sa-east-1 | cn-north-1 | eu-central-1
  },
  GrantFullControl: 'STRING_VALUE',
  GrantRead: 'STRING_VALUE',
  GrantReadACP: 'STRING_VALUE',
  GrantWrite: 'STRING_VALUE',
  GrantWriteACP: 'STRING_VALUE',
  IBMServiceInstanceId: 'STRING_VALUE',
  IBMSSEKPEncryptionAlgorithm: 'STRING_VALUE',
  IBMSSEKPCustomerRootKeyCrn: 'STRING_VALUE'
};
s3.createBucket(params, function(err, data) {
   if (err) console.log(err, err.stack); // an error occurred
   else     console.log(data);           // successful response
});
```

* Parameters (new fields only)
`IBMSSEKPEncryptionAlgorithm` (string) – The encryption algorithm that is used for objects stored in the newly created bucket. The default value is `AES256`.
`IBMSSEKPCustomerRootKeyCrn` (string) – Container for describing the KMS-KP Key CRN. The CRN includes version, `cname`, `ctype`, `servicename`, `location`, `scope`, `serviceinstance`, `resourcetype`, `resource`. We pass the CRN as-is.

Callback (callback)

```
function(err, data) { ... }
```
Called when a response from the service is returned. If a callback is not supplied, you must call `AWS.Request.send()` on the returned request object to initiate the request.

Parameters:
- `err (Error)` - the error object returned from the request. Set to null if the request is successful.
- `data (Object)` - the de-serialized data returned from the request. Set to null if a request error occurs.

The data object has the following properties:
- `Location` - (String)
