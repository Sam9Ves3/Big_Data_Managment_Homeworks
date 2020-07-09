# Chapter 4: Encoding and Evolution

**1. What are the two compatibilities to run old and new versions of the code?**

+ Backward compatibility: Newer code can read data that was written by older code.
+ Forward compatibility: Older code can read data that was written by newer code.

**2. What are the 3 popular standardized encodings seen in this chapter?**

+ *XML* : often criticized for being too verbose and unnecessarily complicated. 
+ *JSON* : is popularity is mainly due to its built-in support in web browsers (by virtue of being a subset of JavaScript) and simplicity relative to XML. 
+ CSV is another popular language-independent format, albeit less powerful.
JSON, XML, and CSV are textual formats, and thus somewhat human-readable (although the syntax is a popular topic of debate).

**3. What is *SOAP*?**

SOAP is an XML-based protocol for making network API requests. Although it is most commonly used over HTTP, it aims to be independent from HTTP and avoids using most HTTP features. Instead, it comes with a sprawling and complex multitude of related standards (the web service framework, known as WS-*) that add various features. The API of a SOAP web service is described using an XML-based language called the Web Services Description Language, or WSDL. WSDL enables code generation so that a client can access a remote service using local classes and method calls (which are encoded to XML messages and decoded again by the framework).


**4. What is RPC?**

The RPC (Remote Procedure Call) model tries to make a request to a remote network service look the same as calling a function or method in your programming language, within the same process (this abstraction is called location transparency).
Although RPC seems convenient at first, the approach is fundamentally flawed

**5. How are message brokers used?**

One process sends a message to a named queue or topic, and the broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic. There can be many producers and many consumers on the same topic.


**6. What are the advantages of using binary encodings based on schemas?**

+ They can be much more compact than the various “binary JSON” variants, since they can omit field names from the encoded data.
+ The schema is a valuable form of documentation, and because the schema is required for decoding, you can be sure that it is up to date
+ Keeping a database of schemas allows you to check forward and backward compatibility of schema changes, before anything is deployed.
+ For users of statically typed programming languages, the ability to generate code from the schema is useful, since it enables type checking at compile time.**

**7. What are the two ways of distributing data across multiple nodes?**

+ Replication: keeping a copy of the same data on several different nodes, potentially in different locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes.
+ Partitioning or sharding: splitting a big database into smaller subsets called partitions, so that different partitions can be assigned to different nodes


**8. What is REST?**

EST is not a protocol, but rather a design philosophy that builds upon the principles of HTTP. It emphasizes simple data formats, using URLs for identifying resources and using HTTP features for cache control, authentication, and content type negotiation. REST has been gaining popularity compared to SOAP, at least in the context of cross-organizational service integration, and is often associated with microservices. An API designed according to the principles of REST is called RESTful.



**9. What is the main difference between synchronous replication and the asynchronous one?**

When replication is synchronous, the leader waits until followers have confirmed that they received the write before reporting success to the user. When the leader sends the message, but doesn’t wait for a response from the follower is asynchronous replication


**10. What's Data Flow and which are its types?**

Data flow is how data flows through your system. It involves thinking about data usage patterns, application boundaries, and similar such things. Its types are:

+ Databases

+ Service Communication

+ Message Bus Pattern
