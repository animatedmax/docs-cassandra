---
title: DataStax Enterprise for Pivotal Cloud Foundry&reg;
---
<div id='architecture'></div>
### Architecture
By default the **multi-tenant** plan will configure `3` *seed nodes* and `1` *node* to give you a `4` node cluster in total.

You can increase these values through `OpsManager` on the `Resource Config` tab.
If you wish to scale the cluster we recommend you increase the instance count of the *Multitenant Cassandra Node* job on the resource page in OpsManager.

### Resource Requirements
These are the default resource and IP requirements for installing the tile

<table border="1" class="nice">
	<tr>
		<th>Resource</th>
		<th>Instances</th>
		<th>CPU</th>
		<th>Ram</th>
		<th>Ephemeral</th>
		<th>Persistent</th>
		<th>Static IP</th>
		<th>Dynamic IP</th>
	</tr>
	<tr>
	 	<td>Multitenant Cassandra Seed Node</td>
	 	<td>3</td>
	 	<td>2</td>
	 	<td>4096</td>
	 	<td>8192</td>
	 	<td>8192</td>
	 	<td>1</td>
	 	<td>0</td>
 	</tr>
 	<tr>
 		<td>Multitenant Cassandra Node</td>
 		<td>1</td>
 		<td>2</td>
 		<td>4096</td>
 		<td>4096</td>
 		<td>8192</td>
 		<td>1</td>
 		<td>0</td>
 	</tr>
	<tr>
 		<td>DataStax OpsCenter</td>
 		<td>1</td>
		<td>4</td>
 		<td>4096</td>
 		<td>4096</td>
 		<td>4096</td>
 		<td>1</td>
 		<td>0</td>
 	</tr>
 	<tr>
 		<td>Cassandra Broker</td>
 		<td>1</td>
 		<td>2</td>
 		<td>1024</td>
 		<td>4096</td>
 		<td>1024</td>
 		<td>1</td>
 		<td>0</td>
 	</tr> 	 	
	<tr>
		<td>Broker Registrar</td>
		<td>1</td>
		<td>1</td>
		<td>1024</td>
		<td>2048</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Broker De-Registrar</td>
		<td>1</td>
		<td>1</td>
		<td>1024</td>
		<td>2048</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Smoke tests</td>
		<td>1</td>
		<td>1</td>
		<td>1024</td>
		<td>2048</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Compliation</td>
		<td>2</td>
		<td>2</td>
		<td>1024</td>
		<td>8192</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
	</tr>
</table>

#### Notes:
* The `multi-tenant` plan consists of the `Multitenant Cassandra Seed Node` and `Multitenant Cassandra Node` resources

<div id='limitations'></div>
### Known Limitations

Limitations with the current Cassandra product include:

* Users are able to list all keyspaces in the cluster, including keyspaces that belong to other users. Keyspaces have random names. This is a Cassandra limitation.
* Users are able to list all tables in all keyspaces, including keyspaces that belong to other users. Users cannot access data in tables outside of their keyspace. This is a Cassandra limitation.
* Users cannot provision multiple keyspaces in a single service instance. They can provision multiple instances, each with their own keyspace.
* Constraining CPU, memory and/or disk usage is not supported.
