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

<div id="example"></div>
## Example Application

To help your application developers get started with DataStax Enterprise for PCF, we have provided an example application, which can be [downloaded here](https://github.com/pivotal-cf/cf-cassandra-example-app/archive/master.zip).
