---
title: DataStax Enterprise for Pivotal Cloud Foundry&reg;
---
<div id="upgrades"></div>
## Upgrades

This product enables a seamless upgrade experience between versions of the product that is deployed through Ops Manager.

The upgrade paths are detailed [here](http://docs.pivotal.io/cassandra/index.html) for each released version.

To upgrade the product:

* The Operator should download the latest version of the product from [Pivotal Network](https://network.pivotal.io/products/p-cassandra)
* Upload the new .pivotal file to Ops Manager
* Upload the stemcell associated with the update (*if required*)
* Update any new mandatory configuration parameters (*if required*)
* Press "Apply changes" and the rest of the process is automated

During the upgrade deployment, we aim to conduct a rolling deployment and follow all DataStax recommend upgrade steps, including disabling the repair service, migrating SSTables and updating packages. See below for more details.

Ops Manager ensures the instances are updated with the new packages and any configuration changes are applied automatically.

Upgrading to a newer version of the product does not cause any loss of data or configuration. This is explicitly tested for during our build and test process for a new release of the product.

### What happens during an upgrade?

1. The repair service is disabled across the cluster
1. On each node:
  * Safe shutdown is initiated via `nodetool disablegossip`, `nodetool disablethrift` and `nodetool drain`
  * The node is stopped
  * Configuration files are backed up
  * Configuration files are updated for the new version of DataStax
  * The DataStax packages are updated
  * The Cassandra process is restarted and is determined to be healthy
  * A snapshot of the data is taken (if there is enough free space to store the snapshot on disk)
  * The SSTables are upgraded
  * The node is started
1. The repair service is reenabled across the cluster

<div id="deployments"></div>
## Rolling deployments

The deployment and upgrade process is designed to only update a single node in the cluster at a time. That node will be fully updated and brought back on-line before BOSH moves onto the next node in the cluster.

We recommend that all applications should use one of the [DataStax Certified Drivers](http://www.datastax.com/download#dl-datastax-drivers), these drivers will handle dropped connections and reconnects automatically and seamlessly in most cases for you, as long as you pass them the array of IPs of each node in the Cassandra cluster.

Combining updating a single node at a time and using a certified driver, along with a well behaved client application it is possible to conduct a rolling deployment and experience minimal if no downtime to your application.

<div id="issues"></div>
## Known issues

On AWS we have observed stale ARP entries remaining in some of the nodes' ARP caches after a node has been updated. This prevents the nodes from being able to communicate with the upgraded node. The Cassandra process will start and the node will appear healthy, but it will not have rejoined the cluster successfully.

We have implemented workarounds to resolve the issue and to also force the local ARP cache to be updated, but we have still witnessed this taking a few minutes to resolve itself.

This can in some cases cause your cluster to lose quorum if you deploy the with default 4 node configuration.

We recommend that you scale your `multi-tenant` cluster to 5 nodes, by increasing the count of the `Multitenant Cassandra Node` to `2` nodes from the default of `1`.

Therefore during an upgrade of a 5 node cluster the following scenario will occur
* Node 1 is updated and brought online - but hasn't yet rejoined the cluster
* Node 2 is taken offline to be updated
* Nodes 3,4,5 are still online and operational - maintaining quorum for reads / writes

<div id="az_awareness"></div>
## Upgraded Cassandra is NOT AZ aware

Your upgraded Cassandra cluster is NOT availability zone aware. If you wish to utilise the multi AZ functionality, you will need to deploy a fresh cluster. 

## Release policy

When a new version of DataStax Enterprise is released we aim to release a new version of the product containing this soon after.

Where there is a new version of DataStax Enterprise or another dependent software component such as the stemcell released due to a critical CVE, Pivotal's goal is to release a new version of the product within 48 hours.
