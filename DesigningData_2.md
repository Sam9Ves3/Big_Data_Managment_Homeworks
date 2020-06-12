## Chapter 2: The Battle of the Data Models


**1. What is the chapter about?**

This chapter looks at a range of general-purpose data models for data storage and
querying.


**2. How the chapters defines the idea *polyglot persistence*?**

When different applications have different requirements, and the best choice of technology for one use
case may well be different from the best choice for another use case. It therefore seems likely
that in the foreseeable future, relational databases will continue to be used alongside a broad
variety of non-relational data stores.



**3. What is defined as *impedance mismatch*?**

When an application is development in object-oriented programming language,
leads to a common criticism of the SQL data model: if data is stored in relational tables, an
awkward translation layer is required between the objects in the application code and the
database model of tables, rows and columns.The disconnect between the models is sometimes
called an impedance mismatch


**4. Given the LinkedIn profile example, what are the advantages of having 
standardized lists and letting users choose from a drop-down list or autocompleter?**

* Consistent style and spelling across profiles.

* Avoiding ambiguity, e.g. if there are several cities with the same name.

* The name is stored only in one place, so it is easy to update across 
the board if it ever needs to be changed (for example, change of a city name due to political events).

*  When the site is translated into other languages, the standardized lists can be localized, and so the
region and industry can be displayed in the viewer’s language.

* Better search. For example, a search for philanthropists in the state of Washington can match this
profile, because the list of regions can include the fact that Seattle is in Washington.


**5. What is the difference between a normalized database from a denormalized database?**

A database in which entities are referred to by ID is called
normalized(like region and industry in the LinkedIn example),
whereas a database that duplicates the names and properties of entities on each
document is denormalized.


**6. How was the design of Information Management System (IMS) database?**

The design of IMS used a fairly simple data model called the hierarchical model, which has
some remarkable similarities to the JSON model used by document databases.It
represented all data as a tree of records nested within records
Like document databases, IMS worked well for one-to-many relationships, but it made
many-to-many relationships difficult and it didn’t support joins. 



**7. What are the arguments in favor when comparing elational vs. document databases?**
The main arguments in favor of the document data model are: 
	* simpler application code, 
	* schema flexibility
	* better performance due to locality.


**8. What data model is the best when many-to-many relationships are very common our your data?**


The relational model, because it can handle simple cases of many-to-many relationships, 
but as the connections within your data become more complex, 
it becomes more natural to start modeling your data as a graph


**9. What are some examples of Graph model?**

* Social graphs: Vertices are people, edges indicate which people know each other.
* The web graph: Vertices are web pages, edges indicate HTML links to other pages.
* Road or rail networks: Vertices are junctions, and edges represent the roads or railway 

In the examples above, all the vertices in a graph represent the same kind of thing (people, web
pages or road junctions, respectively).






**10. If we put graph data in a relational structure, can we also query it using SQL?**

Yes, but with some difficulty. In a relational database, you usually know in
advance which joins you need in your query. In a graph query, you may need to traverse a
variable number of edges before you find the vertex you’re looking for, i.e. the number of joins is
not fixed in advance.
