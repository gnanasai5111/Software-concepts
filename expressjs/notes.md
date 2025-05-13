## Express
- Express.js is a fast, minimalist web framework for Node.js.
- It simplifies server creation, routing, middleware, and handling requests and responses.

## Basic Express Server

```
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

## Middleware in Express
- Middleware in Express.js is a function that has access to the request (req), response (res), and the next middleware function (next) in the request-response cycle.
- Middleware acts like a pipeline for each HTTP request . It can modify the request and response objects, end the request-response cycle, or call the next middleware function or handle errors.

### Middleware Function Signature

```
function middlewareName(req, res, next) {
  // do something
  next(); // Pass control to the next middleware
}
```

## Types of Middleware

### 1. Application-level Middleware
- Applies to the whole app.

```
const express = require('express');
const app = express();

// Logging middleware
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // Pass to next middleware/route
});
```

You can also apply it only to specific routes:

```
app.use('/admin', (req, res, next) => {
  console.log('Admin access');
  next();
});
```

### 2. Built-in Middleware

#### `express.json()` – Parses incoming JSON

```
app.use(express.json());
```

#### `express.urlencoded()` – Parses form data

```
app.use(express.urlencoded({ extended: true }));
```

#### `express.static()` – Serves static files

```
app.use(express.static('public'));
```

---

### 3. Router-level Middleware
- Used with an Express Router.

```
const router = require('express').Router();

router.use((req, res, next) => {
  console.log('Time:', Date.now());
  next();
});

router.get('/', (req, res) => {
  res.send('Home from router');
});

module.exports = router;
```

In `index.js`:

```
const userRouter = require('./routes/userRouter');
app.use('/users', userRouter);
```

### 4. Error-handling Middleware

Defined with **4 parameters**: `(err, req, res, next)`

```
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

Use it after all routes and other middleware.


### 5. Third-party Middleware

```
npm install morgan
```

```
const morgan = require('morgan');
app.use(morgan('dev'));
```





## Routing in Express

### Basic Routing

```
app.get('/about', (req, res) => {
  res.send('About Page');
});

app.post('/data', (req, res) => {
  res.send('Data Posted');
});
```

### Route Parameters

```
app.get('/user/:id', (req, res) => {
  res.send(`User ID is ${req.params.id}`);
});
```

### Query Parameters

```
app.get('/search?id=1', (req, res) => {
  res.send(`Query: ${req.query.id}`);
});
```

## Express Router
- Routers help split your app into modular files. Great for scalability.

### `userRoutes.js`

```
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

### `index.js`

```
const express = require('express');
const app = express();
const userRoutes = require('./routes/userRoutes');

app.use('/users', userRoutes); // All routes prefixed with /users

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

## Serving Static Files

```
app.use(express.static('public'));
```

`public/index.html` will be served when hitting `/`



