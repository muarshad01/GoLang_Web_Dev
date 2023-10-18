## 155. NoSQL

***

## 156. MongoDB

***

## 157. Installing Mongo

* [How to install a local MongoDB on macOS and connect to Studio 3T](https://studio3t.com/knowledge-base/articles/how-to-install-a-local-mongodb-on-macos/?kw=&cpn=20425562857&utm_source=adwords&utm_medium=ppc&utm_term=&utm_campaign=P-Max+%7C+Aug+23+%7C+USA&hsa_net=adwords&hsa_ad=&hsa_src=x&hsa_ver=3&hsa_grp=&hsa_acc=1756351187&hsa_tgt=&hsa_mt=&hsa_kw=&hsa_cam=20425562857&gad=1&gclid=Cj0KCQjwm66pBhDQARIsALIR2zDpdaTAluQY8jUICrwRUXJSMt_XNeUWwneMWxxWl5jhIyGYphjKrM8aAjSmEALw_wcB)

* [How to install Mongodb 5](https://www.youtube.com/watch?v=s1WQ0eEpqqg)

### Install brew
* [Homebrew](https://brew.sh/)
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```
$ brew -v
```

```
$ vim ~/.bash_profile
export PATH=$PATH:/opt/homebrew/bin
$ source ~/.bash_profile
```

```
$ brew update

$ brew upgrade
```

### Install `xcode`
```
$ xcode-select --install
```

### Install mongodb

```
$ brew tap mongodb/brew               # where to install that package from
```

```
$ brew install mongodb-community@6.0
```

```
$ brew services start mongodb-community@6.0
$ brew services stop  mongodb-community@6.0
```

```
$ brew services list
```

```
$ mongod --config /opt/homebrew/etc/mongod.conf --fork
```

```
$ mongosh

test> show dbs
```

```
$ mkdir -p /data/db
$ sudo chown -R 4(whoami) /data/db
```

***

## 158. Database

* mongo -> DBs -> Collections -> Documents


* create a db
```
use <db name>
```

The above will use the database of the provided name if it exists, and create it if it doesn't

* `use` 
```
use <db name>
```

* example
```
use temp
```

The above will use the database of the provided name if it exists, and create it if it doesn't

* see current db
```
db
```

* see all db
```
show dbs
```

You need to have at least one document in a db for it to be seen.

* insert document
```
db.<collection name>.insert({"name":"McLeod"})
```

* example
```
db.dogs.insert({"name":"toby"})
```

* view documents
```
db.<collection name>.find()
```

* example
```
db.cats.insert({"firstname":"coco"})
```

```
db.cats.find().pretty()
```

* view collections
```
show collections
```

* drop db
```
db.dropDatabase()
```

***

## 159. Collection

```
test> db
test
test> show dbs
admin   40.00 KiB
config  72.00 KiB
local   72.00 KiB
test>
```

* create implicitly
```
db.<collection name>.insert({"name":"McLeod"})
```

* create explicitly
```
db.createCollection(<name>, {<optional options>})
```

* optional options

| option | type   | description   |
| ---    | ---    | ---           |
| capped | bool   | caps the size |
| size   | number | sets size of cap in bytes |
| max    | bool   | maximum number of documents allowed in capped collection |

[other options including validation](https://docs.mongodb.com/manual/reference/method/db.createCollection/)

* examples
```
db.createCollection("customers")
```

```
db.createCollection("crs", {capped:true, size:65536, max:1000000})
```

* view collections
```
show collections
```

* drop collection
```
db.<collection name>.drop()
```

***

## 160. Document


* insert
```
db.<collection name>.insert({document})
```

* insert multiple
```
db.<collection name>.insert(< [{document}, {document}, ..., {document}] >)
```
pass in an array of documents

* example
```
use playroom
```

```
db
```

```
show dbs
```

```
db.crayons.insert([
                    {
                        "hex": "#EFDECD", 
                        "name": "Almond", 
                        "rgb": "(239, 222, 205)"
                    }, 
                    {
                        "hex": "#CD9575", 
                        "name": "Antique Brass", 
                        "rgb": "(205, 149, 117)"
                    }, 
                    {
                        "hex": "#FDD9B5", 
                        "name": "Apricot", 
                        "rgb": "(253, 217, 181)"
                    }, 
                    {
                        "hex": "#78DBE2", 
                        "name": "Aquamarine", 
                        "rgb": "(120, 219, 226)"
                    }, 
                    {
                        "hex": "#87A96B", 
                        "name": "Asparagus", 
                        "rgb": "(135, 169, 107)"
                    }, 
                    {
                        "hex": "#FFA474", 
                        "name": "Atomic Tangerine", 
                        "rgb": "(255, 164, 116)"
                    }, 
                    {
                        "hex": "#FAE7B5", 
                        "name": "Banana Mania", 
                        "rgb": "(250, 231, 181)"
                    }
                ])
```
[source of crayon json](https://gist.githubusercontent.com/jjdelc/1868136/raw/c9160b1e60bd8c10c03dbd1a61b704a8e977c46b/crayola.json)


```
show collections
```

```
db.crayons.find()
```

```
db.crayons.drop()
```

```
db.dropDatabase()
```

***

## 161. Find(aka, query)


* setup
```
use store
db
show dbs
db.customers.insert([
    {"role":"double-zero","name": "Bond","      age": 32},
    {"role":"citizen"    ,"name": "Moneypenny", "age":32},
    {"role":"citizen"    ,"name": "Q",          "age":67},
    {"role":"citizen"    ,"name": "M",          "age":57},
    {"role":"citizen"    ,"name": "Dr. No",     "age":52}
])
```

* find
```
db.<collection name>.find()
db.customers.find()
```

* find one
```
db.<collection name>.findOne()
db.customers.findOne()
```

* find specific
```
db.customers.find({"name":"Bond"})
db.customers.find({name:"Bond"})
```
You can do it either way: ```"name" or name```. JSON specification is to enclose name (object name-value pair) in double qoutes

* and
```
db.customers.find({$and: [{name:"Bond"}, {age:32}]})
db.customers.find({$and: [{name:"Bond"}, {age:{$lt:20}}]})
db.customers.find({$and: [{name:"Bond"}, {age:{$gt:20}}]})
```

* or
```
db.customers.find({$or: [{name:"Bond"}, {age:67}]})
db.customers.find({$or: [{name:"Bond"}, {age:{$lt:20}}]})
db.customers.find({$or: [{name:"Bond"}, {age:{$gt:32}}]})
```

* and or
```
db.customers.find({role:"citizen"})
db.customers.find({age:52})
db.customers.find({$and: [{role:"citizen"}, {age:52}]})
db.customers.find({$or:  [{role:"citizen"}, {age:52}]})
db.customers.find({$or:  [{role:"citizen"}, {age:52}, {name:"Bond"}]})
```

```
db.customers.find(
    {$or:[
            { $and : [ { role : "citizen" }, { age : 32 } ] },
            { $and : [ { role : "citizen" }, { age : 67 } ] }
        ]
    }
)
```

* regex
```
db.customers.find({name: {$regex: '^M'}})
```

[regex cheatsheet](regex.pdf)

* pretty
```
db.<collection name>.find().pretty()
```
pretty prints the results

* operators

| operator | syntax | example |
| --- | --- | --- |
| equality | {key:value} | db.customers.find({"name":"Bond"}).pretty() | 
| less than | {key:{$lt:value}} | db.customers.find({"age":{$lt:20}}).pretty() | 
| less than equals | {key:{$lte:value}} | db.customers.find({"age":{$lte:20}}).pretty() | 
| greater than | {key:{$gt:value}} | db.customers.find({"age":{$gt:20}}).pretty() | 
| greater than equals | {key:{$gte:value}} | db.customers.find({"age":{$gte:20}}).pretty() | 
| not equals | {key:{$ne:value}} | db.customers.find({"age":{$ne:20}}).pretty() | 


* JSON reminder
JavaScript Object Notation (JSON) is a text format for the serialization of structured data.

It is derived from the object literals of JavaScript.

JSON can represent four primitive types (strings, numbers, booleans, and null) and two structured types (objects and arrays)

* Primitive JSON

Here are four small JSON texts containing only values:

```
"Hello world!"
42
true
null
```

* Object JSON

An object structure is represented as a pair of curly brackets surrounding zero or more **name-value** pairs (or members).

An object is an unordered collection of zero or more **name:value** pairs

A **name** is a string

A **value** is a string, number, boolean, null, object, or array.

Declare properties using **name:value** pairings separated by commas

Enclose names in curly braces

There is no trailing comma

This is a JSON object:

```
{
    "Image": {
        "Width":  800,
        "Height": 600,
        "Title":  "View from 15th Floor",
        "Thumbnail": {
            "Url":    "http://www.example.com/image/481989943",
            "Height": 125,
            "Width":  100
        },
        "Animated" : false,
        "IDs": [116, 943, 234, 38793]
    }
}
```

* Array JSON

An array structure is represented as square brackets surrounding zero or more values (or elements).

Elements are separated by commas.

A value must be an

```
object
array
number
string
three literal names
true
false
null
```

This is a JSON array containing two objects:

    [
        {
           "precision": "zip",
           "Latitude":  37.7668,
           "Longitude": -122.3959,
           "Address":   "",
           "City":      "SAN FRANCISCO",
           "State":     "CA",
           "Zip":       "94107",
           "Country":   "US"
        },
        {
           "precision": "zip",
           "Latitude":  37.371991,
           "Longitude": -122.026020,
           "Address":   "",
           "City":      "SUNNYVALE",
           "State":     "CA",
           "Zip":       "94085",
           "Country":   "US"
        }
    ]

* Number

The representation of numbers is similar to that used in most programming languages. A number is represented in base 10 using decimal digits. It contains an integer component that may be prefixed with an optional minus sign, which may be followed by a fraction part and/or an exponent part. Leading zeros are not allowed. A fraction part is a decimal point followed by one or more digits.

* String

The representation of strings is similar to conventions used in the C family of programming languages. A string begins and ends with **double quotation marks**.

source: The Internet Engineering Task Force (IETF)

***

## 162. Update

* update will update a record

* save will overwrite a record

* update
```
db.<collection name>.update(<selection criteria>, <update data>, <optional options>)
```

```
db.customers.find()
```
gives this data

```
{ "_id" : ObjectId("5891221756867ebff44cc885"), "role" : "double-zero", "name" : "Bond",       "age" : 32 }
{ "_id" : ObjectId("5891221756867ebff44cc886"), "role" : "citizen",     "name" : "Moneypenny", "age" : 32 }
{ "_id" : ObjectId("5891221756867ebff44cc887"), "role" : "citizen",     "name" : "Q",          "age" : 67 }
{ "_id" : ObjectId("5891221756867ebff44cc888"), "role" : "citizen",     "name" : "M",          "age" : 57 }
{ "_id" : ObjectId("5891221756867ebff44cc889"), "role" : "citizen",     "name" : "Dr. No",     "age" : 52 }
```

update like this
```
db.customers.update({_id:ObjectId("5891221756867ebff44cc886")},{$set:{role:"double-zero"}})
```

```
db.customers.update({name:"Moneypenny"},{$set:{role:"double-zero"}})
```

```
db.customers.update({name:"Moneypenny"},{$set:{role:"citizen", name: "Miss Moneypenny"}})
```

```
db.customers.update({age:{$gt:35}},{$set:{role:"double-zero"}})
```

```
db.customers.update({age:{$gt:35}},{$set:{role:"double-zero"}}, {multi:true})
```
[see options](https://docs.mongodb.com/manual/reference/method/db.collection.update/)

```
db.customers.update({},{$set:{role:"citizen"}}, {multi:true})
```
[see query documentation](https://docs.mongodb.com/manual/tutorial/query-documents/)

("5893888012acb8ada532a8e4"

* save
```
db.customers.save({"role":"villain", "name":"Jaws", "age":43})
```

```
db.customers.save({"_id":ObjectId("5891221756867ebff44cc889"), "role":"villain", "name":"Goldfinger", "age":77})
```

```
db.customers.save({"_id":ObjectId("5893888012acb8ada532a8e4"), "role":"villain", "name":"PussyGalore", "age":31})
```

***

## 163. Remove

***

## 164. Projection

***

## 165. Limit

***

## 166. Sort

***

## 167. Index

***

## 168. Aggregation

***

## 169. Users

***

## 170. JSON

***

## 171. Create Read Update Delete (CRUD)

***




























