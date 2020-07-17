----------------------------
# Designing Data-Intensive Applications
----------------------------

## Chapter 5: Replication

**1. What are the two main approaches to partitioning?**

+ *Key range partitioning:* where keys are sorted, and a partition owns all the keys
from some minimum up to some maximum. Sorting has the advantage that efficient
range queries are possible, but there is a risk of hot spots if the application
often accesses keys that are close together in the sorted order.

+ Hash partitioning:* where a hash function is applied to each key, and a partition
owns a range of hashes. This method destroys the ordering of keys, making range
queries inefficient, but may distribute load more evenly.


**2. How is *skewed* defined in this chapter?**

When the partitioning is unfair, some partitions have more data or queries than others. This is called *skewed*.

**3. What is the  simplest approach for avoiding hot spots while partitioning?**

To assign records to nodes randomly. That would distribute the data quite evenly across the nodes, but it has a
big disadvantage: when you’re trying to read a particular item, you have no way of
knowing which node it is on, so you have to query all nodes in parallel.


**4. How is the Partitioning by Hash of Key?**

A good hash function takes skewed data and makes it uniformly distributed. Once you have a suitable hash function for keys, you can assign each partition a
range of hashes (rather than a range of keys), and every key whose hash falls within a
partition’s range will be stored in that partition.

**5. What is *Consistent hashing*?**

is a way of evenly distributing load across an internet-wide system of caches such as a content delivery network (CDN).
It uses randomly chosen partition boundaries to avoid the need for central control or
distributed consensus.

**6. It can happen that a workload can result in a large volume of writes to the same key, how can be reduced such a highly skewed workload?

For example, if one key is known to be very hot, a simple technique is to add a random
number to the beginning or end of the key. Just a two-digit decimal random number
would split the writes to the key evenly across 100 different keys, allowing those keys
to be distributed to different partitions.

**7. What are the two methods of partitioning secondary indexes?**

+ *Document-partitioned indexes (local indexes):*  secondary indexes are
stored in the same partition as the primary key and value. This means that only a
single partition needs to be updated on write, but a read of the secondary index
requires a scatter/gather across all partitions.

+ *Term-partitioned indexes (global indexes):* the secondary indexes are partitioned
separately, using the indexed values. An entry in the secondary index may
include records from all partitions of the primary key. When a document is written,
several partitions of the secondary



**8. What is the problem with secondary indexes?**

They don’t map neatly to partitions. Therefore, there are two main approaches to partitioning a database with secondary indexes:
document-based partitioning and term-based partitioning.



**9. What is rebalancing partitions? **

The process of moving load from one node in the cluster to another because over time, the following aspects change in a database:

+ The query throughput increases, so you want to add more CPUs to handle the
load.

+ The dataset size increases, so you want to add more disks and RAM to store it.

+ A machine fails, and other machines need to take over the failed machine’s
responsibilities.


**10. What are the strategies for Rebalancing seen in this chapter?**

+ Hash mod N
+ Fixed number of partitions
+ Dynamic partitioning
+ Partitioning proportionally to nodes


**11. It can be possible an hybrid approach using the two main partitioning?**

Yes, hybrid approaches are also possible, for example with a compound key: using one
part of the key to identify the partition and another part for the sort order.




