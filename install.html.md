---
title: Installing DataStax Enterprise for Pivotal Cloud Foundry&reg;
---

<div id="steps"></div>
## Installation Steps

To install DataStax Enterprise for PCF, follow the procedure for installing Pivotal Ops Manager tiles:

1. Download the product file from [Pivotal Network](https://network.pivotal.io/).
1. Upload the product file to your Ops Manager installation.
1. Click **Add** next to the uploaded product description in the Available Products view to add this product to your staging area.
1. Click the newly added tile to review any configurable options.
1. Click **Apply Changes** to install the service.

<div id="making_changes"></div>
## Making changes to an existing installation

Your installed Cassandra cluster is availability zone aware. If you make changes to your installation's availability zones, please be
aware that you will need to manually run a [sequential repair](http://docs.datastax.com/en/cassandra/2.1/cassandra/operations/opsRepairNodesManualRepair.html) and [cleanup process](http://docs.datastax.com/en/cassandra/2.1/cassandra/tools/toolsCleanup.html) on each node before your cluster is ready for use. For more information please see the Datastax documentation on [topology changes](http://docs.datastax.com/en/cassandra/2.1/cassandra/operations/opsMoveNodeRack.html).

<div id="data_center_name"></div>
## Data Center Name

Once the data center name has been set for a deployment, it must not be changed. Any attempt to change the data center name of
an existing deployment will result in a deployment failure, since the deployment will prevent the change from being applied in
order to protect your data. 

Should you accidentally change the name and encounter this scenario, you can recover your deployment simply by resetting the
data center name back to its original value, and clicking 'Apply changes'.

<div id="example"></div>
## Example Application

To help your application developers get started with DataStax Enterprise for PCF, we have provided an example application, which can be [downloaded here](https://github.com/pivotal-cf/cf-cassandra-example-app/archive/master.zip).
