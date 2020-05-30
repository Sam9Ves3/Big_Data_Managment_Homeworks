# Designing Data-Intensive Applications 

## Chapter 1. Reliable, Scalable and Maintainable Applications


**1. What do we expect for software to be *Reliable*?**

* The application performs the function that the user expected.

* It can tolerate the user making mistakes, or using the software in unexpected ways.

* Its performance is good enough for the required use case, under expected load and data volume.

* The system prevents any unauthorized access and abuse.

All those things together mean “working correctly”, then we can understand reliability as
meaning, roughly, “continuing to work correctly, even when things go wrong”.


**2. How do we differentiate *fault* from *failure* ?**

A *fault* is usually defined as one component of the system deviating from its spec, whereas a *failure* is 
when the system as a whole stops providing the required service to the user.

**3. How can we reduce the failure rate of a hardware system?**

Disks may be set up in a RAID configuration, servers
may have dual power supplies and hot-swappable CPUs, and data centers may have batteries
and diesel generators for backup power. When one component dies, the redundant component
can take its place while the broken component is replaced. This approach cannot completely
prevent hardware problems from causing failures, but it is well understood, and can often keep a
machine running uninterrupted for years.


**4. Why faults in software tend to cause many more system failures than hardware faults?**

Systematic errors within the system are harder to anticipate because they are correlated across nodes, they 
tend to cause many more system failures han uncorrelated hardware faults
The bugs that cause these kinds of software fault often lie dormant for a long time until they are
triggered by an unusual set of circumstances. In those circumstances, it is revealed that the
software is making some kind of assumption about its environment, and whilst that assumption
is usually true, it eventually stops being true for some reason.


**5. How twitter handles the tweets delivery within 5 seconds? According to the scalability section**

Twitter is moving to a hybrid of both approaches. Most users’ tweets continue to be fanned out to home timelines at the time when they are posted, but a small number of users with a very large number of followers are excepted from this fan-out. Instead, when the home timeline is read, the tweets from celebrities followed by the user are fetched separately and merged with the home timeline when the timeline is read. This hybrid approach is able to deliver consistently good performance.

**6. What are the tree design principles for software systems to minimize pain during maintenance?**

* *Operability*: Make it easy for operations teams to keep the system running smoothly.

* *Simplicity*: Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. (Note this is not the same as simplicity of the user interface.)

* *Plasticity*: Make it easy for engineers in future to make changes to the system, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability or malleability.


**7. What is the relation between complexity in software with its maintenance?**

Complexity slows down everyone who needs to work on the system, further increasing the cost of maintenance. In
complex software, there is also a greater risk of introducing bugs when making a change: when
the system is harder for developers to understand and reason about, hidden assumptions,
unintended consequences and unexpected interactions are more easily overlooked. Conversely,
reducing complexity greatly improves the maintainability of software, and thus simplicity
should be a key goal for the systems we build.

**8. How does Monseley and Marks define *complexity*?**

as accidental if it isnot inherent in the problem that the software solves (as seen by the users), but arises only from
the implementation

**9. What word is used to refer to agility on a data system level?**

Plasticity.


**10. What is *Redis*?**
Redis is not a plain key-value store, it is actually a data structures server, supporting different kinds of values. What this means is that, while in traditional key-value stores you associate string keys to string values, in Redis the value is not limited to a simple string, but can also hold more complex data structures.

