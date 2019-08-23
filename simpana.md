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


# Using Commvault Simpana with the Archive tier

Commvault Simpana integrates with the Archive tier of {{site.data.keyword.cos_full_notm}}. For more information about Simpana, see [Commvault Simpana documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/)

For more information about {{site.data.keyword.cos_full_notm}} Infrastructure Archive, see [How to archive data](/docs/infrastructure/cloud-object-storage-infrastructure?topic=cloud-object-storage-infrastructure-archiving-data).

## Integration steps

1.	From the Simpana console, create an Amazon S3 cloud storage library.

2. Ensure that the Service Host points to the endpoint. Simpana provisions buckets at this step or it can consume provisioned buckets.

3.	Create a policy on the bucket. You can use the AWS CLI, SDKs or the web console to create the policy. An example of a policy follows:

```shell
{
  "Rules": [
    {
      "ID": "Commvault",
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

### To associate the policy with the bucket

1.  Execute the following CLI command:

```shell
aws s3api put-bucket-lifecycle-configuration --bucket <bucket name> --lifecycle-configuration file://<saved policy file> --endpoint <end point>
```

2.	Create a storage policy with Simpana and associate the storage policy to the Cloud Storage library that you created in the first step. A storage policy governs the way Simpana interacts with COS for backup transfers. A policy overview can be found [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://documentation.commvault.com/commvault/v11/article?p=13804.htm).

3.	Create a backup set and associate the backup set to the storage policy created in the previous step. The backup set overview can be found [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/v11/article?p=11666.htm)

## Performing backups

You can initiate your backup to the bucket with the policy and perform backups to {{site.data.keyword.cos_full_notm}}. For more information about Simpana backups, see [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/v11/article?p=11677.htm). Backup contents transition to the Archive tier based on the policy configured on the bucket.

## Performing restores

You can restore backup contents from {{site.data.keyword.cos_full_notm}}. For more information about Simpana restores, see [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/v11/article?p=12867.htm).

### Configure Simpana to automatically restore objects from the Archive tier

1. Create a task that triggers {{site.data.keyword.cos_full_notm}} restore when you restore a backup from {{site.data.keyword.cos_short}}. For more information, see the [Simpana documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/v11/article?p=features/cloud_storage/t_restoring_data_amazon_and_oracle.htm).

2. Restore backed up contents from the Archive tier to its original tier through a cloud storage recall task. This task is executed once Simpana receives the return code from {{site.data.keyword.cos_full_notm}}. For more information about Archive recall, see [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://documentation.commvault.com/commvault/v11/article?p=9218.htm).

3. Once the restoration (from the Archive tier to its original tier) is complete, Simpana reads the contents and writes to its original or configured location.
