## Chapter 3: Storage and Retrieval


**1. Why should you care how the database handles storage and retrieval internally?**

You do need to select a storage engine that is appropriate to your application, from the many
that are available. In order to tune a storage engine to perform well on your kind of workload,
you need to have a rough idea of what the storage engine is doing under the hood.


**2. What is an *index* in the database context?**

Referred to an additional structure that is derived from the primary data in order to efficiently find the value for a particular key in the database


**3. How do we avoid eventually running out of disk space?**

A good solution is to break the log into segments of a certain size, and to periodically
run a background process for compaction and merging of segments. This makes the segments much smaller (assuming that every key is updated
multiple times on average), so we can also merge several segments into one.

**4. What does *compaction* means in the chapter context?**

It means throwing away all key-value pairs in the log except for the most recent
update for each key.

**5. What happens to segments during the proccess of merging them?**

Segments are never modified after they have been written, so the merged segment is written to a
new file. While the merge is going on, we can still continue to serve read and write requests as
normal, using the old segment files. After the merging process is complete, we switch read
requests to using the new merged segment instead of the old segments—and then the old
segment files can simply be deleted.

**6. What are the reasons for the append-only design, instead of overwrite the old value with the new value?**

+  Appending and segment merging are sequential write operations, which are generally much faster
than random writes.

+ Concurrency and crash recovery are much simpler if files are immutable. For example, you don’t have
to worry about the case where a crash happened while a value was being overwritten, leaving you with
a file containing part of the old and part of the new value spliced together.

+  Merging old segments avoids problems of data files getting fragmented over time.

**7. Maintaining a sorted structure on memory is easier than in disk, but what is the main problem?**

If the database crashes, the most recent writes (which are in the memtable but not yet written out to disk) are lost


**8. How to avoid losing writes when using memtable and the database crashes?**

We can keep a separate log on disk to which every write is immediately appended. That log is not in sorted order, but that doesn’t
matter, because its only purpose is to restore the memtable after a crash. Every time the
memtable is written out to an SSTable, the corresponding log can be discarded.


**9. Why keeping a cascade of SSTables that are merged in the background is considered very effective?**

Since data is stored in sorted order, you can efficiently perform range queries (scanning all
keys above some minimum and up to some maximum). And because the disk writes are
sequential, the LSM-tree can support remarkably high write throughput.


**10. How to make the database resilent to crashes when using B-trees?**

It is normal for B-tree implementations to include an additional data structure on disk: a *write-ahead log* (WAL, also known as redo log).
This is an append-only file to which every B-tree modification must be written before it can be
applied to the pages of the tree itself. When the database comes back up after a crash, this log is
used to restore the B-tree back to a consistent state.



