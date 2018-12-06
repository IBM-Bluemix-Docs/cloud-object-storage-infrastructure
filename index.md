---

copyright:
  years: 2017
lastupdated: "2018-12-05"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# {{site.data.keyword.cos_short}} in the IBM Cloud

{{site.data.keyword.cos_short}} is storage for the cloud.  Essentially a key-value store, files (or any binary data) are given an identifying key (or name) and stored as an 'object' in a uniquely named 'bucket' or 'container'. This allows for highly scalable storage where the only information you need to retrieve your data is the name of the object and the bucket where it's stored.
In addition to {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.cloud_notm}} currently provides several {{site.data.keyword.cos_short}} offerings for different user needs, all of which are accessible through web-based portals and REST APIs.

| Offering                                   | Interface | Defining advantage                             | Docs |
|--------------------------------------------|-----------|------------------------------------------------|------|
| {{site.data.keyword.cos_full_notm}}        | COS API   | Ideal for cloud-native development and provides strong integration with IBM Cloud Services, including Data Science Experience. Most new projects should use this to make use of {{site.data.keyword.iamlong}}, {{site.data.keyword.keymanagementservicelong}}, and other new features as they become available. | [Link](../docs/services/cloud-object-storage/getting-started.html) |
| {{site.data.keyword.cos_full_notm}} (infrastructure)  | COS API   | This version provides certain regulatory compliance only available when purchasing through IBM Cloud Infrastructure.  Does not support {{site.data.keyword.iamlong}} or  {{site.data.keyword.keymanagementservicelong}}. | [Link](quickstart.html) |
| OpenStack Swift (infrastructure)           | Swift API | In addition to using the OpenStack Swift API, this version is available outside of the standard set of IBM Cloud regions. | [Link](../docs/infrastructure/objectstorage-swift/index.html) |
| OpenStack Swift (Cloud Foundry)            | Swift API | This is the original OpenStack Swift {{site.data.keyword.cos_short}} that was provided through IBM Cloud as a Cloud Foundry service. | [Link](../docs/services/ObjectStorage/index.html) |
