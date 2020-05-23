# Chapter 3: Data model for Big Data: Illustration.


**1. What's the problem of writing raw data in JSON format**

This appeals because of how easy it is to get started, but this approach quickly leads to problems. Whether due to bugs or 
misunderstandings between different developers, data corruption inevitably occurs. Data corruption errors are some of the most
time-consuming to debug. Data corruption issues are hard to debug because you have very little context on how the corruption occurred.


**2. Rules to change the schema and still be compatible with existing data**

* Fields may be renamed. This is because the serialized form of an object uses the field IDs, not the names, to identify fields.

* A  field may be removed, but you must never reuse that field ID. When deserializing existing data, Thrift will ignore all fields 
with field IDs not included in the schema. If you were to reuse a previously removed field ID, Thrift would try to deserialize that 
old data into the new field, which will lead to either invalid or incorrect data.

* Only optional fields can be added to existing structs. You can’t add required fields because existing data won’t have those fields
and thus won’t be deserializable.


**3. How to understand a schema in Apache Thrift**

The right way to think about a schema is as a function that takes in a piece of data and returns whether it’s valid or not. 
The schema language for Apache Thrift lets you represent a subset of these functions where only field existence and field types 
are checked. The ideal tool would let you implement any possible schema function


**4. What is the limitation for serialization frameworks?**

They only check that all required fields are present and are of the expected type. They’re unable to check richer properties 
like “Ages should be nonnegative” or “true-as-of timestamps should not be in the future.” Data not matching these properties 
would indicate a problem in your system, and you wouldn’t want them written to your master dataset.


**5. What are the two approaches to around these limitations with a serialization framework like Apache Thrift?**

* Wrap your generated code in additional code that checks the additional properties you care
about, like ages being non-negative. This approach works well as long as you’re only
reading/writing data from/to a single language—if you use multiple languages,
you have to duplicate the logic in many languages.

* Check the extra properties at the very beginning of your batch-processing workflow. This
step would split your dataset into “valid data” and “invalid data” and send a notification
if any invalid data was found. This approach makes it easier to implement
the rest of your workflow, because anything getting past the validity check
can be assumed to have the stricter properties you care about. But this approach
doesn’t prevent the invalid data from being written to the master dataset and
doesn’t help with determining the context in which the corruption happened.

-------------------------------------------------------------------------------------------------------------------------

# Chapter 4: Data storage on the batch layer

**1.Why batch layer storage system needs to be good at reading data?**

Because is responsible for computing functions on the dataset to produce the batch views.

**2. What are the two requisites of the writing operation in the batch layer?**

* Effitient append of new data: The only write operation is to add new pieces of data, so it must be easy
and efficient to append a new set of data objects to the master dataset.

* Scalable storage: The batch layer stores the complete dataset—potentially terabytes or petabytes
of data. It must therefore be easy to scale the storage as your dataset
grows.


**3. What is the requisites of the reading operation in the batch layer?**

Support for parallel processing to handle large amounts of data in a scalable manner.

**4. What is the biggest problem when using a key/value store for the master dataset**

The biggest problem is that a key/value store has a lot of things you don’t need: random reads, random writes, and all
the machinery behind making those work. In fact, most of the implementation of a key/value store is dedicated to these features you don’t need at all. Additionally, the key/value store indexes your data and provides unneeded services, which will increase your storage costs and lower your performance when reading and writing data.


**5. What differentiates a file system from a key/value store?**

Unlike a key/value store, a filesystem gives you exactly what you need and no more, while also not limiting your ability to tune storage cost versus processing cost. On top of that, filesystems implement fine-grained permissions systems, which are perfect for enforcing immutability.


**6. What is a problem with regular file system?**

Is that it exists on just a single machine, so you can only scale to the storage limits and processing power of that one machine


**7. What does the distibuted file system technology does?**

Distributed filesystems are quite similar to the filesystems you’re familiar with, except they spread their storage across a cluster of computers. They scale by adding more machines to the cluster. Distributed filesystems are designed so that you have fault tolerance when a machine goes down, meaning that if you lose one machine, all your files and data will still be accessible.









