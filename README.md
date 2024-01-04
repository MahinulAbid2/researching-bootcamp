### Table content
1. [higher order function](#higher-order-function)
2. [express router](#express-router)



<br>

## Higher order function
* A function that returns another function is called a `higher-order function.` This concept is common in programming languages that support functional programming,
* where functions are treated as first-class citizens and can be passed around as arguments or returned from other functions.
* The way higher function works is pretty complicated in the begining.
```javascript
const a = (fn) => {
    return () => {
        fn(); // executing callback heree
        // fn will not execute untill I execute the returned function
        // calling "a" will not execute the returned function
    }
}

const outerFunction = () => {
    console.log('this is a function passed to higher order function as arguments')
}

let z = a(outerFunction);
/* 
this returns another function to z variable 
that returned function is not yet executed
even If I call "a" function, the "z" function will not be executed instantly
*/

z()
// this is executing the returned function.
// TIP: theory can only take you far. Test it in online javascript compiler and feel the pattern. Use practical
```


<br>
<br>

## Express Router
* Express Router is a class in Express.js Framework.
* It allows to create `modular route handlers`.
*  It provides a way to organize different routes and their corresponding handlers into separate modules or files.
*  This is RouterHandler FIle:
```javascript
const express = require('express');
const router = express.Router();

// Define routes using the router instance
router.get('/', (req, res) => {
  res.send('Homepage');
});

router.get('/about', (req, res) => {
  res.send('About page');
});

// Export the router to use in other files
module.exports = router;

```

* This is main.js file
```javascript
const express = require('express');
const app = express();

// Import the router module
const mainRouter = require('./routes/mainRouter');

// Mount the router at a specific path
app.use('/main', mainRouter);

// Start the server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});

```

* Setting up middleware in router
```javascript
// Middleware specific to the router
router.use((req, res, next) => {
  console.log('Router-specific middleware');
  next();
});

router.get('/protected', (req, res) => {
  res.send('Protected route');
});

```
