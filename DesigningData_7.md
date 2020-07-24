----------------------------
# Designing Data-Intensive Applications
----------------------------

## Chapter 7: Transactions


**1. How is defined a transaction?**

As a way for an application to group several reads and writes
together into a logical unit. Conceptually, all the reads and writes in a transaction are
executed as one operation: either the entire transaction succeeds (commit) or it fails
(abort, rollback).

**2. What characterizes transactions?**

If a transaction fails, the application can safely retry. With transactions, error
handling becomes much simpler for an application, because it doesn’t need to worry
about partial failure—i.e., the case where some operations succeed and some fail (for
whatever reason).


**3. What is known as *safety garantee*?**

When transactions, the application is free to ignore certain
potential error scenarios and concurrency issues, because the database takes care of
them instead

**4. What defines the acronym *ACID*?**

Stands for Atomicity, Consistency, Isolation, and Durability. Defines the safety guarantees provided by transactions.

**5. How are called systems that are not ACID?**

Systems that do not meet the ACID criteria are sometimes called BASE, which
stands for *Basically Available*, *Soft state*, and *Eventual consistency*.


**6. What is the defining feature of ACID atomicity?**

The ability to abort a transaction on error and have all writes from that transaction discarded


**7. Why *serializable isolation* is rarely used in databases?**

Because it carries a performance penalty


**8. Why many distributed datastores have abandoned multi-object transactions?**

because they are difficult to implement across partitions, and they can get in the way in some scenarios
where very high availability or performance is required.


**9. How is described the philosophy of ACID database?**

If the database is in danger of violating its guarantee of atomicity, isolation, or durability, it would rather abandon
the transaction entirely than allow it to remain half-finished.

**10. What is the result of not retry aborted transactions?**

The error usually results in an exception bubbling up the stack, 
so any user input is thrown away and the user gets an error message. 
This is a shame, because the whole point of aborts is to enable safe retries.








