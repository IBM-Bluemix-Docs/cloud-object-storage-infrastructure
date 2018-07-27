---

copyright:
  years: 2018
lastupdated: "2018-07-22"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Using CommVault with Archive Tier

CommVault Simpana integrates with Archive tier of COS. For more information about Simpana, see: [CommVault Simpana documentation](https://documentation.commvault.com/commvault/)

## Pre-requisites

Configure Simpana to automatically restore objects from the Archive tier. See the [CommVault Simpana documentation](http://documentation.commvault.com/commvault/v11/article?p=features/cloud_storage/t_restoring_data_amazon_and_oracle.htm) to configure.

## Integration Steps

1.	From the Simpana console, create an Amazon S3cloud storage library. Ensure that the Service Host points to the end point. Simpana provisions buckets at this step or it can consume buckets that are provisioned. 

2.	Create a policy on the bucket. You can use the AWS CLI, SDKs or the portal to create the policy. An example of a policy follows:

```shell
{
  "Rules": [
    {
      "ID": "CommVault",
      "Status": "Enabled",
      "Filter": {
        "Prefix": ""
      },
      "Transitions": [
        {
        "Days": 0,
        "StorageClass": "GLACIER"
        }
      ]
    }
  ]
}
```

To associate the policy with the bucket, execute the following CLI command:

```shell
aws s3api put-bucket-lifecycle-configuration --bucket <bucket name> --lifecycle-configuration file://<saved policy file> --endpoint <end point>
```

3.	Create a storage policy with Simpana and associate the storage policy to the Cloud Storage library that you created in the first step. A storage policy governs the way Simpana interacts with COS for backup transfers. A policy overview can be found [here](https://documentation.commvault.com/commvault/v11/article?p=13804.htm).

4.	Create a Backup Set and associate the backup set to the storage policy created in the previous step. The backup set overview can be found [here](https://documentation.commvault.com/commvault/v11/article?p=11666.htm)

5.	Initiate your backup to the bucket with the policy.

## Performing Backups

You can perform backups to IBM COS. More information on Simpana backups is available [here](https://documentation.commvault.com/commvault/v11/article?p=11677.htm). Backup contents transition to the Archive tier based on the policy configured on the bucket.

## Performing Restores

You can restore backup contents from IBM COS. More information on Simpana restore can be found [here](https://documentation.commvault.com/commvault/v11/article?p=12867.htm).

The backed up contents is restored from the Archive tier to its original tier through a cloud storage recall task. This task is executed once Simpana  receives the return code from COS. More information on Archive recall can be found [here](http://documentation.commvault.com/commvault/v11/article?p=9218.htm).

Once the restoration from the Archive tier to its original tier is complete, Simpana reads the contents and writes to its original or configured location.
