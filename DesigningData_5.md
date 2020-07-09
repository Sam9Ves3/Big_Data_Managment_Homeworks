----------------------------
# Designing Data-Intensive Applications
----------------------------

## Chapter 5: Replication

**1. What are the three main reasons to distribute a database across multiple
machines?**

1. Scalability: if your data volume or your query throughput grows bigger than a single machine can handle, you can
potentially spread the load across multiple machines.

2. Fault tolerance/high availability: if your application needs to continue working, even if one machine (or several machines, or an entire
datacenter) goes down, you can use multiple machines to give you redundancy. When one fails,
another one can take over.

3. Latency: if you have users around the world, you might want to have have servers at various locations
worldwide, so that users can be served from a datacenter that is geographically close to them. That
avoids the user having to wait for network packets to travel halfway around the world.


**2. What is refered as *a shared-memory architecture* in the chapter context?**

Join many CPUs, RAM chips and disks together under one operating system, and a fast 
interconnect that allows any CPU to access any part of memory or disk.

**3. What is the *shared-disk architecture* approach?**

Approach which uses several machines with independent CPUs and RAM, but stores data on
an array of disks that is shared between the machines, connected via a fast network.

**4. What is the *shared-nothing architectures* approach?**

In this approach, each machine or virtual machine running the database software is called a node. Each node uses
uses its CPUs, RAM and disks independently. Any coordination between nodes is done at the software level, using a conventional network.
No special hardware is required by a shared-nothing system and it can potentially distribute data across multiple
geographic regions, and thus reduce latency for users and potentially be able to survive the loss
of an entire datacenter.

**5. What are the two ways of distribute data across multiple nodes?**

1. Replication: keeping a copy of the same data on several different nodes, potentially in different locations.
Replication provides redundancy: if some nodes are unavailable, the data can still be served from the
remaining nodes. Replication can also help improve performance.

2. Partitioning: splitting a big database into smaller subsets called partitions, so that different partitions can be
assigned to different nodes (also known as *sharding*).


**6. What is the process of the *leader-based replication*?**

1. One of the replicas is designated the leader (also known as master or primary). When clients want to
write to the database, they must send their query to the leader, which first writes the new data to its
local storage.

2. The other replicas are known as followers (read replicas, slaves, or hot standbys[128]). Whenever the
leader writes new data to its local storage, it also sends the data change to all of its followers. Each
follower takes the stream of changes from the leader and updates its local copy of the database
accordingly.

3. When a client wants to read from the database, it can query either the leader or any of the followers.
However, writes are only accepted on the leader (the followers are read-only from the client’s point of
view).



**7. How do we differentiate *synchronous* replication from the *asynchronous*?**

For example, when replication is *synchronous*, the leader waits until followers have confirmed that they received the 
write before reporting success to the user. When the leader sends the message, but doesn’t wait for a
response from the follower is *asynchronous* replication


**8. What can we consider as the main advantage of *synchronous* replication?**

The follower is guaranteed to have an up-to-date copy of the data that is consistent with the leader. 
If the leader suddenly fails, we can be sure that the data is still available on the follower. 

**8. What can we consider as the main disadvantage of *synchronous* replication?**

If the synchronous follower doesn’t respond (because it has crashed, or there is a network fault, or for
any other reason), the write cannot be processed. The leader must block all writes and wait until
the synchronous replica is available again.

**9. How a follower is restarted if crashes or its network is interrupted?**

From its log, it knows the last transaction that was processed before the fault occurred. Thus the follower can connect to the
leader, and request all data changes that occurred during the time when the follower was disconnected. When it has applied these changes,
it has caught up to the leader, and can continue receiving a stream of data changes as before.


**10. What are the use cases seen on this chapter of *Multi-leader replication*?**

1. Multi-datacenter operation
2. Clients with offline operation
3. Collaborative editing







