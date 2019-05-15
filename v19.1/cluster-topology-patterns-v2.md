---
title: Topology Patterns
summary:
toc: true
---

This section covers recommended topology patterns for running CockroachDB in a cloud environment, each with latency and resiliency characteristics and required configurations.

Use the matrix below to choose the pattern that matches your requirements:

Pattern | App Location | Latency | Resiliency
--------|--------------|---------|-----------
[Development](single-region-topologies.html#development.html) | Laptop, etc. | Fast reads<br>Fast writes | N/A
[Basic Production](single-region-topologies.html#basic-production) | Single region | Fast reads<br>Fast writes | 1 AZ failure
[Follow-the-workload](multi-region-topologies.html#follow-the-workload) | Multiple regions | Fast reads in most active region<br>Slower reads in other regions<br>Slower writes | 1 region failure
[Geo-Partitioning](multi-region-topologies.html#geo-partitioning) | Multiple regions | Fast reads<br>Fast writes | 1 AZ failure per partition
[Pinned Secondary Indexes](multi-region-topologies.html#pinned-secondary-indexes) | Multiple regions | Fast reads<br>Slower writes | 1 AZ failure
[Follower Reads](multi-region-topologies.html#follower-reads) | Multiple regions | Fast reads (stale)<br>Slower writes | 1 region failure

Keep in mind that multiple patterns can be used a single deployment of CockroachDB. For example, for a multi-region deployment, you might use the [Geo-Partitioning](multi-region-topologies.html#geo-partitioning) pattern for frequently updated tables that are geographically specific and the [Region-Specific Secondary Indexes](multi-region-topologies.html#pinned-secondary-indexes) pattern for seldom updated tables (e.g., reference tables) that are not tied to geography.

<!-- Pattern | Client Location | Latency | Data Resiliency | Configuration
--------|-----------------|---------|-----------------|--------------
[Development](single-region-topologies.html#development.html) | Laptop, etc. | Fast reads<br>Fast writes | N/A | 1 node<br>No replication
[Basic Production](single-region-topologies.html#basic-production) | Single region | Fast reads<br>Fast writes | 1 AZ failure | 3 AZs<br>3+ nodes<br>3-way replication
[Follow-the-workload](multi-region-topologies.html#follow-the-workload) | Multiple regions | Fast reads in most active region<br>Slower reads in other regions<br>Slower writes | 1 region failure
[Geo-Partitioning](multi-region-topologies.html#geo-partitioning) | Multiple regions | Fast reads<br>Fast writes | 1 AZ failure per partition
[Pinned Secondary Indexes](multi-region-topologies.html#pinned-secondary-indexes) | Multiple regions | Fast reads<br>Slower writes | 1 AZ failure
[Follower Reads](multi-region-topologies.html#follower-reads) | Multiple regions | Fast reads (stale)<br>Slower writes | 1 region failure -->

<!-- Client Location | Read Latency | Write Latency |Data Resiliency | Pattern
----------------|--------------|---------------|----------------|--------
Dev environment | Low | Low | N/A | [Single Node](single-node-toplogy.html)
Single region | Low | Low | 1 AZ failure | [Multiple Availability Zones](single-region-topologies.html#multiple-availability-zones)
Multiple regions | Low (for most active region) | High | 1 region failure |  [Follow-the-workload](multi-region-topologies.html#follow-the-workload)
Multiple regions | Low | Low | 1 AZ failure per partition | [Geo-Partitioning](multi-region-topologies.html#geo-partitioning)
Multiple regions | Low | High | 1 region failure | [Pinned Secondary Indexes](multi-region-topologies.html#pinned-secondary-indexes)
Multiple regions | Low (Stale) | High | 1 region failure | [Follower Reads](multi-region-topologies.html#follower-reads) -->
