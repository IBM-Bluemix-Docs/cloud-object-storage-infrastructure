---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# Ordering {{site.data.keyword.cos_full_notm}} (Classic)

Until recently, IBM offered Platform-as-a-Service and Infrastructure-as-a-Service in two distinct environments: [{{site.data.keyword.cloud_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/){: new_window} and [{{site.data.keyword.cloud_notm}} Infrastructure ![External link icon](../../icons/launch-glyph.svg "External link icon")](www.softlayer.com){:new_window}. The {{site.data.keyword.cloud_notm}} provided a robust application development platform with direct access to cutting edge IBM technologies and DevOps services. {{site.data.keyword.cloud_notm}} Infrastructure provided access to infrastructure services, such as bare metal or virtual servers, data storage, and networking.

Now these lines are dissolving as all offerings are integrated into [the {{site.data.keyword.cloud_notm}} catalog of services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/){: new_window}. Existing `SoftLayer` customers are encouraged to take advantage of [an IBMid for single-sign-on authentication ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://blog.softlayer.com/2016/new-softlayer-accounts-now-ibmid-authentication){: new_window}, and it is possible to [link existing `SoftLayer` and {{site.data.keyword.cloud_notm}} accounts ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://blog.softlayer.com/2016/meet-integrated-ibm-cloud-platform-softlayer-and-bluemix){: new_window}.


## Creating an {{site.data.keyword.cloud_notm}} account

Before you can order a storage account, it is necessary to create a customer account first.

1. Go to [{{site.data.keyword.cloud_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window} and click the **Create a Free Account** button.
2. Complete the form, by providing your email address, name, region, and phone number. Choose a password.
3. Follow the link provided by the confirmation email, and follow the links to log in to {{site.data.keyword.Bluemix}}.
4. Before you can use the {{site.data.keyword.Bluemix}}, you need to set up a basic development environment. Choose a region based on your geographic location, and choose a name for your organization. Don't worry about being perfect - you can change it or create more organizations later. Follow the **Create** link.
5. Now you need to name your first development space. This name can be changed at any time. After you chose a name, follow the **Create** link.
6. Follow the **I'm Ready** link to get started with {{site.data.keyword.Bluemix}}.
7. Ordering infrastructure services requires upgrading to a Pay-As-You-Go account. Upgraded accounts still receive runtime and service allowances, and are only charged for resources that were used. Go to the {{site.data.keyword.Bluemix}} catalog, and follow the link for **Cloud Object Storage - S3 API**.
8. Follow the **Upgrade** link.
9. Complete the Contact and Billing information forms, check the box to acknowledge Cloud Service terms, and follow the **Submit Order** link.
10. Follow the **Done** link, and wait for an email that confirms your account upgrade.

## Creating an {{site.data.keyword.objectstorageshort}} account

Accounts are limited to 100 {{site.data.keyword.cos_full}} accounts. If more storage accounts are needed, contact customer support.
{:tip}

Existing `SoftLayer` customers can log in to [{{site.data.keyword.slportal}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){:new_window}, but are encouraged to create an IBMid and explore the {{site.data.keyword.Bluemix}} catalog. Both control portals are equivalent in functionality and differ only in their header design and branding.
1. Log in to [https://control.bluemix.net/ ![External link icon](../../icons/launch-glyph.svg "External link icon"))](https://control.bluemix.net/){: new_window}.
2. Navigate to the {{site.data.keyword.objectstorageshort}} page, by clicking **Storage** > **{{site.data.keyword.objectstorageshort}}** in the Navigation menu.
3. Click the **order {{site.data.keyword.objectstorageshort}}** link on the upper right to open the order menu.
4. Select **{{site.data.keyword.cos_full_notm}}** in the **Storage Type** menu.
5. Click **Continue** and accept the Master Service Agreement before you complete the order. The new {{site.data.keyword.objectstorageshort}} account is provisioned momentarily and shows ups in the objects list when it is done.

You can archive rarely accessed data. Archive works with existing storage-class tiers, as a result, you can reduce storage costs even further by storing data offline with our lowest-priced storage. For more information, see [Archiving data](archiving.html).
{:tip}
