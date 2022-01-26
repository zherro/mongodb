# mongoDB

## What is it?\

## Why use mongoDB?


## DataTypes

- **Text:** String value. Ex: "Sample text"
- **Boolean:** `true` or `false`
- **Number:**
- - **Integer:** (int32) integer value
- - **NumberLong:** (int64) long integer value
- - **NumberDecimal:** decimal value
- **ObjectId:** registry unique id. Ex: ObjectId("asdf")
- **ISODate:** ISODate("2022-01-28")
- **Timestamp:** Timestamp(1142532)
- **Embedded Document:** {"a": {...}}
- **Array:** {"b": [..]}


## Commands and functions

### List all collections - db.getCollectionNames()

Return all collections name


```
db.getCollectionNames()
```

### Create and Drop

```
db.createCollection("easyPeasy") # create collection
db.easyPeasy.drop()		 # drop collection

db.createCollection("easyPeasy") # create collection
```

### Insert - db.collection.insert()

Insert new data in collection

```
db.easyPeasy.insert(
   {
	id: 1
	shouldString: "string",
	couldInt: 0,
	mustBeDecimal: 10.123,
	thisIsDate: "2022-01-28 00:00:00",
	items : [
		{
			id: 1,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 2,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 3,
			value1: "teste",
			value2: 100,
			value3: 1.00
		}
	]	
   }
)
```

### InsertMany - db.collection.insertMany()

Insert more than one data in collection

```
db.easyPeasy.insertMany( [
  {
	id: 2,
	shouldString: "string",
	couldInt: 0,
	mustBeDecimal: 10.123,
	thisIsDate: "2022-01-28 00:00:00",
	items : [
		{
			id: 1,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 2,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 3,
			value1: "teste",
			value2: 100,
			value3: 1.00
		}
	]	
   },
   {
	shouldString: "string",
	couldInt: 0,
	mustBeDecimal: 10.123,
	thisIsDate: "2022-01-28 00:00:00",
	items : [
		{
			id: 1,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 2,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 3,
			value1: "teste",
			value2: 100,
			value3: 1.00
		}
	]	
   },
   {
	id: 3,
	shouldString: "string",
	couldInt: 0,
	mustBeDecimal: 10.123,
	thisIsDate: "2022-01-28 00:00:00",
	items : [
		{
			id: 1,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 2,
			value1: "teste",
			value2: 100,
			value3: 1.00
		},
		{
			id: 3,
			value1: "teste",
			value2: 100,
			value3: 1.00
		}
	]	
   }
])
```

**RESULT:**
```
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("61f05e8c3a205e3287e6f209"),
		ObjectId("61f05e8c3a205e3287e6f20a"),
		ObjectId("61f05e8c3a205e3287e6f20b")
	]
}
```

### Find db.collection.find({})

Find function allows to get data from collection
and too set filters for resume data

```
db.easyPeasy.find({})			# find all data
db.easyPeasy.find({}).count()		# find all data and count
```

#### Find: Greather Than and Less Then
```
db.easyPeasy.find({id: {$gt: 3}})	# return all where id greather than 3
db.easyPeasy.find({id: {$lt: 4}})	# return all where id less than 4
```

### Find db.collection.count()

Return a integer count of data in collection

```
db.easyPeasy.find({}).count()		# filter result data and count
db.easyPeasy.count()			# count all data in collection
```

### update - db.collection.update and db.collection.updateOne

**updateMany():** It update all documents in a collection with matching filter.

**updateOne():** It update only one top most document in a collection with matching filter.

**update():** By default, the update() method updates a single document. Include the option {multi : true} to update all documents that match the query criteria. Hence we can use it as both ways.

```
db.easyPeasy.updateOne({_id: ObjectId("61f05e8c3a205e3287e6f209")}, {$set: {id: 5}})
db.easyPeasy.updateOne({_id: ObjectId("61f05e8c3a205e3287e6f20a")}, {$set: {id: 3}})
```

```
# not registered ID
db.easyPeasy.updateOne({_id: ObjectId("61f05e8c3a205e3287e6f2dd")}, {$set: {id: 3}})
db.easyPeasy.find({_id: ObjectId("61f05e8c3a205e3287e6f2dd")}).count()
```

```
# not registered ID
db.easyPeasy.update({_id: ObjectId("61f05e8c3a205e3287e6f2dd")}, {$set: {id: 3}})
db.easyPeasy.find({_id: ObjectId("61f05e8c3a205e3287e6f2dd")}).count()
```

```
# update value2 of item
# in this example, is update de first result match
db.easyPeasy.update({items: {'$elemMatch':{ id: 3 }}}, {$set: {'items.$.value2': 30}})

# find fist result
db.easyPeasy.findOne()
```

```
# update value2 of all itens
# in this example, is update de first result match
db.easyPeasy.updateMany({items: {'$elemMatch':{ id: 3 }}}, {$set: {'items.$.value2': 30}})

# RESULT
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 3 }

# find fist result
db.easyPeasy.find({})
```




