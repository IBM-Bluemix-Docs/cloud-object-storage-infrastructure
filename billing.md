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


# Billing

For more information about pricing, see the [IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/).

## Invoices
Account invoices can be found at **Account** > **Billing** > **Invoices** in the navigation menu.

Each account receives a single bill. If you need separate billing for different sets of containers, then creating multiple accounts is necessary.
{:tip}

## How does IBM COS pricing work?

Storage costs for {{site.data.keyword.cos_full}} are determined by total volume of data stored, the amount of public outbound bandwidth consumed, and the total number of operational requests processed by the system.

{{site.data.keyword.Bluemix_short}} offerings are connected to a three-tiered network, segmenting public, private, and management traffic. Infrastructure on a customer's {{site.data.keyword.Bluemix_short}} account may transfer data between one another across the private network at no cost. Infrastructure offerings (such as bare metal servers, virtual servers, and cloud storage) connect to other applications and services in the {{site.data.keyword.Bluemix_short}} catalog (such as Watson services, containers, runtimes) across the public network, so data transfer between those two types of offerings is metered and charged at standard public network bandwidth rates.
{:tip}

## What is the difference between 'Class A' and 'Class B' requests?

'Class A' requests are operations that involve modification or listing. This category includes creating buckets, uploading or copying objects, creating or changing configurations, listing buckets, and listing the contents of buckets.

'Class B' requests are those related to retrieving objects or their associated metadata and configurations from the system.

There is no charge for deleting buckets or objects from the system.

| Class | Requests | Examples |
|--- |--- |--- |
| Class A | PUT, COPY, and POST requests, as well as GET requests used to list buckets and objects | Creating buckets, uploading or copying objects, listing buckets, listing contents of buckets, setting ACLs, and setting CORS configurations |
| Class B | GET (excluding listing), HEAD, and OPTIONS requests | Retrieving objects and metadata |

## What is the difference between the Standard, Vault, and Flex billing tiers?

Vault billing is a way to control costs for infrequently accessed data, such as compliance or backup data. These objects incur lower storage costs but higher costs for operational requests. Unlike the Standard billing tier, additional costs are incurred on a per-GB basis for objects retrieved from the system. Flex billing is intended for use when data access patterns are difficult to predict, and pricing is optimized based on frequency of access.

## Archiving Data

Archive is our lowest cost option for data that is rarely accessed. For more information, see the [pricing page](https://www.ibm.com/cloud/object-storage/pricing/).
