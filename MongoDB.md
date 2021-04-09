# Sections

<details open="open">
  <summary>Contents table</summary>
  <ol>
    <li>
      <a href="#Generalities">Generalities</a>
    </li>
    <li>
      <a href="#Databases">Databases</a>
    </li>
    <li>
      <a href="#Create-a-Database">Create a Database</a>
    </li>
    <li>
      <a href="#Create-a-Collection">Create a Collection</a>
    </li>
    <li>
      <a href="#Create-a-view">Create a view</a>
    </li>
    <li>
      <a href="#Change-the-document-root">Change the document root</a>
    </li>
    <li>
      <a href="#Finding-registers">Finding registers</a>
    </li>
    <li>
      <a href="#Finding-parameters">Finding parameters</a>
    </li>
  </ol>
</details>

## Generalities

### Databases
It was took form documentation :
https://docs.mongodb.com/manual/core/databases-and-collections/

To select a database to use, in the mongo shell, issue the use <db> statement, as in the following example:
``` JavaScript
use myDB
```
### Create a Database

If a database does not exist, MongoDB creates the database when you first store data for that database. As such, you can switch to a non-existent database and perform the following operation in the mongo shell:
``` JavaScript
use myNewDB
db.myNewCollection1.insertOne( { x: 1 } )
```
The insertOne() operation creates both the database myNewDB and the collection myNewCollection1 if they do not already exist. Be sure that both the database and collection names follow MongoDB Naming Restrictions.

### Create a Collection
If a collection does not exist, MongoDB creates the collection when you first store data for that collection.
``` JavaScript
db.myNewCollection2.insertOne( { x: 1 } )
db.myNewCollection3.createIndex( { y: 1 } )
```
Both the insertOne() and the createIndex() operations create their respective collection if they do not already exist.

### Create a view

Use the db.createCollection() method or the create command:
``` JavaScript
// Estructura
db.createCollection(
  "<viewName>",
  {
    "viewOn" : "<source>",
    "pipeline" : [<pipeline>],
    "collation" : { <collation> }
  }
)
// Example
``` 

Use the db.createView() method:
``` JavaScript
// Estructura
db.createView(
  "<viewName>",
  "<source>",
  [<pipeline>],
  {
    "collation" : { <collation> }
  }
)
// Example
``` 

## Change the document root
> This is really usefull when you want to change document's root, it means if there are any neasted array and toy want to place it as the main "Table" to display you can place it
``` JavaScript
// Estructure
{ $replaceRoot: { newRoot: <replacementDocument> } }
// Example
// Inserting data
db.collection.insertMany([
   { "_id": 1, "name" : { "first" : "John", "last" : "Backus" } },
   { "_id": 2, "name" : { "first" : "John", "last" : "McCarthy" } },
   { "_id": 3, "name": { "first" : "Grace", "last" : "Hopper" } },
])
// Executing query to change root
db.collection.aggregate([
   { $replaceRoot: { newRoot: "$name" } }
])
```

## Finding registers
We have different options for this, whe have:
1. FindOne: This will return a single document
``` JavaScript
db.collection.findOne()
```
2. Find: This will return all the data we have in the database
``` JavaScript
db.collection.find()
```

## Finding parameters
> It can be used with find or findOne
We can pass somme extra parms to the command, they are the next ones: 
1. Query: Is optional. It specifies selection filter using query operators. To return all documents in a collection, omit this parameter or pass an empty document ({}).
``` JavaScript
// Structure
db.collection.find({ <field1>: <value> })
// Example

```
2. Projection: Is optional. It specifies the fields to return in the documents that match the query filter. To return all fields in the matching documents, omit this parameter.
``` JavaScript
// Structure
db.collection.find({}, { <field1>: <value>, <field2>: <value> ... })
db.collection.find({}, { <field>: <1 or true> }) // Specifies the inclusion of a field.
db.collection.find({}, { <field>: <0 or false> }) // Specifies the exclusion of a field.
Specifies the inclusion of a field.
// Example
db.bios.insertMany([
   {
       "_id" : 1,
       "name" : {
           "first" : "John",
           "last" : "Backus"
       },
       "birth" : ISODate("1924-12-03T05:00:00Z"),
       "death" : ISODate("2007-03-17T04:00:00Z"),
       "contribs" : [
           "Fortran",
           "ALGOL",
           "Backus-Naur Form",
           "FP"
       ],
       "awards" : [
           {
               "award" : "W.W. McDowell Award",
               "year" : 1967,
               "by" : "IEEE Computer Society"
           },
           {
               "award" : "National Medal of Science",
               "year" : 1975,
               "by" : "National Science Foundation"
           },
           {
               "award" : "Turing Award",
               "year" : 1977,
               "by" : "ACM"
           },
           {
               "award" : "Draper Prize",
               "year" : 1993,
               "by" : "National Academy of Engineering"
           }
       ]
   },
   {
       "_id" : ObjectId("51df07b094c6acd67e492f41"),
       "name" : {
           "first" : "John",
           "last" : "McCarthy"
       },
       "birth" : ISODate("1927-09-04T04:00:00Z"),
       "death" : ISODate("2011-12-24T05:00:00Z"),
       "contribs" : [
           "Lisp",
           "Artificial Intelligence",
           "ALGOL"
       ],
       "awards" : [
           {
               "award" : "Turing Award",
               "year" : 1971,
               "by" : "ACM"
           },
           {
               "award" : "Kyoto Prize",
               "year" : 1988,
               "by" : "Inamori Foundation"
           },
           {
               "award" : "National Medal of Science",
               "year" : 1990,
               "by" : "National Science Foundation"
           }
       ]
   },
   {
       "_id" : 3,
       "name" : {
           "first" : "Grace",
           "last" : "Hopper"
       },
       "title" : "Rear Admiral",
       "birth" : ISODate("1906-12-09T05:00:00Z"),
       "death" : ISODate("1992-01-01T05:00:00Z"),
       "contribs" : [
           "UNIVAC",
           "compiler",
           "FLOW-MATIC",
           "COBOL"
       ],
       "awards" : [
           {
               "award" : "Computer Sciences Man of the Year",
               "year" : 1969,
               "by" : "Data Processing Management Association"
           },
           {
               "award" : "Distinguished Fellow",
               "year" : 1973,
               "by" : " British Computer Society"
           },
           {
               "award" : "W. W. McDowell Award",
               "year" : 1976,
               "by" : "IEEE Computer Society"
           },
           {
               "award" : "National Medal of Technology",
               "year" : 1991,
               "by" : "United States"
           }
       ]
   },
   {
       "_id" : 4,
       "name" : {
           "first" : "Kristen",
           "last" : "Nygaard"
       },
       "birth" : ISODate("1926-08-27T04:00:00Z"),
       "death" : ISODate("2002-08-10T04:00:00Z"),
       "contribs" : [
           "OOP",
           "Simula"
       ],
       "awards" : [
           {
               "award" : "Rosing Prize",
               "year" : 1999,
               "by" : "Norwegian Data Association"
           },
           {
               "award" : "Turing Award",
               "year" : 2001,
               "by" : "ACM"
           },
           {
               "award" : "IEEE John von Neumann Medal",
               "year" : 2001,
               "by" : "IEEE"
           }
       ]
   },
   {
       "_id" : 5,
       "name" : {
           "first" : "Ole-Johan",
           "last" : "Dahl"
       },
       "birth" : ISODate("1931-10-12T04:00:00Z"),
       "death" : ISODate("2002-06-29T04:00:00Z"),
       "contribs" : [
           "OOP",
           "Simula"
       ],
       "awards" : [
           {
               "award" : "Rosing Prize",
               "year" : 1999,
               "by" : "Norwegian Data Association"
           },
           {
               "award" : "Turing Award",
               "year" : 2001,
               "by" : "ACM"
           },
           {
               "award" : "IEEE John von Neumann Medal",
               "year" : 2001,
               "by" : "IEEE"
           }
       ]
   },
   {
       "_id" : 6,
       "name" : {
           "first" : "Guido",
           "last" : "van Rossum"
       },
       "birth" : ISODate("1956-01-31T05:00:00Z"),
       "contribs" : [
           "Python"
       ],
       "awards" : [
           {
               "award" : "Award for the Advancement of Free Software",
               "year" : 2001,
               "by" : "Free Software Foundation"
           },
           {
               "award" : "NLUUG Award",
               "year" : 2003,
               "by" : "NLUUG"
           }
       ]
   },
   {
       "_id" : ObjectId("51e062189c6ae665454e301d"),
       "name" : {
           "first" : "Dennis",
           "last" : "Ritchie"
       },
       "birth" : ISODate("1941-09-09T04:00:00Z"),
       "death" : ISODate("2011-10-12T04:00:00Z"),
       "contribs" : [
           "UNIX",
           "C"
       ],
       "awards" : [
           {
               "award" : "Turing Award",
               "year" : 1983,
               "by" : "ACM"
           },
           {
               "award" : "National Medal of Technology",
               "year" : 1998,
               "by" : "United States"
           },
           {
               "award" : "Japan Prize",
               "year" : 2011,
               "by" : "The Japan Prize Foundation"
           }
       ]
   },
   {
       "_id" : 8,
       "name" : {
           "first" : "Yukihiro",
           "aka" : "Matz",
           "last" : "Matsumoto"
       },
       "birth" : ISODate("1965-04-14T04:00:00Z"),
       "contribs" : [
           "Ruby"
       ],
       "awards" : [
           {
               "award" : "Award for the Advancement of Free Software",
               "year" : "2011",
               "by" : "Free Software Foundation"
           }
       ]
   },
   {
       "_id" : 9,
       "name" : {
           "first" : "James",
           "last" : "Gosling"
       },
       "birth" : ISODate("1955-05-19T04:00:00Z"),
       "contribs" : [
           "Java"
       ],
       "awards" : [
           {
               "award" : "The Economist Innovation Award",
               "year" : 2002,
               "by" : "The Economist"
           },
           {
               "award" : "Officer of the Order of Canada",
               "year" : 2007,
               "by" : "Canada"
           }
       ]
   },
   {
       "_id" : 10,
       "name" : {
           "first" : "Martin",
           "last" : "Odersky"
       },
       "contribs" : [
           "Scala"
       ]
   }
] )

// 

```
