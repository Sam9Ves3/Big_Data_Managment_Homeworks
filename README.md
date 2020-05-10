# MongoDB-cheatsheet
This is for showing the basic commands for querying in the MongoD shell

## Installation 
This is the link onf the ownload page: https://www.mongodb.com/download-center

## Before starting
First if all, a few features of MongoDB:
  - Open-source NoSQL database
  - Document oriented
  - Great for unstructured data, especially when you have a lot of it
  - In the database youwill find collections
  - Documents are stored in collections, that are analogous to tables in relational databases. 

To run the commands, you must open de cmd (Windows) or the relatives in your SO and type ```mongo``` to start.
  
 ## help
  ```help``` This command will show you all the basic commads for use when you need to show where you are in and other help commands. Take a look at ir before jump to the following


## Collections
If a collection does not exist, MongoDB creates the collection when you first store data for that collection. The following example uses the db.collection.insertMany() method to insert new documents into the inventory collection.MongoDB adds an _id field with an ObjectId value if the field is not present in the document:

```
db.inventory.insertMany([
   { item: "journal", qty: 25, status: "A", size: { h: 14, w: 21, uom: "cm" }, tags: [ "blank", "red" ] },
   { item: "notebook", qty: 50, status: "A", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank" ] },
   { item: "paper", qty: 10, status: "D", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank", "plain" ] },
   { item: "planner", qty: 0, status: "D", size: { h: 22.85, w: 30, uom: "cm" }, tags: [ "blank", "red" ] },
   { item: "postcard", qty: 45, status: "A", size: { h: 10, w: 15.25, uom: "cm" }, tags: [ "blue" ] }
]);
```

To select the documents from a collection, you can use the db.collection.find() method. To select all documents in the collection, pass an empty document as the query filter document to the method.
```
db.inventory.find({})
```

To format the results, append the .pretty() to the find operation:
```
db.inventory.find({}).pretty()
```

## Finding 
To find where the status field equals "D" you should type:
```
db.inventory.find( { status: "D" } );
```
To return document where qty field equals 0
```
db.inventory.find( { qty: 0 } )
```


In the shell, copy and paste the following to return document where qty field equals 0 and status field equals "D":

db.inventory.find( { qty: 0, status: "D" } )
In the shell, copy and paste the following to return document where the uom field, nested inside the size document, equals "in":

db.inventory.find( { "size.uom": "in" } )
In the shell, copy and paste the following to return document where the size field equals the document { h: 14, w: 21, uom: "cm" }:

db.inventory.find( { size: { h: 14, w: 21, uom: "cm" } } )
Equality matches on the embedded document require an exact match, including the field order.

In the shell, copy and paste the following to return documents where the tags array contains "red" as one of its elements:

db.inventory.find( { tags: "red" } )
If the tags field is a string instead of an array, then the query is just an equality match.

In the shell, copy and paste the following to return documents where the tags field matches the specified array exactly, including the order:

db.inventory.find( { tags: [ "red", "blank" ] } )

Author
[Samuel Venegas][

## License
Open source project
