- [1. Install MongoDB](#1-install-mongodb)
- [2. Add below notes](#2-add-below-notes)
  - [Version check](#version-check)
- [3. Start MongoDB](#3-start-mongodb)
- [4. Using MongoDB](#4-using-mongodb)
  - [Show all DBs](#show-all-dbs)
  - [Select DB name](#select-db-name)
  - [Write data in the DB](#write-data-in-the-db)
  - [Remove DB](#remove-db)
  - [Create Collection](#create-collection)
  - [Remove Collection](#remove-collection)
  - [Insert Document](#insert-document)
  - [View Documents](#view-documents)
  - [Remove Documents](#remove-documents)
- [5. Updating Field](#5-updating-field)
  - [Update Field](#update-field)
  - [Replace Field](#replace-field)
  - [Remove field   ::   `$unset`](#remove-field------unset)
  - [Upsert option](#upsert-option)
  - [Add values to field Array  ::  `$push`](#add-values-to-field-array----push)
      - [Add values to field Array + sort   ::  `$each`, `$sort`](#add-values-to-field-array--sort-----each-sort)
      - [Remove value from field Array   ::   `$pull`](#remove-value-from-field-array------pull)
      - [Remove multiple values from field Array   ::  `$in`](#remove-multiple-values-from-field-array-----in)
- [6. Insert Query](#6-insert-query)
  - [Comaprison operator](#comaprison-operator)
  - [Logic operator](#logic-operator)
  - [Regex Operator](#regex-operator)
  - [`$where` Operator](#where-operator)
  - [$elementMatch Operator](#elementmatch-operator)
- [7. [projection]](#7-projection)
  - [`$slice` Operator](#slice-operator)
  - [`$elemMatch` Operator](#elemmatch-operator)
- [8. Sorting](#8-sorting)
  - [`sort()`](#sort)
  - [`limit()`](#limit)
  - [`skip()`](#skip)

-------------------


# 1. Install MongoDB

Install the mongoDB server
``` sh
  $ sudo yum install -y mongodb-org mongodb-org-server
    # error?
    # No match for argument: mongodb-org
    # No match for argument: mongodb-org-server
```
If error messages come up, then you have to make an repository for MongoDB

``` sh
  $ vim /etc/yum.repos.d/mongodb-org-4.2.repo
```
  
# 2. Add below notes

``` sh
  [mongodb-org-4.2]   
  name=MongoDB Repository

  baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
  gpgcheck=1
  enabled=1
  gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
```

You can install it from now on.    
``` sh
  $ sudo yum install -y mongodb-org
    ...
    Complete!
```
  
## Version check
``` sh
  $ mongod --version
  $ mongo --version
```
  
# 3. Start MongoDB
``` sh
  $ sudo service mongod start
  
    Redirecting to /bin/systemctl status mongod.service
    ● mongod.service - MongoDB Database Server
        Loaded: loaded (/usr/lib/systemd/system/mongod.service; enabled; vendor prese>
        Active: active (running) since Thu 2020-01-23 20:21:30 KST; 10s ago
          ...
        
  $ mongo
```

# 4. Using MongoDB

## Show all DBs
``` sh
  > show dbs
    admin   0.000GB
    config  0.000GB
    local   0.000GB
``` 

## Select DB name
``` sh
  > use mongodb_tutorial
```

## Write data in the DB
``` sh
  > db.sample.insert({"name": "sample"});
  > show dbs
    admin             0.000GB
    config            0.000GB
    local             0.000GB
    mongodb_tutorial  0.000GB
```

## Remove DB

Before using it, you must select a database.

``` sh
  > db.dripDatabase() 
    { "dropped" : "mongodb_tutorial", "ok" : 1 }
  > show dbs
    admin   0.000GB
    config  0.000GB
    local   0.000GB
```


## Create Collection

* `db.createCollection(name, [options])`

``` sh
  > db.createCollection("books")
    { "ok" : 1 }
  > db.people.insert({"name": "velopert"})
      WriteResult({ "nInserted" : 1 })
  > show collections
      books
      people
```

## Remove Collection
``` sh
  > db.people.drop()
      true
  > show collections
      books
```

## Insert Document 

``` sh
  > db.books.insert({"name": "NodeJS Guide", "author": "Velopert"})
    WriteResult({ "nInserted" : 1 })
```

if you want to insert multiple documents, you can put it into Array.
``` sh
  > db.books.insert([
      ... { "name": "Book1", "author": "Velopert" },
      ... { "name": "Book2", "author": "Velopert" }
      ... ])
      
    BulkWriteResult({
    "writeErrors" : [ ],
    "writeConcernErrors" : [ ],
    "nInserted" : 2,     # successfully added
    "nUpserted" : 0,
    "nMatched" : 0,
    "nModified" : 0,
    "nRemoved" : 0,
    "upserted" : [ ]
  })
```

## View Documents
* `db.collection_name.find([query],[projection])`

``` sh
  > db.books.find()
      { "_id" : ObjectId("5e2987b9dd8593d1a93c5708"), "name" : "NodeJS Guide", "author" : "Velopert" }
      { "_id" : ObjectId("5e298840dd8593d1a93c5709"), "name" : "Book1", "author" : "Velopert" }
      { "_id" : ObjectId("5e298840dd8593d1a93c570a"), "name" : "Book2", "author" : "Velopert" }
      
  > db.books.find().pretty()
      {
        "_id" : ObjectId("5e298840dd8593d1a93c570a"),
        "name" : "Book2",
        "author" : "Velopert"
      }
      {
        "_id" : ObjectId("5e298d1bdd8593d1a93c570b"),
        "name" : "Book1",
        "author" : "Velopert"
      }
      {
        "_id" : ObjectId("5e298d1bdd8593d1a93c570c"),
        "name" : "Book2",
        "author" : "Velopert"
      }
```

## Remove Documents
* `*db.collection_name.remove(criteria, [justOne])`

``` sh
  > db.books.remove({"name": "NodeJS Guide"})
      WriteResult({ "nRemoved" : 1 })
  >  db.books.find()
      { "_id" : ObjectId("5e298840dd8593d1a93c5709"), "name" : "Book1", "author" : "Velopert" }
      { "_id" : ObjectId("5e298840dd8593d1a93c570a"), "name" : "Book2", "author" : "Velopert" }
      
  > db.books.remove({"author": "Velopert"}, true)
      WriteResult({ "nRemoved" : 1 })
  >  db.books.find()
      { "_id" : ObjectId("5e298840dd8593d1a93c570a"), "name" : "Book2", "author" : "Velopert" }
```    

# 5. Updating Field

## Update Field
``` sh
  > db.people.update( {"name": "Abet"}, { $set: { age: 20 } } )
      WriteResult({ "nRemoved" : 1, "nUpserted": 0, "nModified": 1 })
```

## Replace Field
Just do not use `$set` operator to replace the document.

``` sh
  > db.people.update( {"name": "Abet"}, { "name": "Betty 2nd", age:1 } )
      WriteResult({ "nRemoved" : 1, "nUpserted": 0, "nModified": 1 })
```
## Remove field   ::   `$unset`

Use `$unset` operator to remove field

``` sh
  > db.people.update({ name: "David" }, { $unset: { score: 1 } })
      WriteResult({ "nRemoved" : 1, "nUpserted": 0, "nModified": 1 })
```
## Upsert option
If there are not exist what we searched, it will add new field.

``` sh
  > db.people.update({ name: "Elly" }, { name: "Elly", age: 17 }, { upsert: true })
```

## Add values to field Array  ::  `$push`
``` sh
  > db.people.update(
      {name: "Charlie"},
      {$push: { "skills": "angular.js" }}
    )
```

#### Add values to field Array + sort   ::  `$each`, `$sort`
``` sh
  > db.people.update(
      {name: "Charlie"},
      {$push: { 
          "skills": {
              $each: ["c++", "java"],
              $sort: 1              
            }
          }
        }
    )
```
#### Remove value from field Array   ::   `$pull`

```` sh
  > db.people.update(
      { name: "Charlie" },
      { $pull: { skills: "mongoDB } }
    )
````
#### Remove multiple values from field Array   ::  `$in`

``` sh
  > db.people.update(
      { name: "Charlie" },
      { $pull: { skills: $in: [ "angular.js", "java" ] } }
    )
```

# 6. Insert Query

MongoDB can filter the result through the conditions.

## Comaprison operator

|operator|explanation|
|------|---|
|`$eq`|equal|
|`$gt`|greater than|
|`$gte`|greater than or equal|
|`$lt`|less than|
|`$lte`|less than or equal|
|`$ne`|not equal|
|`$in`|values within the Array|
|`$nin`|values not within the Array|

``` sh
  > db.numbers.find({"value": 56})
    # Tt will show results filtered "value" key is the same with 56
  
  > bd.numbers.find({"value": { $gt: 100 } })
    # It will show results filtered "value" key is bigger than 100
    
  > db.numbers.find({"value": { $gt: 0, $lt: 100 })
    # It will show results filtered between bigger than 0 and less than 100
    
  > db.numbers.find({"value": { $gt: 0, $lt: 100, $nin: [12, 33] })
    # It will show results filtered between bigger than 0 and less than 100 within given array.
```

## Logic operator
|OR|AND|NOT|NOR|
|------|---|---|---|
|`$or`|`$and`|`$not`|`$nor`|

``` sh
  > db.articles.find({ $or: [ {"title": "article01"}, {"writer": "Alpha"}] })
    # It will show results filtered either "title" key is "article01" || "writer" key is "Alpha"
    
  > db.articles.find({ $and: [ {"writer": "Velopert"}, {"likes": { $lt: 10 } }] })
    # It will show results filtered either "writer" key is "Velopert" && "likes" key is less than 10
    # Similar with =>     db.articles.find( {"writer": "Velopert"}, {"likes": { $lt: 10 } })
```

## Regex Operator
you can find Document by using $regex operator.

``` sh
  > db.article.find( {"title": /article0[1-2] } )
  > db.article.find( {"writer": /velopert/i } )
```

|operator|explanation|
|------|---|
|`i`|ignore case|
|`m`| ... |
|`x`|ignore all whitespaces|
|`s`|including \n, using '.'|


## `$where` Operator

You can use javascript expression with 'where operator'

``` sh
  > db.article.find({ $where: "this.comments.length == 0" }).pretty()
      # It will show results filtered the condition with JS syntax
```      

## $elementMatch Operator

Using it when you query the Array of subdocument (embedded document).

``` sh
  > db.articles.find({ "comments": { $elementMatch: { "name": "Charlie" } } })
```

# 7. [projection] 

🍟🍟🍟 ?? 설명 필요

* `db.collection_name.find([query], [projection])`

``` sh
  > db.articles.find({}, {"id": false, "title": true, "content": true })
```
  
## `$slice` Operator

When subdocument array is read, make a limitation.
``` sh
  > db.articles.find({ "title": "article03", { commetns: { $slice: 1 } } })
```

## `$elemMatch` Operator

In an Array, it prints certain subdocument.

  > ★★★★★★★★★★★★★★★
  


# 8. Sorting

## `sort()`
|value| meaning|
|---|----|
|1| asc|
|-1| desc|

``` sh
  > db.numbers.find({ "value": 1 })
      # It will show ascending results 
  
  > db.numbers.find({ "value": -1 })
      # It will show descending results 
```

## `limit()`

``` sh
  > db.numbers.find().limit(3)
      # It will show only 3 results
```

## `skip()`
``` sh
  > db.numbers.find().skip(2)
      # It will show results, except 2 before the result. 
```









