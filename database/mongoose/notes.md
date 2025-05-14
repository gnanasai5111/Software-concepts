### **Mongoose Notes**

Mongoose is an **ODM (Object Data Modeling)** library for MongoDB and Node.js, providing a straightforward way to interact with MongoDB databases. It allows you to define schemas and models for your data, making it easier to handle data validation, relationships, and queries.

---

### **1. Setting up Mongoose**

#### **Install Mongoose**:

```bash
npm install mongoose
```

#### **Connecting to MongoDB**:

```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/yourDB', {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
.then(() => console.log('Connected to MongoDB'))
.catch(err => console.error('Failed to connect to MongoDB', err));
```

* **Explanation**: The `connect()` method connects to the MongoDB database.

  * Replace `'mongodb://localhost:27017/yourDB'` with your actual MongoDB URI.
  * `useNewUrlParser` and `useUnifiedTopology` are options to handle MongoDB's internal connection logic.

---

### **2. Mongoose Schema and Model**

#### **Schema**:

A schema is the structure of the data in MongoDB, defining what data fields are required and their data types.

```js
const mongoose = require('mongoose');

// Define a schema
const commentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  age: { type: Number, required: true },
  message: String,
  createdAt: { type: Date, default: Date.now }
});
```

* **Explanation**: This schema defines the `name`, `age`, `message`, and `createdAt` fields for a `comment`.

#### **Model**:

A model is a wrapper around the schema and provides an interface for interacting with the database.

```js
const Comment = mongoose.model('Comment', commentSchema);
```

* **Explanation**: `mongoose.model()` creates a model based on the schema, which is then used to interact with the `comments` collection.

---

### **3. CRUD Operations with Mongoose**

#### **Create**:

* **Single Document**:

```js
const newComment = new Comment({
  name: 'Alice',
  age: 25,
  message: 'Great post!'
});

newComment.save()
  .then(comment => console.log('Comment saved:', comment))
  .catch(err => console.error('Error saving comment:', err));
```

* **Multiple Documents**:

```js
const comments = [
  { name: 'Alice', age: 25, message: 'Great post!' },
  { name: 'Bob', age: 30, message: 'Nice article!' }
];

Comment.insertMany(comments)
  .then(result => console.log('Comments added:', result))
  .catch(err => console.error('Error adding comments:', err));
```

---

#### **Read**:

* **Find All Documents**:

```js
Comment.find()
  .then(comments => console.log('All comments:', comments))
  .catch(err => console.error('Error fetching comments:', err));
```

* **Find Documents with Conditions**:

```js
Comment.find({ age: { $gte: 25 } })
  .then(comments => console.log('Comments with age >= 25:', comments))
  .catch(err => console.error('Error fetching comments:', err));
```

* **Find a Single Document**:

```js
Comment.findOne({ name: 'Alice' })
  .then(comment => console.log('Found comment:', comment))
  .catch(err => console.error('Error finding comment:', err));
```

* **Find and Return Specific Fields**:

```js
Comment.find({ age: { $gte: 25 } }, { name: 1, age: 1 })
  .then(comments => console.log('Comments (name, age only):', comments))
  .catch(err => console.error('Error fetching comments:', err));
```

---

#### **Update**:

* **Update One Document**:

```js
Comment.updateOne({ name: 'Alice' }, { $set: { age: 26 } })
  .then(result => console.log('Update result:', result))
  .catch(err => console.error('Error updating comment:', err));
```

* **Update Many Documents**:

```js
Comment.updateMany({ age: { $gte: 30 } }, { $set: { message: 'Updated message' } })
  .then(result => console.log('Updated many comments:', result))
  .catch(err => console.error('Error updating comments:', err));
```

---

#### **Delete**:

* **Delete One Document**:

```js
Comment.deleteOne({ name: 'Alice' })
  .then(result => console.log('Deleted comment:', result))
  .catch(err => console.error('Error deleting comment:', err));
```

* **Delete Many Documents**:

```js
Comment.deleteMany({ age: { $lte: 25 } })
  .then(result => console.log('Deleted many comments:', result))
  .catch(err => console.error('Error deleting comments:', err));
```

---

### **4. Mongoose Validation**

Mongoose allows you to add **validation rules** to your schema fields to ensure data integrity.

#### **Example**:

```js
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  age: { type: Number, min: 18, max: 100 }
});
```

* `required`: Makes the field mandatory.
* `unique`: Ensures no two documents have the same value for the field.
* `min` / `max`: Validates the field's value is within a certain range.

---

### **5. Mongoose Middleware (Hooks)**

Mongoose provides middleware (also called **hooks**) that you can use to run logic before or after certain actions, such as saving or deleting documents.

#### **Example**: Run a function before saving a document (`pre` hook).

```js
commentSchema.pre('save', function (next) {
  if (this.age < 18) {
    throw new Error('Age must be 18 or older');
  }
  next(); // Continue to save the document
});
```

* **Explanation**: This middleware runs before saving a `comment` document and throws an error if the age is less than 18.

#### **Example**: Run a function after saving a document (`post` hook).

```js
commentSchema.post('save', function (doc) {
  console.log('Comment saved:', doc);
});
```

* **Explanation**: This middleware runs after the document has been successfully saved.

---

### **6. Virtuals in Mongoose**

**Virtuals** are fields that are not stored in MongoDB but are computed dynamically when accessing the document.

#### **Example**: Create a virtual field `fullName` for the `User` schema.

```js
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});
```

* **Explanation**: The `fullName` field will not be stored in the database but will be computed on the fly when you access it.

---

### **7. Mongoose Population**

Mongoose provides a powerful **population** feature that allows you to reference documents in other collections and join them together.

#### **Example**: Reference a `User` model inside a `Comment` model.

```js
const userSchema = new mongoose.Schema({
  name: String
});

const commentSchema = new mongoose.Schema({
  message: String,
  userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});

// Populate the 'userId' field with the full User document
Comment.findOne({ message: 'Great post!' })
  .populate('userId')
  .then(comment => console.log('Comment with user:', comment))
  .catch(err => console.error('Error fetching comment:', err));
```

* **Explanation**: When calling `populate('userId')`, Mongoose will replace the `userId` field with the actual document from the `User` collection.

---

### **8. Mongoose Queries with `exec`**

You can use `.exec()` to execute a query and get a promise.

```js
Comment.find({ age: { $gte: 25 } }).exec()
  .then(comments => console.log('Comments:', comments))
  .catch(err => console.error('Error:', err));
```

* **Explanation**: `exec()` returns a promise, which allows you to handle asynchronous behavior with `.then()` and `.catch()`.


