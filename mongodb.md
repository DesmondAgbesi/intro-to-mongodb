# MongoDB Cheatsheet

Show the version of database server
```
  db.version()
```

Return some statics about the server
```
  db.stats()
```
Show all the databases that are present in your MongoDB server
```
  show bds
```

Switch to use the database specified
```
  use <dbName>
```

Creates new collection in the database
```
  db.createCollection(“name”)
```



List all collections under the specified database
```
  show collections
```
### Inserting Document

Inserts one document into the collection
```
insertOne({…})
Syntax
db.<collectionName>.insertOne({})

db.students.insertOne({})
```
Inserts many documents into the collection.
```
  insertMany([{}, {} … {}])
  Syntax
    db.<collectionName>.insertMany([ {}, {} … {}])

    db.teachers.insertMany({})
```
### Finding documents in collection
Returns all the documents in the collection that matches the query. It will return an empty array if there is no document in the collection. If empty object ({}) is passed as query it will return all the documents in the collection.
```
  find({query})

  db.students.find({class: 5})
```

Returns a single document that matches the query
```
    findOne({ query })
    db.students.findOne({_id: ObjectId("6318904f2cc34f3a62aafec0")})
```
### Query methods
Sorts documents in either ascending or descending order
```
    sort()
    db.students.find({}).sort({class: -1})---descending order
    db.students.find({}).sort({class: 1})---ascending order

```

Counts the number of documents returned from a find result
```
    count()
    db.students.find({class: 2}).count()
```

Limits the returning documents to the number specified
```
    limit()
    db.students.find({}).limit()
```

Skips the first number of items specified
```
    skip()
    db.students.find({}).skip(5)
```
### Equality query
Match by field name and it’s exact value
```
  Syntax
    {<fieldName1> :  <value1>, <fieldName1> :  <value1>}

    Example
{“name”:  “John Doe” }
{“age”:  30}
{“gender”: “male”,  “maritalStatus” :  “single”}
```





### Query operators
```
$or				$eq				$lt
$and				$ne				$gt
$gte				$lte				$in
$nin				$regex

db.students.find({
    age: {$gte:10}
})

db.students.find({
    $or: [{gender: "Female"}, {class:5 }]
})
```

### Comparison Operators
Operators add conditions that compares two or more values
```
  Syntax
    {<fieldName1>: {<operator1>: <value1>}, …}

   Examples
    {“age”: {$gt : 25}}
    {“age”: {$lt : 25}}
    {“favouriteFruit”: {“$in”: [“apple”, “orange”]}}
```
This comparison operators require an ARRAY
```
  Syntax
  {<fieldName1>: { <operator1>:  [ <value1>,  <value2>] }, …}

  Examples
    {“eyeColor”: {“$in”: [“blue”, “brown”]}}
    {“favouriteFruit”: {“$nin”: [“apple”, “orange”]}}
```
### "and" operator
Logically combines multiple conditions. Resulting documents must much ALL conditions
```
  Syntax
    { $and: [ { <condition1> }, { <condition2> } … ] }

  Example
    { $and: [ {“gender” : “male”} , “age” : 25 } ] }
```

NB
Explicit $and MUST be used if conditions contains same field or operator

