----------------------------
# Designing Data-Intensive Applications
----------------------------

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

+ Concurrenc
