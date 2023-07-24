---
layout: default
title: Distributed Systems:Memcached
---
# Scaling Memcache at Facebook
## Memcached
An open-source implementation of an in-memory hash table
### Operations
- set
- get
- delete

## Demand-filled Look-aside Cache
- Demand-filled: Reader will trigger filling the cache
- Look-aside:

## Objectives
- Reduce the latency of fetching cached data
- Reduce the load imposed due to a cache miss
### Reducing Latency
### Reducing Load
#### Problems
##### Stale sets
"A stale set occurs when a web server sets a value in memcache that does not reflect the latest value that should be cached." \\
How can this happen? \\
"This can occur when concurrent updates to memcache get reordered." \\
Web Server 1 get(key) --> Cache miss in MC --> DB return A --> Some one update key from A to B --> Web Server 2 get(key) --> Cache miss in MC --> DB return B
--> Web Server 2 set(key, B) --> Web Server 1 set(key, A) \\
set is reordered, this can happen when web server 1 is slow \\
Result: DB(key: B), MC(key: A) --> Inconsistency
##### Thundering Herds
"A thundering herd happens when a specific key undergoes heavy read and write activity." \\
write invalidate memcache --> read bring it to memcache --> write invalidate memcache \\
Ping pong effect \\

delete is not actually deleted, but mark the entry as stale instead \\
get may be marked, saying stale data can be tolerated \\
Clients given a choice of using a slightly stale value or waiting

#### Leases
"Only one web server is allowed to set this key at once"
##### How does it solve stale sets
MC server returns Web Server a lease when a cache miss happened --> Any delete happened between the lease grant and set operation invalidate the lease \\
Why? Delete operation indicates that an updates may happen between read from DB and set to MC. If so, the set operation that happens after delete operation will make the MC entry stale.

## Failure Handling
Cannot treat no response from MC server as cache miss --> Will lead to DB server overload
MC server no response is probably becuase it is overloaded --> If another MC server becomes responsible for the key space of the failed MC server, that MC server will also be overloaded --> lead to cascading failure

## Mutiple Clusters
Cluster 1: Web Servers + MC Servers \  \\
                                     ---- DB Servers \\
Cluster 2: Web Servers + MC Servers /  \\
### Who invalidates the cache?
DB Server --> Because we want to maintain independence between clusters \\

### Cold Cluster Warmup
Cluster bootup will overload DB servers --> Fetch from a Warm Cluster's MC servers \\
Race condition: DB (k: v1) MC in warm cluster (k: v1) --> C1 in cold cluster updates k to v2 --> DB (k: v2) --> C1 delete(k) in cold cluster --> C2 in cold cluster get(k) --> MC miss 
--> C2 v1 = get(k) from warm cluster instead of DB server --> MC hits --> C2 set(k, v1) into cold cluster --> Cluster 1 MC server inconsistent with DB Server \\
Solution: deletes to the cold cluster's Memcached servers have two-second holdoff

## Geographically Distributed Database
Remote marked in MC Server \\
Read miss path:
If marker set, read from master DB \\
Else, read from replica DB \\
Master DB always represent up-to-date DB
