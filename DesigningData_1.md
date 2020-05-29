# Chapter 1


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



