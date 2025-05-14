## Mongo DB
- MongoDB is a NoSQL database that stores data in BSON (Binary JSON) format.
- It is a document oriented Database.


- **Database**   : A container for collections.                                               
- **Collection** : A group of MongoDB documents (similar to a table in RDBMS).                
- **Document**   : A record in BSON format (similar to a row in RDBMS).                       
- **Field**      : A key-value pair in a document.                                            
- **_id**       : A unique identifier for each document, automatically created if not given.

### DataTypes
- String, Number, Boolean, Array, Object, Date, Null, ObjectId

## MongoDB Command Notes

### **Basic Commands**

1. **View all databases**

```
show dbs
```

2. **Create or switch to a database**

```
use dbname
```

3. **View current database**

```
db
```

4. **Delete a database**

```
db.dropDatabase()
```

### **Collections**

5. **Show collections**

```
show collections
```

6. **Create a collection**

```
db.createCollection("comments")
```

7. **Drop a collection**

```
db.comments.drop()
```

---

### **CRUD Operations**

8. **View all documents in a collection**

```
db.comments.find()
```

9. **Find a single document**

```js
db.comments.findOne({ name: "soil" })
```

10. **Insert a document**

```
db.comments.insert({ name: "soil", age: 25 })
```

11. **Insert many documents**

```
db.comments.insertMany([
  { name: "Soil", age: 25 },
  { name: "Grame", age: 26 }
])
```

12. **Search with a condition**

```
db.comments.find({ name: "soil" })
```

13. **Limit and count**

```
db.comments.find().limit(2)
db.comments.find().count()
```

14. **Update one document**

```
db.comments.updateOne(
  { name: "soil" },
  { $set: { name: "Grame", age: 29 } }
)
```

15. **Update many documents**

```
db.comments.updateMany(
  { age: { $lt: 30 } },
  { $set: { verified: true } }
)
```

16. **Delete one document**

```
db.comments.deleteOne({ name: "soil" })
```

17. **Delete many documents**

```
db.comments.deleteMany({ age: { $lt: 20 } })
```

18. **Increment a field**

```
db.comments.update(
  { name: "soil" },
  { $inc: { age: 2 } }
)
```

19. **Rename a field**

```
db.comments.update(
  { name: "soil" },
  { $rename: { name: "test" } }
)
```

### **Query Operators**

20. **Comparison operators**

```
db.comments.find({ age: { $eq: 25 } })         // Equal
db.comments.find({ age: { $ne: 25 } })         // Not equal
db.comments.find({ age: { $gt: 25 } })         // Greater than
db.comments.find({ age: { $gte: 25 } })        // Greater than or equal
db.comments.find({ age: { $lt: 25 } })         // Less than
db.comments.find({ age: { $lte: 25 } })        // Less than or equal
db.comments.find({ age: { $in: [25, 30] } })   // In array
db.comments.find({ age: { $nin: [20, 22] } })  // Not in array
```

21. **Logical operators**

```
db.comments.find({
  $and: [{ age: { $gt: 20 } }, { age: { $lt: 30 } }]
}) // Both conditions must match

db.comments.find({
  $or: [{ name: "soil" }, { age: 25 }]
}) // Either condition matches

db.comments.find({
  $nor: [{ name: "soil" }, { age: 25 }]
}) // Neither condition matches

db.comments.find({
  age: { $not: { $gt: 25 } }
}) // Does not match the condition
```

22. **Evaluation operators**

```
db.comments.find({ name: { $regex: /soil/i } })     // Regex match (case-insensitive)

db.comments.find({ $text: { $search: "soil" } })     // Full-text search (requires text index)

db.comments.find({
  $where: function () {
    return this.age > 25 && this.name === "soil"
  }
}) // JavaScript expression
```

### **Extra Useful Commands**

23. **Sort**

```
db.comments.find().sort({ age: 1 })  // Ascending
db.comments.find().sort({ age: -1 }) // Descending
```

24. **Projection (select specific fields)**

```
db.comments.find({}, { name: 1, _id: 0 })
```

25. **Regex search**

```
db.comments.find({ name: /soil/i })
```

26. **Aggregation (example)**

```
db.comments.aggregate([
  { $match: { age: { $gt: 25 } } },
  {
    $group: {
      _id: "$name",
      total: { $sum: "$age" }
    }
  }
])
```



