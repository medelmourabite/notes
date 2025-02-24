# Express.js interview quesitons

## A. Express

### 1. Advantages?

1. simple and light weight
2. Middleware support
3. Flexible routing system
4. Template engine integration

### 2. How to use?

```
// Install express: npm install express
const express = require('express');

const app = express();

app.get('/', (req, res) => {
    res.send('Hello World');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

## B. Middleware

The middleware is a function that handles an http request, performs some operations (cors, body-parser, auth...) and calls the `next()` function in the chain until it reaches the request handler (This is called a `request pipeline`)

### 1. How to use middleware?

```
const myMiddleware = (req, res, next) => {
    console.log('Hello from middleware');
    next();
};

// Application level middleware: apply to all routes below
app.use(myMiddleware);

// Route level middleware: Use for specific routes
app.use('/example', myMiddleware);

// Use per route
app.get('/', myMiddleware, (req, res) => {});

```

### 2. Types of middlewares:

#### 2.1. Application level

Apply to all routes below

#### 2.2. Route level

Apply to specific route/sub routes

#### 2.3. Error handling

The error middleware is the last middleware in the request pipeline. it captures errors from the request pipeline using the error object parameter, log it, and send a user friendly error page to the client

```
// Some error
app.use((req, res, next) => {

    next(new Error('Something went wrong'));
});

// Error handling middleware
app.use((err, req, res, next) => {
    console.log(err.stack)
    res.status(500).send("Some user friendly error message");
});
```

#### 2.4. Build in middleware

Express comes with a set of built in middleware functions.

```
// Serves static files from the public folder
app.use(express.static('public'));

// Parse incoming requests with JSON payloads
app.use(express.json());

// Parse incoming requests with urlencoded payloads
app.use(express.urlencoded({ extended: true }));
```

#### 2.5. Third party middleware

1. cors: Cross origin resource sharing
2. body-parser: Parse POST requests body with JSON payloads
3. cookie-parser: Parse cookies
4. helmet: Helmet helps you secure your Express apps by setting various HTTP security headers.
5. compression: Compress responses

### 3. Advantages of using middleware

1. Modularity: modulirize the code into smaller self-contained units
2. Reusability
3. Improved request handling: validate the request, parse the request, and modify the response
4. Flexible control flow: Can be applied globally or on a per-route basis
5. Thir party middlewares

## C. Routing

Routing is the process of direction incoming http requests to the corresponding handler functions based on the url path and method.

### 1. What is the diiference between routing and middleware?

Middleware is a function
Routing is a process of mapping requests to handlers

### 2. How to use?

```
app.get('/', (req, res) => {
    res.send('Hello World');
});

app.post('/',  (req, res) => {
    res.send('Hello World');
});
```

### 4. How to use in a real application?

```
// index.js
const express = require('express');
const app = express();

// import routes
const userRoutes = require('./routes/user');

// use routes
app.use('/users', userRoutes);

// /routes/user.js
const express = require('express');
// Create a router object
const router = express.Router();

// import controller
const userController = require('../controllers/user');

// define routes using router methods
router.get('/', userController.getUsers);
router.post('/', userController.createUser);

// export router
module.exports = router;
```

### 5. What are Route Parameters?

Allows to capture the dynamic part of the url.

```
app.get('/users/:id', (req, res) => {
    const userId = req.params.id;
    res.send(`User with id ${userId}`);
});
```

### 6. Router Methods

Methods of router object:

1. router.get(path, callback)
2. router.post(path, callback)
3. router.put(path, callback)
4. router.delete(path, callback)

### 7. What is Route Chaining?

It is the process of chaining multiple middleware functions to a single route.

```
router.get('/users', middleware1, middleware2, (req, res) => {
    res.send('Hello World');
});
```

### 8. What is Route Nesting?

Route Nesting organizes the routes in a hierarchical manner, by grouping them under a common parent route.

```
// /routes/user.js
router.get('/', (req, res)  => {});
router.get(':id',  (req, res)  => {});
router.get(':id/posts',  (req, res)  =>  {} );

// /index.js
app.use('/users', userRouter);

```

## D. Template Engine

A template engine is library used to generate HTML content by combining data with a static HTML template.
Such as:

1. Handlebars
2. EJS
3. Pug

### 1. How to use EJS in Express?

1. Install ejs: npm install ejs
2. Create views folder
3. Create the template file index.ejs inside views folder
4. Set the view engine in app.js

```
// /views/index.ejs
<html>
    <head>
        <title>Home Page</title>
    </head>
    <body>
        <h1><%= name %></h1>
    </body>
</html>
```

```
//  /index.js
const express = require('express');
const app = express();
const path = require('path');

// Set the view engine
app.set('view engine', 'ejs');

// Set the views folder
app.set('views', path.join(__dirname, 'views'));

// Use the render method
app.get('/',  (req, res)  => {
    res.render('index', {name: 'John'});
});
```
