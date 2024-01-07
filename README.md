### Table content
1. [higher order function](#higher-order-function)
2. [express router](#express-router)
3. [Catch without try](#Catch-without-try)
4. [throw new Error() breakdown](#throw-new-Error-breakdown)
5. [Understanding the Error Object](#Understanding-the-Error-Object)
6. [Node.js package research](#Nodejs-package-research)



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

<br>
<br>

## Catch without try
## .catch() /Promise.prototype.catch()
* `catch()` can be confused with `try{} catch(err) {}`.
* Both are a different. Not same.
* SIMILARITY: is that-- they both work for `promise`.
* This `catch()` basically calls a function when a promise is rejected.
```javascript
const promise1 = new Promise((resolve, reject) => {
  throw new Error('Uh-oh!');
});

promise1.catch((error) => {
  console.error(error);
});
// Expected output: Error: Uh-oh!
```

<br>

# throw new Error() breakdown
* Error is a class which is used to store error.
* By the keyword `new Error()` -  I'm instantiating a new class's object.
* I already know what is instantiating a new class. But I'm re-defining it here:
```javascript
class Hello {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    
    print() {
        console.log(`${this.firstName} and ${this.lastName}`);
    }
}

// this is instantiating a new class
// means creating a new object from the class Prototype
const helloObject = new Hello("john", "smith");
// now "helloObject" is an OBJECT instantiated from "Hello" class

// instantiating means creating object from a class
console.log(helloObject)
```
<br>

* Just like that, `Error` is also a class. I'm instantiating it
```javascript
class Error {
    constructor(message) {
        this.message = message;
    }
    // this is an error object
}


const x = new Error('Something went wrong');
```
> This is exactly how Error looks like. I learned about the error but I never knew how it works behind the scene.

* `throw` is nothing but a keyword that throws something at `console`.
* And the `console` thinks it's an error. No matter what you throw at it.
```javascript


throw "hello"

/*
EXPECTED OUTPUT:
----------------------------------
throw "hello"
^
hello 
(Use `node --trace-uncaught ...` to show where the exception was thrown)
*/
```
* So, the console thinks its an error. Meanwhile I just threw just a string. Nothing else.
* I can use `thow` keyword with any data type including `Object`. It simply will throw something at console.
* `throw new Error("error message")` - I'm instantiating a new Error Object from `Error` class and `throw`ing them in the console at the same time. 

<br>

# Understanding the Error Object
* Error.captureStackTrace()

<br>
<br>

# Node.js package research
### What is `morgan`?
```
- Morgan is a node package manager.
- Morgan is a logging tool (middleware) that can be used in HTTP servers implemented using Express & Node.js.
- It can be used to log requests, errors, and more to the console.

- It logs information in the console to make development easier.
- This makes development easier. Easy to implement.
```
![image](https://github.com/MahinulAbid2/researching-bootcamp/assets/70069009/e002641a-3c4a-433b-9499-1e5d4f239a69)

<br>

### What is `express-rate-limit`?
```
-Rate limiting prevents the same IP address from making too many requests that
 will help us prevent attacks like brute force.
- It blocks if same IP is making many request at the
  same time.
```

<br>

### What is `helmet`?
```
- Helmet can help protect your app from some well-known web vulnerabilities by
  setting HTTP headers appropriately.
- Generally, Helmet is just a collection of smaller middleware functions
  that set security-related HTTP headers
- If you use middleware like helmet or cors after you define a route,
  then that middleware will not apply to that route, it will only apply to routes defined
  after the middleware.
```

<br>

### What is `express-mongo-sanitize`?
```
- Express Mongo Sanitize is a package that provides middleware to sanitize "user-input"
  before it is used in a database query. It is designed specifically to prevent NoSQL
  injection attacks in Node. js applications that use MongoDB.
```

<br>

### What is `xss-clean`?
```
The “xss-clean” library helps prevent XSS attacks by removing
or encoding potentially dangerous characters and scripts from user input.
```

<br>

### What is `hpp`?
```
- hpp = http parameter pollution

```
![image](https://github.com/MahinulAbid2/researching-bootcamp/assets/70069009/e11ac746-8ebf-4413-8997-58fd785af22e)
![image](https://github.com/MahinulAbid2/researching-bootcamp/assets/70069009/a6011ab5-ca02-4689-bf1a-aa616b6a4356)

<br>

### What is `compression`?
```
- It compress user uploaded files like images from "req" object.
```

<br>

### What is `cors`?
```
- CORS in node. js stands for Cross-Origin Resource Sharing. It is a mechanism by
  which resources are shared across different servers.
- Single-origin policy is important for safety however, blocks external requests.
- We need CORS to bypass this feature.
```

<br>

### What is `body-parser`?
```
- Body parser middleware is an essential component in Express applications.
- It processes incoming request bodies, making it easier to handle POST and PUT requests.
- By parsing the body of an HTTP request and attaching it to the `req.body` property,
  it simplifies data extraction and manipulation in server-side logic
- According to chatGPT body-parser can also process and simplify "multi-part" form data.
```

<br>

### What is `cookie-parser`?
```
- Cookie parser is a software library used in web development that
  helps to parse ( parsing means to analyze or break up something ) and extract cookie data from HTTP requests
```

<br>

### What is `crypto`?
```
- Crypto is a node.js "built-in" module.
```

































