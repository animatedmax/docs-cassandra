---
title: Using DataStax Enterprise for Pivotal Cloud Foundry&reg;
---

<div id="available"></div>
## Available Plans

There is one available plan:

<table border="1" class="nice">
<tr>
<th><strong>Plan Name</strong></th>
<th><strong>Suitable for</strong></th>
<th><strong>Tenancy Model per Instance</strong></th>
<th><strong>Highly Available</strong></th>
<th><strong>Availability Zone support</strong></th>
<th><strong>Rolling Deployments</strong></th>
<th><strong>Operational Monitoring & Logging</strong></th>
<th><strong>Backup Functionality</strong></th>
</tr>

<tr>
<td><b>multi-tenant</b></td>
<td>Workloads that do not require dedicated resources</td>
<td>Shared Cluster</td>
<td>Yes</td>
<td>
  <ul>
    <li>vSphere - Yes, we recommend 2 AZs</li>
    <li>AWS - No, PCF Ops Manager 1.6 does not support multiple AZ for AWS</li>
  </ul>
</td>
<td>Yes</td>
<td>Syslog for all components</td>
<td>Can be enabled by the Operator in DataStax OpsCenter</td>
</tr>

</table>

<div id="plan"></div>
### Multi-tenant plan features
Key features of this plan are:

* Ability to provision an instance in a shared Cassandra cluster
* Offers redundancy across a 4-node cluster
* Powered by DataStax Enterprise release of Cassandra
* Repair functionality powered by DataStax OpsCenter to ensure your cluster remains healthy
* Suitable for workloads which do not require a dedicated cluster
* Automated upgrades of DataStax Enterprise and migrations of data
* Rolling deployments across the cluster ensuring minimal downtime

<div id='binding'></div>
## Provisioning and Binding

### Using Pivotal Apps Manager

1. From within Pivotal Apps Manager, select Marketplace from the left navigation menu under Spaces. The Services Marketplace displays.
1. Select **DataStax Enterprise** from the displayed tiles and click to view the [available plans](#available).
1. Click on the appropriate **Select this plan** button to select the required **DataStax Service Plan**.
1. In the Instance Name field, enter a name that will identify this specific DataStax service instance.
1. From the Add to Space drop-down list, select the space where you or other users will deploy the applications that will bind to the service.
1. Click the **Add** button.

### Using the CLI

Once you have installed the product, it automatically registers itself with your Elastic Runtime. At this point, the product is available to your application developers, either in the Marketplace in the web based console, or via `cf marketplace`. They can add, provision, and bind the service to their applications like any other CF service:

```
$ cf create-service p-cassandra multi-tenant datastax
$ cf bind-service my-application datastax
$ cf restart my-application
```
