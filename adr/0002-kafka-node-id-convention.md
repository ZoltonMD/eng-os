---
id: adr-0002
title: 'ADR-0002: Kafka node ID Convention'
date: 2025-11-01
status: Accepted
---

# ADR-0002: Kafka node ID Convention (Template)

## Context
To ensure consistent identification of brokers and controllers, we need a unified `node.id` (or `broker.id` in case of 
ZK based cluster) assignment scheme across different locations. This simplifies automation, troubleshooting, 
and other maintenance activities.

## Decision
* Node IDs consist of `2+N` digits. *(where N is the possible max. number of brokers in one rack|dc)*
* The first digit defines the role: `1` for controllers, `2` for brokers
* The second digit defines the location (or rack|dc|az):  
    `1` - Location-1, `2` - Location-2, `3` - Location-3, etc.
* The last two-three digits are the sequential Node (or instance) Number.
* The `Node Number` must be the same as `host_id` in the hostname.

### Example:
We have:
* 6 brokers in 3 DC:
    * srv1-dc1, srv2-dc1;
    * srv1-dc2, srv2-dc2;
    * srv1-dc3, srv2-dc3.
* 3 controllers, started on the first hosts of each DC:
    * srv1-dc1
    * srv1-dc2
    * srv1-dc3
* We know that this cluster never grows to hundreds of brokers.

So, we can use two-digit `Node Number`, and the `node.id` will be distributed as follows:
* **srv1-location1**: broker: `2101`, controller: `1101`;
* **srv2-location1**: broker: `2102`;
* **srv1-location2**: broker: `2201`, controller: `1201`;
* **srv2-location2**: broker: `2202`;
* **srv1-location3**: broker: `2301`, controller: `1301`;
* **srv2-location3**: broker: `2302`.

## Rationale
We wanted a convention that:
* Works for both co-located (controller+broker on the same host) and separated deployments.
* Is human-readable and easy to correlate with physical or cloud nodes.
* Allows future expansion (e.g., new location, roles, brokers) without breaking existing IDs.
* Applicable to ZooKeeper and KRaft based clusters.

## Consequences
* Simplifies node-to-host and node-to-dc|az mapping and troubleshooting.
* Allows predictable node allocation during migration and recovery.
* Requires coordination  when adding new nodes to avoid ID conflicts.
