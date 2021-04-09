
# Sections

<details open="open">
  <summary>Contents table</summary>
  <ol>
    <li>
      <a href="#Change-the-document-root">Change the document root</a>
    </li>
  </ol>
</details>
## Change the document root
> This is really usefull when you want to change document's root, it means if there are any neasted array and toy want to place it as the main "Table" to display you can place it
``` JavaScript
{ $replaceRoot: { newRoot: <replacementDocument> } }
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
We can pass somme extra parms to the command, they are the next ones: 
1. Query: Is optional. It specifies selection filter using query operators. To return all documents in a collection, omit this parameter or pass an empty document ({}).
``` JavaScript
db.collection.findOne({ "name" : "Guillermo" })
db.collection.find({ "name" : "Guillermo" })
```
2. Projection: Is optional. It specifies the fields to return in the documents that match the query filter. To return all fields in the matching documents, omit this parameter.
``` JavaScript
db.collection.findOne({ }, { <field1>: <value>, <field2>: <value> ... })
db.collection.find({ }, { <field1>: <value>, <field2>: <value> ... })
```
