# Availability

<!-- TOC -->
* [Availability](#availability)
  * [Definition](#definition)
  * [Availability patterns](#availability-patterns)
    * [Fail-over](#fail-over)
      * [Active-Passive / Master-Slave](#active-passive--master-slave)
      * [Active-Active / Master-Master](#active-active--master-master)
    * [Replication](#replication)
  * [In Parallel vs In Sequence](#in-parallel-vs-in-sequence)
<!-- TOC -->

## Definition

Availability is defined on the [CAP Theorem](../cap) as:

Every request receives a response, without guarantee that it contains the most recent version of the information.

## Availability patterns

There are two complementary patterns to support *high availability*: **fail-over** and **replication**.

### Fail-over

Fail-over presents some **disadvantages**:

* Adds more hardware and additional complexity.
* There is a potential for loss of data if the active system fails before any newly written data can be replicated to the passive.

#### Active-Passive / Master-Slave

With *Active-Passive Fail-over*, heartbeats are sent between the active and the passive server on standby. If the heartbeat is interrupted, the passive server takes over the active's IP address and ersumes service.

The length of downtime is determined by whether the passive server is already runnin in *"hot"* standby or whether it needs to start up from *"cold"* standby. Only the active server handles traffic.

#### Active-Active / Master-Master

In *Active-Active Fail-over*, both servers are managing traffic, spreading the load between them.

if the servers are public-facing, the DNS would need to know about the public IPs of both servers. If the servers are internal-facing, application logic would need to know about both servers.

### Replication

See [Replication in Databases](../../databases/replication).

## In Parallel vs In Sequence

If a service consists of multiple components prone to failure, the service's overall availability depends on whether the components are in sequence or in parallel

* In Sequence: `Availability (Total) = Availability (c1) * Availability (c2) * ...`

* In Parallel: `Availability (Total) = 1 - (1 - Availability (c1)) * (1 - Availability (c2)) * ...`
