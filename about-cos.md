---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2018-08-22"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# About {{site.data.keyword.cos_full_notm}} (Classic)

Information stored with {{site.data.keyword.cos_full}} is encrypted and dispersed across multiple geographic locations, and accessed over HTTP using a REST API. This service uses distributed storage technologies that are provided by the {{site.data.keyword.cos_full_notm}} System (formerly Cleversafe).

{{site.data.keyword.cos_full_notm}} is available with three types of resiliency: Cross Region, Regional, and Single Data Center. Cross Region provides higher durability and availability than using a single region at the cost of slightly higher latency, and is available today in the US and the EU. Regional service reverses those tradeoffs, and distributes objects across multiple availability zones within a single region. Regional service is available in the US South and US East regions. If a region or availability zone is unavailable, the object store continues to function without impediment. Single Data Center distributes objects across multiple machines within the same physical location.

Developers use an {{site.data.keyword.cos_full_notm}} API to interact with their {{site.data.keyword.objectstorageshort}}. This documentation provides support to [get started](/docs/infrastructure/cloud-object-storage-infrastructure/quickstart.html) with provisioning accounts, creating buckets, uploading objects, and using common API interactions.
