Here’s a comprehensive GitHub-style note for **Express.js** that includes **theory**, **routers**, and **code examples**, all clearly formatted with `##` headings and \`\`\` code blocks. Great for revision or uploading to GitHub!

---

## 📘 What is Express.js?

* **Express.js** is a minimal and flexible **Node.js web application framework**.
* It simplifies the process of building server-side applications by handling:

  * Routing (URL handling)
  * Middleware (functions that run before sending a response)
  * HTTP requests/responses
  * Serving static files
* It's widely used to build **REST APIs**, **web servers**, and even **full-stack apps** (with a frontend).

---

## ⚙️ Installation

```bash
npm init -y
npm install express
```

---

## 🚀 Basic Express Server

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

---

## 🧱 Middleware in Express

Middleware functions are functions that have access to `req`, `res`, and `next()`.

```js
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

Built-in middleware:

```js
app.use(express.json()); // To parse JSON in POST requests
app.use(express.urlencoded({ extended: true })); // For form data
```

---

## 🛣️ Routing in Express

### Basic Routing

```js
app.get('/about', (req, res) => {
  res.send('About Page');
});

app.post('/data', (req, res) => {
  res.send('Data Posted');
});
```

### Route Parameters

```js
app.get('/user/:id', (req, res) => {
  res.send(`User ID is ${req.params.id}`);
});
```

### Query Parameters

```js
app.get('/search', (req, res) => {
  res.send(`Query: ${req.query.q}`);
});
```

---

## 🗂️ Express Router

Routers help split your app into modular files. Great for scalability.

### 📁 Folder Structure

```
project/
├── index.js
└── routes/
    └── userRoutes.js
```

### 📝 `userRoutes.js`

```js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('All users');
});

router.get('/:id', (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

module.exports = router;
```

### 📝 `index.js`

```js
const express = require('express');
const app = express();
const userRoutes = require('./routes/userRoutes');

app.use('/users', userRoutes); // All routes prefixed with /users

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

---

## 📄 HTTP Request Methods

| Method | Purpose                 |
| ------ | ----------------------- |
| GET    | Fetch data              |
| POST   | Create new resource     |
| PUT    | Replace entire resource |
| PATCH  | Modify part of resource |
| DELETE | Remove resource         |

```js
app.get('/item', (req, res) => res.send('GET'));
app.post('/item', (req, res) => res.send('POST'));
app.put('/item', (req, res) => res.send('PUT'));
app.patch('/item', (req, res) => res.send('PATCH'));
app.delete('/item', (req, res) => res.send('DELETE'));
```

---

## 🧍 Serving Static Files

```js
app.use(express.static('public'));
```

`public/index.html` will be served when hitting `/`

---

## 🛑 404 Not Found Handler

```js
app.use((req, res) => {
  res.status(404).send('Page Not Found');
});
```

---

## ⚠️ Error Handler Middleware

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Internal Server Error');
});
```

---

## 📚 Summary

* Express makes backend development with Node.js much easier.
* It supports REST API creation, routing, middleware, and error handling.
* Express Router allows modular structure for large applications.
* Middleware can preprocess requests or handle errors.
* Use HTTP methods (GET, POST, PUT, PATCH, DELETE) to define RESTful routes.

---

Would you like me to add **MongoDB integration**, **authentication (JWT)**, or **REST API project example** next?
