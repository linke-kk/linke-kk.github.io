---
layout: default
title: Distributed Systems:TensorFlow
---
# TensorFlow: A system for large-scale machine learning
## Parallel Training
- Data Parallel
Train on different shards of training data in parallel
- Model Parallel
Train different parts of the model in parallel, may need communication between parts
## Parameter Server
Each computation cluster report parameter update to the parameter server using put() \\
Each computation cluster fetch up-to-date parameter from the parameter server using get()

### Why not parameter server (DistBelief) ?


## Key Distribution
- Dataflow Graph
"Tensorflow uses a unified dataflow graph to represent both the computation in an algorithm and the state on which the algorithm operates."


## Dataflow
### Dataflow Systems
- Theano
- MapReduce
- Dryad
#### Traditional Dataflow Systems
"Graph vertices represent functional computation on immutable data"
#### Tensorflow
Vertex: "TensorFlow allows vertices to represent computations that own or update mutable state." \
Edge: "Edges carry tensors (multi-dimensional arrays) between nodes, and TensorFlow transparently inserts the appropriate commmunication between distribued subcomputations."
## Parameter Server Architecture
What is parameter servers?
"A job comprises two disjoint sets of processes"
- stateless worker processes
"Perform the bulk of the computation when training a model"
- stateful parameter server processes
"maintain the current version of the model parameters"
### Consistency
"Because the parameter updates in many algoriths are commutative and have weak consistency requirements, the worker processes can compute updates independently and write back "delta" updates to each parameter server, which combines the updates with its current state."
### Limitations
- Defining new layer needs C++
- Refining the training algorithms involves modifying the parameter server implementation


- Adam
- 

## Synchrounous Replication

## Consistency
