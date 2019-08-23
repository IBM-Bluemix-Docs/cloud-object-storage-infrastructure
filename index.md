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


# {{site.data.keyword.cos_short}} in the IBM Cloud

{{site.data.keyword.cos_short}} is storage for the cloud. Essentially, it is a key-value store, where files (or any binary data) are given an identifying key (or name), and are stored as an 'object' in a uniquely named 'bucket' or 'container'. This feature allows for highly scalable storage where the only information you need to retrieve your data is the name of the object and the bucket where it is stored.

| Offering                                   | Interface | Defining advantage                             | IBM Docs |
|--------------------------------------------|-----------|------------------------------------------------|------|
| {{site.data.keyword.cos_full_notm}}        | COS API   | Ideal for cloud-native development and provides strong integration with IBM Cloud Services, including Data Science Experience. Most new projects can benefit from using this offering with {{site.data.keyword.iamlong}}, {{site.data.keyword.keymanagementservicelong}}, and other new features as they become available. | [Link](../docs/services/cloud-object-storage/getting-started.html) |
| {{site.data.keyword.cos_full_notm}} (Classic)  | COS API   | This version provides certain regulatory compliance only available when you purchase it through IBM Cloud Infrastructure.  Does not support {{site.data.keyword.iamlong}} or {{site.data.keyword.keymanagementservicelong}}. | [Link](/docs/infrastructure/cloud-object-storage-infrastructure?topic=cloud-object-storage-infrastructure-quickstart-guide) |
