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




 ### **MongoDB Command Notes** #### **Basic Commands** 1. **View all databases** ```js show dbs ``` 2. **Create or switch to a database** ```js use dbname ``` 3. **View current database** ```js db ``` 4. **Delete a database** ```js db.dropDatabase() ``` #### **Collections** 5. **Show collections** ```js show collections ``` 6. **Create a collection** ```js db.createCollection("comments") ``` 7. **Drop a collection** ```js db.comments.drop() ``` #### **CRUD Operations** 8. **View all documents in a collection** ```js db.comments.find() ``` 9. **Find a single document** ```js db.comments.findOne({ name: "soil" }) ``` 10. **Insert a document** ```js db.comments.insert({ name: "soil", age: 25 }) ``` 11. **Insert many documents** ```js db.comments.insertMany([ { name: "Soil", age: 25 }, { name: "Grame", age: 26 } ]) ``` 12. **Search with a condition** ```js db.comments.find({ name: "soil" }) ``` 13. **Limit and count** ```js db.comments.find().limit(2) db.comments.find().count() ``` 14. **Update one document** ```js db.comments.updateOne( { name: "soil" }, { $set: { name: "Grame", age: 29 } } ) ``` 15. **Delete a document** ```js db.comments.remove({ name: "soil" }) // deprecated // or use db.comments.deleteOne({ name: "soil" }) ``` 16. **Increment a field** ```js db.comments.update( { name: "soil" }, { $inc: { age: 2 } } ) ``` 17. **Rename a field** ```js db.comments.update( { name: "soil" }, { $rename: { name: "test" } } ) ``` #### **Query Operators** 18. **Comparison operators** ```js db.comments.find({ age: { $lt: 25 } }) // Less than db.comments.find({ age: { $lte: 25 } }) // Less than or equal db.comments.find({ age: { $gt: 25 } }) // Greater than db.comments.find({ age: { $gte: 25 } }) // Greater than or equal db.comments.find({ age: { $ne: 25 } }) // Not equal db.comments.find({ age: { $in: [25, 30] } }) // In list db.comments.find({ age: { $nin: [20, 22] } }) // Not in list ``` #### **Extra Useful Commands** 19. **Sort** ```js db.comments.find().sort({ age: 1 }) // Ascending db.comments.find().sort({ age: -1 }) // Descending ``` 20. **Projection (select specific fields)** ```js db.comments.find({}, { name: 1, _id: 0 }) ``` 21. **Regex search** ```js db.comments.find({ name: /soil/i }) ``` 22. **Aggregation (example)** ```js db.comments.aggregate([ { $match: { age: { $gt: 25 } } }, { $group: { _id: "$name", total: { $sum: "$age" } } } ]) ``` --- Let m
