![Book folder](/src/Picture_1.jpg)

You are about to read some important aspects (according to my criteria) that best summarizes the first two chapters focused in how to approach building a solution to any Big Data problem.. Make yourself comfortable and take a look to get great learning about this amazing book for Big Data ~~beginners~~.


# Chapter 1: A new paradigm for Big Data

1. **Typical problems encountered when scaling a traditional database**

![Figure 1.1](/src/fig 1_2.png)
  
  Imagine that your back end consists of an RDBMS with a table of that schema and a web server(Figure 1.1). After some success, you’ll   run into problems with both scalability and complexity: The database can’t keep up with the load, so write requests to increment       pageviews are timing out. the best approach is to use multiple database servers and spread the table across all the servers. Each       server will have a subset of the data for the table. This is known as horizontal partitioning or sharding. This technique spreads the   write load across multiple machines.

  Your code needs to know how to talk to the right shards, and if you make a mistake, there’s nothing preventing you from reading from or writing to the wrong shard. But the worst problem is that the system is not engineered for human mistakes. Mistakes in software are inevitable, and if you’re not engineering for it, you might as well be writing scripts that randomly corrupt data. Backups are not enough; the system must be carefully thought out to limit the damage a human mistake can cause. Human-fault tolerance is not optional. It’s essential, especially when Big Data adds so many more complexities to building applications.
  

2. **Why NoSQL is not a panacea**

  The past decade has seen a huge amount of innovation in scalable data systems. These include large-scale computation systems like Hadoop and databases such as Cassandra and Riak. These systems can handle very large amounts of data, but with serious trade-offs. These tools on their own are not a panacea. But when intelligently used in conjunction with one another, you can produce scalable systems for arbitrary data problems with human-fault tolerance and a minimum of complexity. This is the Lambda Architecture you’ll learn throughout the book.
  

3. **Thinking about Big Data systems from first principles**

  A data system answers questions based on information that was acquired in the past up to the present. So a social network profile answers questions like “What is this person’s name?” and “How many friends does this person have?” Data systems don’t just memorize and regurgitate information. They combine bits and pieces together to produce their answers. Another crucial observation is that not all bits of information are equal. Some information is derived from other pieces of information. A friend count is derived from a friend list, and a friend list is derived from all the times a user added and removed friends from their profile. When you keep tracing back where information is derived from, you eventually end up at information that’s not derived from anything. This is the rawest information you have: information you hold to be true simply because it exists. Let’s call this information data. You may have a different conception of what the word data means. Data is often used interchangeably with the word information. But for the remainder of this book, when we use the word data, we’re referring to that special information from which everything else is derived.
The properties you should strive for in Big Data systems are:
  * Robustness and fault tolerance
  * Low latency reads and updates
  * Scalability
  * Generalization
  * Extensibility
  * Ad hoc queries
  * Minimal maintenance
  * Debuggability
  

4. **Lambda Architecture**

  Computing arbitrary functions on an arbitrary dataset in real time is a daunting problem. There’s no single tool that provides a complete solution. Instead, you have to use a variety of tools and techniques to build a complete Big Data system. The main idea of the Lambda Architecture is to build Big Data systems as a series of layers. Each layer satisfies a subset of the properties and builds upon the functionality provided by the layers beneath it.
The beauty of the Lambda Architecture is that once data makes it through the batch layer into the serving layer, the corresponding results in the realtime views are no longer needed. This means you can discard pieces of the realtime view as they’re no longer needed. This is a wonderful result, because the speed layer is far more complex than the batch and serving layers. This property of the Lambda Architecture is called complexity isolation, meaning that complexity is pushed into a layer whose results are only temporary. If anything ever goes wrong, you can discard the state for the entire speed layer, and everything will be back to normal within a few hours.

 ![Figure 1.1](/src/fig 1_11.png)
  

5. **Introducing SuperWebAnalytics.com**

  You’ll build an example Big Data application throughout this book to illustrate the concepts. We’ll build the data management layer for a Google Analytics–like service. The service will be able to track billions of pageviews per day. The service will support a variety of different metrics. Each metric will be supported in real time. The metrics range from simple counting metrics to complex analyses
of how visitors are navigating a website. These are the metrics we’ll support:
    * Pageview counts by URL sliced by time
    * Unique visitors by URL sliced by time
    * Bounce-rate analysis



# Chapter 2: 


