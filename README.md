### Table content
1. [helo](#higher-order-function)
2. 



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
```
