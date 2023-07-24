Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing

Two types of aaplications that current computing frameworks handle inefficiently
1. Iterative Algorithms
PageRank, K-means
2. Interactive Data Mining Tools
"where a user runs multiple ad-hoc queries on the same subset of the data"
Why?
Reuse intermediate results. 
How in traditional systems?
Reuse data between two MapReduce jobs. -> write it to an external stable storage system, e.g. a distributed file system
Ways to tackle it is by keeping the intermediate result in memory.

"In this paper, we propose a new abstraction called resillient distributed datasets (RDDs) that enables efficient data reuse in a broad range of applications."
What is abstraction?

How is fault toleratn provided?
Replicating the data across machines or to log updates across machines. -----> Expensive for data-intensive workloads, copying large amounts of data over the cluster network, network bandwidth < RAM

If a partition of an RDD is lost, how does the system recover?
"If a partition of an RDD is lost, the RDD has enough information about how it was derived from other RDDs to recompute just that partition." ?

Lineage?
"RDDs do not need to be materialized at all times. Instead, an RDD has enough information about how it was derived from other datasets (its lineage) to compute its partitions from data in stable storage"

Transformation
E.g. map, filter, and join

"Each dataset is represented as an object and transformantions are invoked using methods on these objects."

.persist()
Indicate which RDDs they want to reuse in future operations.

closure?

Dependencies
1. Narrow Dependency
2. Wide Dependency
