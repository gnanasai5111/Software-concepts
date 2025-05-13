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
- Middleware functions are functions that have access to `req`, `res`, and `next()`.

```
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

## Built-in middleware:

```
app.use(express.json()); // To parse JSON in POST requests
app.use(express.urlencoded({ extended: true })); // For form data
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

## Error Handler Middleware

```
app.use((err, req, res, next) => {
  res.status(500).send('Internal Server Error');
});
```


