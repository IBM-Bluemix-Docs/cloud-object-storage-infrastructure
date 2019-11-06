---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2018-08-22"

subcollection: cloud-object-storage-infrastructure

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}

# Select regions and endpoints

A bucket's resiliency is defined by the endpoint used to create it.  _Cross Region_ resiliency will spread your data across several metropolitan areas, while _Regional_ resiliency will spread data across a single metropolitan area.  _Single Data Center_ resiliency spreads data across multiple appliances within a single data center.  Regional and Cross Region buckets can maintain availability during a site outage.

Compute workloads that are colocated with a Regional {{site.data.keyword.cos_short}} endpoint result in lower latency and better performance. For workloads not concentrated in a single geographic area, a Cross Region `geo` endpoint routes connections to the nearest regional data centers.

When you use a Cross Region endpoint, it is possible to direct inbound traffic to a specific access point while still distributing data across all three regions. When you send requests to an individual access point there is no automated failover if that region becomes unavailable.  Applications that direct traffic to an access point instead of the `geo` endpoint **must** implement appropriate failover logic internally to achieve the availability advantages of the cross-region storage.
{:tip}

Some workloads may benefit from using a Single Data Center endpoint.  Data stored in a single site is still distributed across many physical storage appliances, but is contained to a single data center.  This can improve performance for compute resources within the same site, but will not maintain availability in the case of a site outage.  Single Data Center buckets do not provide automated replication or backup in the case of site destruction, so any applications using a single site should consider disaster recovery in their design.

Types of endpoint:

{{site.data.keyword.cloud}} services are connected to a three-tiered network, segmenting public, private, and management traffic.

* **Private endpoints** are available for requests originating from Kubernetes clusters, bare metal servers, virtual servers, and other cloud storage services. Private endpoints provide better performance and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers. **Whenever possible, it is best to use a private endpoint.**
* **Public endpoints** can accept requests from anywhere and charges are assessed on outgoing bandwidth. Incoming bandwidth is free. Public endpoints should be used for access not originating from an {{site.data.keyword.cloud_notm}} cloud computing resource.  **Note**: Cloud Foundry applications are unable to access the private network, so data transfer is metered and charged at standard public network bandwidth rates.

As of December 2018, we have updated our endpoints. Legacy endpoints will continue to work until further notice. Please update your applications to use the new endpoints listed below.
{:note}

## Regional Endpoints
{: #endpoints-region}

Buckets that are created at a regional endpoint distribute data across three data centers that are spread across a metro area. Any one of these data centers can suffer an outage or even destruction without impacting availability.

<table>
  <thead>
    <tr>
      <th>Region</th>
      <th>Type</th>
      <th>Endpoint</th>
    </tr>
  </thead>
  <tbody>
    <caption>Regional Endpoints</caption>
    <tr>
      <td>US South</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.us-south.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.us-south.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>US East</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.us-east.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.us-east.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>EU United Kingdom</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.eu-gb.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.eu-gb.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>EU Germany</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.eu-de.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.eu-de.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>AP Australia</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.au-syd.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.au-syd.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>AP Japan</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.jp-tok.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.jp-tok.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


## Cross Region Endpoints
{: #endpoints-geo}

Buckets that are created at a cross region endpoint distribute data across three regions. Any one of these regions can suffer an outage or even destruction without impacting availability. Requests are routed to the nearest region's data center by using Border Gateway Protocol (BGP) routing. In an outage, requests are automatically rerouted to an active region. Advanced users who want to write their own failover logic can do so by sending requests to a [specific access point](/docs/services/cloud-object-storage/info?topic=cloud-object-storage-advanced-endpoints) and bypassing the BGP routing.

<table>
  <thead>
    <tr>
      <th>Region</th>
      <th>Type</th>
      <th>Endpoint</th>
    </tr>
  </thead>
  <tbody>
    <caption>Cross Region Endpoints</caption>
    <tr>
      <td>US Cross Region</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.us.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.us.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>EU Cross Region</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.eu.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.eu.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>AP Cross Region</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.ap.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.ap.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>




## Single Data Center Endpoints
{: #endpoints-zone}

Single data centers are not colocated with IBM Cloud services, such as IAM or Key Protect, and offer no resiliency in a site outage or destruction. 

If a networking failure results in a partition where the data center is unable to access IAM, authentication and authorization information is read from a cache that might become stale. This cached data might result in a lack of enforcement of new or altered IAM policies for up to 24 hours.
{:important}

<table>
  <thead>
    <tr>
      <th>Region</th>
      <th>Type</th>
      <th>Endpoint</th>
    </tr>
  </thead>
  <tbody>
    <caption>Table 3: Single Data Center Endpoints</caption>
    <tr>
      <td>Amsterdam, Netherlands</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.ams03.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.ams03.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Chennai, India</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.che01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.che01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Hong Kong S.A.R. of the PRC</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.hkg02.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.hkg02.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Melbourne, Australia</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.mel01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.mel01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Mexico City, Mexico</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.mex01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.mex01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Milan, Italy</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.mil01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.mil01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Montréal, Canada</td>
      <td>
        <p>Public</p>
        <p>Private</p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.mon01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.mon01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Oslo, Norway</td>
      <td>Public</td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.osl01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.osl01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Paris, France</td>
      <td>Public</td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.par01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.par01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>San Jose, US</td>
      <td>Public</td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.sjc04.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.sjc04.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr> 
      <td>São Paulo, Brazil</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.sao01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.sao01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Seoul, South Korea</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.seo01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.seo01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>Toronto, Canada</td>
      <td>
        <p>Public</p>
        <p>Private
        </p>
      </td>
      <td>
        <p>
          <code class="highlighter-rouge">s3.tor01.cloud-object-storage.appdomain.cloud</code>
        </p>
        <p>
          <code class="highlighter-rouge">s3.private.tor01.cloud-object-storage.appdomain.cloud</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

## EU-Managed Endpoints
{: #endpoints-eu-managed}

The Activity Tracker and Logging Service with LogDNA can archive to a bucket at specific {{site.data.keyword.cos_full}} instances. This table shows the EU-Managed locations of {{site.data.keyword.cos_full}} instances for archiving events.

| COS bucket location | Resiliency | City |
|----|----|---
| `ams03` | Single Site | Amsterdam |
| `eu-de` | Regional | Frankfurt |
| `eu-gb` | Regional | London |
| `mil01` | Single Site | Milan |
| `osl01` | Single Site | Oslo |
| `par01` | Single Site | Paris |
| `eu-geo` | Cross Region | Amsterdam, Frankfurt, Milan |
{: caption="EU-managed Endpoints"}