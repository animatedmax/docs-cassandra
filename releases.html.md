---
title: DataStax Enterprise for Pivotal Cloud Foundry&reg;
---

Release notes for [DataStax Enterprise for Pivotal Cloud Foundry&reg;](https://network.pivotal.io/products/p-cassandra)

### 1.4.0

**Release Date: xx May 2016**

**Stale entries in Address Resolution Protocol (ARP)**

On AWS we have observed stale ARP entries remaining in some of the nodes' ARP caches after a node has been updated. This prevents the nodes from being able to communicate with the upgraded node. The Cassandra process will start and the node will appear healthy, but it will not have rejoined the cluster successfully.

We have implemented workarounds to resolve the issue and to also force the local ARP cache to be updated, but we have still witnessed this taking a few minutes to resolve itself.

There is a risk that with the default 4 node cluster setup, you can lose quorum in the cluster which, depending on the chosen settings in your application, could result in you not being able to read / write data.

To alleviate this, we recommend scaling the cluster to 5 nodes before upgrading to this `1.4.0` tile. This can be achieved by increasing the number of `Multitenant Cassandra Node` to 2 nodes and deploying successfully. This reduces the probability of the cluster losing quorum, but does not eliminate it. However, we have observed the cluster resolve itself in a few minutes.

During an upgrade of a 5 node cluster the following scenario will occur
* Node 1 is updated and brought online - but hasn't yet rejoined the cluster
* Node 2 is taken offline to be updated
* Nodes 3,4,5 are still online and operational - maintaining quorum for reads / writes

Before then upgrading to this `1.4.0` tile, we recommend you log into DataStax OpsCenter and validate that all 5 nodes are online and healthy and are now fully replicated.

**Availability zone awareness**

To benefit from availability zone awareness in your DataStax Enterprise cluster, you will need to delete your existing DataStax Enteprise product and install `1.4.0` as a new product. Upgrading from a previous DataStax Enterprise version will not enable this feature.

**New features**

* Updated stemcell to xxxx
* DataStax Enterprise updated to 4.8.2
* DataStax OpsCenter updated to 5.2.2
* DataStax OpsCenter is now located on its own VM
* DataStax Enterprise is automatically upgraded when moving to this tile version. Including executing all of the recommend upgrade steps **Please refer to the [upgrade documentation](upgrade.html) for more details before executing this upgrade**
* DataStax Enterprise is availability zone aware when installed as a new product
* Support for rolling upgrades
* Suitable for workloads that do not require dedicated resources
* Smoke tests are run after a deployment to perform basic functionality and ensure the cluster is in a healthy state

### 1.3.8
**Release Date: 11th November 2015**

Features included in this release:

* Updated stemcell to 3130. Resolves CVE USN-2806-1.

### 1.3.7
**Release Date: 30th October 2015**

Features included in this release:

* Updated stemcell to 3112
* Fixed bug where long URLs would cause the OpsCenter job to fail
* Updated NTPD to the latest package

### 1.3.6
**Release Date: 6th July 2015**

Features included in this release:

* Support for OpsManager 1.5.x or 1.4.x
* Support for Elastic Runtime 1.5.x or 1.4.x
* Support for HTTPS-only environments
* Support for vSphere or AWS Deployments
* Requires stemcell 2989

### 1.3.5
**Release Date: 17th April 2015**

Features included in this release:

* Support for vSphere & AWS
* Requires OpsManager 1.4.0 and Elastic Runtime 1.4.0 or greater

**Known issues:**

* On AWS, this version supports deployments in the US-East region. Multi-region support is coming in a future release.
* The experimental HTTPS-only feature in Elastic Runtime 1.5 may cause issues with this version of the product. Full support for HTTPS-only traffic is coming in a future release.

<p class="note"><strong>Note</strong>: BOSH Stemcell 2865.1 is required for installation on Ops Manager 1.5.x and above. </p>

### 1.3.4
**Release Date: 24th March 2015**

Features included in this release:

* Updated stemcell to 2889 to resolve [these OpenSSL CVE alerts](http://pivotal.io/security/usn-2537-1)

### 1.3.3
**Release Date: 11th February 2015**

Features included in this release:

* Updated stemcell to 2824 to resolve [CVE-2015-0235 Ghost](http://www.pivotal.io/security/cve-2015-0235)

### 1.3.2
**Release Date: 29th October 2014**

Features included in this release:

* General Availability release
* `development` service plan, providing a 4 node cassandra cluster
  * suitable for development and test workloads
