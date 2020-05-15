**This is for showing the basic commands for querying in the MongoD shell**

## Installation 
This is the link onf the ownload page: https://www.mongodb.com/download-center

## Before starting
First if all, a few features of MongoDB:
  - Open-source NoSQL database
  - Document oriented
  - Great for unstructured data, especially when you have a lot of it
  - Databases hold collections of documents.
  - Documents are stored in collections, that are analogous to tables in relational databases. 
  
## Structure
```
  Database_1
    Collection_1
      Record_1
        Field_1: value_1
        Field_2: value_2
        Field_2: value_2
      Record_2:
        Field_1: "String_1"
        Field_2: [Element_1, Element_2]
        Field_3: {Element_1, Element_2}
    Collection_2
      Record_1
      Record_2
 Database_2
  Collection_1
    Record_1
```

To run the commands, you must open de cmd (Windows) or the relatives in your SO and type ```mongo``` to start.
  
 ## help
 ```help``` This command will show you all the basic commads for use when you need to show where you are in and other help commands. Take a look at ir before jump to the following

## Database
To select a database to use, in the mongo shell, issue the use <db> statement, as in the following example:
```
use myNewDB
```
  
If a database does not exist, MongoDB creates the database when you first store data for that database. As such, you can switch to a non-existent database and type:
```
use myNewDB
```
```
db.myNewCollection1.insertOne( { x: 1 } )
```


## Collection

### Create a collection
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
### Finding in the collection
To select the documents from a collection, you can use the db.collection.find() method. To select all documents in the collection, pass an empty document as the query filter document to the method.
```
db.inventory.find({})
```

To format the results, append the .pretty() to the find operation:
```
db.inventory.find({}).pretty()
```

To find where the status field equals "D" you should type:
```
db.inventory.find( { status: "D" } );
```

To return document where qty field equals 0
```
db.inventory.find( { qty: 0 } )
```

To return document where qty field equals 0 and status field equals "D":
```
db.inventory.find( { qty: 0, status: "D" } )
```

To return document where the uom field, nested inside the size document, equals "in":
```
db.inventory.find( { "size.uom": "in" } )
```
To return document where the size field equals the document { h: 14, w: 21, uom: "cm" }:
```
db.inventory.find( { size: { h: 14, w: 21, uom: "cm" } } )
```

To return documents where the tags array contains "red" as one of its elements:
```
db.inventory.find( { tags: "red" } )
```

To return documents where the tags field matches the specified array exactly, including the order:
```
db.inventory.find( { tags: [ "red", "blank" ] } )
```
## Specific returns
To specify fields to return, pass a projection document to the db.collection.find(<query document>, <projection document>) method.

To return the _id, item, and the status fields from all documents in the inventory collection:
```
db.inventory.find( { }, { item: 1, status: 1 } )
```

You do not have to specify the _id field to return the field. It returns by default. To exclude the field, set it to 0 in the projection document. For example to return only the item, and the status fields in the matching documents:
```
db.inventory.find( {}, { _id: 0, item: 1, status: 1 } );
```


## License
Open source project
